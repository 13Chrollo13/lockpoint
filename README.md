# Seafile for armv/7/

## 🇩🇪 wenn du deutsch bist findest du ein deutsches readme unter [deutsches readme](README_german.md)

## ❗ Please note: This project was created for the Raspberry Pi 3b, but it may also work on other machines that use armv/7/, although it hasn't been tested on them yet ❗

### The project was created at the code+design camp https://code.design/

### 🛠️ Tools used:<br/>
-https://hub.docker.com/r/yobasystems/alpine-mariadb/<br/>
-https://hub.docker.com/r/arm32v7/memcached/<br/>
-https://hub.docker.com/r/franchetti/seafile-arm\

## 🏁start
After you have finished installing Raspberry Pi OS (https://www.raspberrypi.com/documentation/computers/getting-started.html#setting-up-your-raspberry-pi), install Docker (https://docs.docker.com/engine/install/)
and create a folder in the Docker folder:
```
mkdir seafile
cd seafile
```
Then create a Docker Compose file using the command
```
nano docker-compose.yml
```
and insert the docker compose file into it
(remember to use ctrl+shift+c/v to copy)
```dockerfile
services:
  db:  # MariaDB database for Seafile
    image: yobasystems/alpine-mariadb
    container_name: seafile-database
    environment:
      MYSQL_ROOT_PASSWORD: example_password
      MYSQL_DATABASE: seafiledb
      MYSQL_USER: seafileuser
      MYSQL_PASSWORD: example_password
    restart: always

  memcache:  # Caching service
    image: arm32v7/memcached
    container_name: seafile-memcached
    command:
      - --conn-limit=1024
      - --memory-limit=64
      - --threads=4
    restart: always

  seafile:  # Main service (web UI & file sync)
    image: franchetti/seafile-arm
    container_name: seafile
    ports:
      - "8000:8000"  # Web interface
      - "80:8000"    # HTTP
      - "8082:8082"  # File transfer
      - "443:443"    # HTTPS
    volumes:
      - /opt/seafile-data:/data  # Persistent data
    environment:
      MYSQL_HOST: db
      MYSQL_ROOT_PASSWD: example_password
      MYSQL_USER: seafileuser
      MYSQL_USER_PASSWD: example_password
      SEAFILE_ADMIN_EMAIL: example_email
      SEAFILE_ADMIN_PASSWORD: example_password
    depends_on:
      - db
      - memcache

```
Now replace example_password and example@mail.com
then remove the comments.
Now press Ctrl+X to go back.
Next, enter this text into the command line:
```
docker-compose up
```
## client installation
First, go to the Seafile website and download the client that works for you (https://www.seafile.com/en/download/)
and run the file. Next, we need to find the IP of our host device.
To do this, type:
```
ip a
```
The IP can usually be found as:
```
inet 192.168.1.42/24
```
Then type in the address above:
```
http://ip_address:portnumber
#example:
http://192.168.37.142:80
```
Then enter your email address and password and you're connected.

## 🔧 troubleshooting

```
Operation not permitted
```
If you get this error, you need to add sudo when composing, like this:
```
sudo docker-compose up
```
<br/>

```
docker services must be a mapping
docker mapping values are not allowed in this context
```
If you get this error, There are still spaces somewhere in docker-compose, or it is not indented properly.
