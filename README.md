# Seafile for armv/7/

## ! Achtung das Projekt wurde Für den rasperry pi 3 b erstellt kann aber auch in auf anderen maschinen die armv/7/ verwenden funktionieren wurde dort aber noch nicht getest ! 

### das projekt wurde bei den code+design camp erstellt #link einfügen

verwendete tools:
-(https://hub.docker.com/r/yobasystems/alpine-mariadb/)
-(https://hub.docker.com/r/arm32v7/memcached/)
-(https://hub.docker.com/r/franchetti/seafile-arm)

nachdem ihr den rasperry pi instaliert habt ((https://www.raspberrypi.com/documentation/computers/getting-started.html#setting-up-your-raspberry-pi)) 
instaliert ihr docker ((https://docs.docker.com/engine/install/))
erstellt ihr im docker ein ordner
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
```
```
nun ersetzt ihr die example_password und die example@mail.com 
danach entfernt ihr die komentare.
Nun drückt ihr strg+x zurück zu gehen
als nächstes gebt ihr in die command line diesen text ein
```
docker compose
```


