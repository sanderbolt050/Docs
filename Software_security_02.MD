## Software security 02
>In dit practicum gaan we aan de slag met het opsporen van beveiligingsproblemen binnen een webshop-applicatie. Voor deze opdracht werken we met OWASP ZAP (Open Web Application Security Project – Zed Attack Proxy) en Docker.

#### Installatie van OWASP ZAP
Het installeren van OWASP ZAP gaat via de website. Na selecteren van het juiste OS kan het downloaden beginnen.

Zoals aangegeven gebruik is Ubuntu. Ik heb gekozen om OWASP ZAP te installeren via de installer en niet de package. Als je dit download krijg je een bash script die al het werk voor je doet.

### Installatie Docker. 
Ik heb ervoor gekozen om Docker te installeren via apt. Dat gaat eenvoudig via de commandline met het commando. `sudo apt install docker`

##### Testen of Docker goed werkt
Om te of docker werkt kan je een test container aan zetten. Deze container heet hello-world. Alleen als ik die aanroep krijg ik een error. 
```sh
sabo@Macbook-Air:~$ docker run hello-world
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```
Hieruit kan je opmaken dat er een probleem is met de rechten. Ik kan als user `sabo` niet docker goed gebruiken. Als ik dit als sudo run kan het wel. 
```sh
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
719385e32844: Pull complete 
Digest: sha256:fc6cf906cbfa013e80938cdf0bb199fbdbb86d6e3e013783e5a766f50f5dbce0
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
```

Het is niet ideaal om elke de commando's als sudo te runnen. Daarom heb ik mijn groep toegevoegd aan de docker groep. 
```sh
 sudo usermod -aG docker sabo
 newgrp docker
```
Hierna kon ik docker gebruiken als `sabo` en hoefde ik het niet elke keer als root.
### Installatie van de Juice Shop-container
> Download en draai nu de Juice Shop Docker-container met de volgende commando’s:
`docker pull bkimminich/juice-shop
>docker run --rm -p 3000:3000 bkimminich/juice-shop
`

Hierna was het voor mij mogelijk om via `127.0.0.1:3000` de Juiceshop berijken.

## De opdracht: het opsporen van beveiligingsproblemen
> Toon je antwoord aan met een of meer screenshots waaruit duidelijk naar voren komt dat je succesvol bent ingelogd. Laat ook de invoer zien die deze illegale inlog mogelijk maakt. Beschrijf hierbij kort welke stappen je hebt uitgevoerd om tot je antwoord te komen. (20%)

Bij de eerste poging heb ik een `'` aan het einde van een fictieve email toegevoegd. Ook voerde ik een wachtwoord in. Daardoor kreeg ik de volgende melding in beeld: 

You successfully solved a challenge: Error Handling (Provoke an error that is neither very gracefully nor consistently handled.)

Ook stond boven de email een de volgede melding: `[object Object]`. Dit samen met de andere melding heb ik het idee dat ik op de goede weg ben. 

Nadat ik achter mijn email in totaal: `'OR 1=1;`. was ik binnen.


