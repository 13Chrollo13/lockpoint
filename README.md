# Seafile for armv/7/

## ! Achtung das Projekt wurde Für den rasperry pi 3 b erstellt kann aber auch in auf anderen maschinen die armv/7/ verwenden funktionieren wurde dort aber noch nicht getest ! 

### das projekt wurde bei den code+design camp erstellt (https://code.design/)

verwendete tools:
-(https://hub.docker.com/r/yobasystems/alpine-mariadb/)
-(https://hub.docker.com/r/arm32v7/memcached/)
-(https://hub.docker.com/r/franchetti/seafile-arm)

nachdem ihr rasperry pi os fertig instaliert habt ((https://www.raspberrypi.com/documentation/computers/getting-started.html#setting-up-your-raspberry-pi)) 
instaliert ihr docker ((https://docs.docker.com/engine/install/))
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
```
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

```
danach tippt ihr oben die adresse ein 
```

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


```
docker services must be a mapping
docker mapping values are not allowed in this context
```
wenn ihr diesen fehler bekommen habt sind ihrgendwo im docker-compose 
noch leezeichen oder es ist nicht richtig eingerückt

