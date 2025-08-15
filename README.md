# Seafile for armv/7/

## ! Achtung das Projekt wurde Für den rasperry pi 3 b erstellt kann aber auch in auf anderen maschinen die armv/7/ verwenden funktionieren wurde dort aber noch nicht getest ! 

### das projekt wurde bei den code+design camp erstellt https://code.design/

### verwendete tools:<br/>
-https://hub.docker.com/r/yobasystems/alpine-mariadb/<br/>
-https://hub.docker.com/r/arm32v7/memcached/<br/>
-https://hub.docker.com/r/franchetti/seafile-arm\

## Quickstart
nachdem ihr rasperry pi os fertig instaliert habt (https://www.raspberrypi.com/documentation/computers/getting-started.html#setting-up-your-raspberry-pi)
instaliert ihr docker (https://docs.docker.com/engine/install/)
und erstellt im docker ordner einen ordner
```
mkdir seafile
cd seafile
```
im anschluss erstellt ihr ein docker compose file mit den befehl
```
nano docker-compose.yml
```
und fügt in diesen den docker compose file ein 
(denkt daran das man strg+shift+c/v zum kopieren bentzen muss)
```dockerfile
services:
  db:  # MariaDB-Datenbank für Seafile
    image: yobasystems/alpine-mariadb
    container_name: seafile-database
    environment:
      MYSQL_ROOT_PASSWORD: example_password
      MYSQL_DATABASE: seafiledb
      MYSQL_USER: seafileuser
      MYSQL_PASSWORD: example_password
    restart: always

  memcache:  # Caching-Service
    image: arm32v7/memcached
    container_name: seafile-memcached
    command:
      - --conn-limit=1024
      - --memory-limit=64
      - --threads=4
    restart: always

  seafile:  # Hauptdienst (Web-UI & Dateisync)
    image: franchetti/seafile-arm
    container_name: seafile
    ports:
      - "8000:8000"  # Web-Interface
      - "80:8000"    # HTTP
      - "8082:8082"  # Dateiübertragung
      - "443:443"    # HTTPS
    volumes:
      - /opt/seafile-data:/data  # Persistente Daten
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
nun ersetzt ihr die example_password und die example@mail.com 
danach entfernt ihr die komentare.
Nun drückt ihr strg+x zurück zu gehen
als nächstes gebt ihr in die command line diesen text ein
```
docker-compose up
```
## client instalation
als erstes geht ihr zur seafile websit und ladet euch dort den client 
runter welcher für euch passt (https://www.seafile.com/en/download/)
und führt die datei aus. Im anschluss müssen wir die ip unseres host geräts
heraus finden dafür tippt ihr ein 
```
ip a
```
die ip findet man meist als
```
inet 192.168.1.42/24
```
danach tippt ihr oben die adresse ein 
```
http://ip_adresse:portnumber
#example:
http://192.168.37.142:80
```
dann gibt ihr noch eure email und euer passwort ein und seit verbunden

## troubleshooting 

```
Operation not permitted
```
wenn etwas mit diesen fehler kommt müsst ihr beim composen sudo dazugeben also:
```
sudo docker-compose up
```
<br/>

```
docker services must be a mapping
docker mapping values are not allowed in this context
```
wenn ihr diesen fehler bekommen habt sind ihrgendwo im docker-compose 
noch leezeichen oder es ist nicht richtig eingerückt

