# Software security 
###### Week 1 - Sander Bolt 
Deze opdrachten zijn gemaakt op een laptop die draait op ubuntu 20.04.
Ik heb mijn laptop met Windows en Ubuntu. Na het bekijken van de opdrachten heb ik gekozen om dit te maken op Ubuntu. 
Het is makkelijker om deze opdrachten direct op Linux te maken in plaats van WSL. 

### Opgave 1: Wachtwoord-fuzzing met Hydra

##### Hydra installeren (1 - voor Windows)
Ik heb de eerste stap kunnen overslaan, aangezien ik geen gebruik maak van WSL, zoals eerder vermeld.

#### Hydra installeren (2)
Ik had al in mijn homedir een map genaamd `school`. Hierin heb ik de map `SS` gemaakt. Waarna zoals aangegeven ik een submap voor de applicatie kon maken `Hydra`

Hydra kon ik installeren via de volgende commando's

```sh
git clone https://github.com/vanhauser-thc/thc-hydra.git hydra
cd hydra
./configure
sudo make
sudo make install
```

Nadat ik dit had gekopieerd en geplakt werkte het niet. Dit kwam onder adere doordat ik nog op enter of `y` moest invoeren bij het `git clone` commando. Ook had het te maken met de sudo commando waar ik mijn wachtwoord moest invullen. 

Nadat ik het een voor een had ingevoerd werkte.
Verder had ik geen problemen. `git` was al op mijn laptop geïnstalleerd. 

#### Hydra draaien op een webapp
Ik had geen webapp meer. Ik heb de van [webapp](https://github.com/hanze-hbo-ict/sw_sec_docs/tree/master/src/wc-wk1) van erik roos had gebruikt en alle flask modules had geïnstalleerd werkte dit ook weer en had ik een webapp om aan mee aan de slag te kunnen!

Eerst was het belangrijk om een account aan te maken. 
De inlog gegevens die ik had aagemaakt waren:
- Username: 123@gmail.com 
- Password: 123

Nadat ik de code die in de opdracht stond een beetje had aangepast werkte het niet helemaal. 
##### Mijn eerste poging

```sh
hydra -l 123@gmail.com -x 3:3:1 127.0.0.1 -s 5000 http-post-form "/login:email=^USER^&password=^PASS^:Inlog niet correct"
``` 
- `-l` geeft het email adres aan
- `-x` geeft de parameters van de de wachtwoord combinaties aan.
- `-s` De poort van de webapp
- `http-post-form` is het protocol die hydra zal gebruiken
- `"/login:email=^USER^&password=^PASS^` Is de plek waarop de username en password moeten in de request
- `:Inlog niet correct!` is de melding die je krijgt zodat Hydra weet dat de inlog niet goed is. 


De output die ik kreeg was niet helemaal te verwachten. Na wat troubleshooten kwam ik erachter dat de melding die Hydra verwacht als de inlog fout is niet helemaal klopt.

##### De eerste poging
```sh
Hydra v9.5-dev (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-05-30 01:40:10
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1000 login tries (l:1/p:1000), ~63 tries per task
[DATA] attacking http-post-form://127.0.0.1:5000/login:email=^USER^&password=^PASS^:Inlog niet correct
[5000][http-post-form] host: 127.0.0.1   login: 123@gmail.com   password: 002
[5000][http-post-form] host: 127.0.0.1   login: 123@gmail.com   password: 004
[5000][http-post-form] host: 127.0.0.1   login: 123@gmail.com   password: 013
[5000][http-post-form] host: 127.0.0.1   login: 123@gmail.com   password: 008

```

##### De verbeterde versie
Nadat dit was aangepast werkte de code een stuk beter.
```sh
hydra -l 123@gmail.com -x 3:3:1 127.0.0.1 -s 5000 http-post-form "/login:email=^USER^&password=^PASS^:Inlog mislukt"
Hydra v9.5-dev (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-05-30 01:47:02
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1000 login tries (l:1/p:1000), ~63 tries per task
[DATA] attacking http-post-form://127.0.0.1:5000/login:email=^USER^&password=^PASS^:Inlog mislukt
[5000][http-post-form] host: 127.0.0.1   login: 123@gmail.com   password: 123
[STATUS] 139.00 tries/min, 139 tries in 00:01h, 861 to do in 00:07h, 16 active
^CThe session file ./hydra.restore was written. Type "hydra -R" to resume session.
```
Zoals te zien heb ik de code eerder laten stoppen met Ctrl c.

### De opdracht
> Je gaat je eigen Webtech- of IOT-applicatie uit de vorige periode* brute-forcen! Maak een gebruiker aan met een simpel wachtwoord, bijvoorbeeld bestaande uit 3 cijfers, en kijk hoelang Hydra erover doet om het te kraken. Maak nu het wachtwoord stapsgewijs complexer door meer cijfers en eventueel letters en leestekens (pas dan wel je -x-parameter aan) toe te voegen, en noteer steeds hoelang Hydra erover doet. Welke wachtwoord-complexiteit vind jij veilig genoeg? Schaalt dit naar een echte productie-applicatie of gelden er dan toch nog strengere eisen, en waarom? 
> Benoem daarnaast drie mogelijkheden om dit soort brute-force-aanvallen tegen te gaan.
Lever een kort verslagje in over deze "penetration test" (pentest), inclusief screenshots van je Hydra-aanroeptijden, metingen, conclusies en tegenmaatregelen. (50%)

De drie accounts: 
- 123@gmail.com:123
- 1234@1234.nl:1234
- 12345@12345.nl:12345

De eerste heb ik al in de snippit hier boven laten zien. Daarvan is de uitkomst ongeveer 1 minuut. 

#### 4 cijfers. 
Om de vier cijfers zo efficiënt mogelijk te laten lopen moest je wel de `-x` vlag aanpassen. Deze heb ik aangepast naar: `4:4:1`. Het fijne hieraan is dat we vooraf al weten dat het wachtwoord 4 cijfers lang is. 

**3 minuten**
```sh
hydra -l 1234@1234.nl -x 4:4:1 127.0.0.1 -s 5000 http-post-form "/login:email=^USER^&password=^PASS^:Inlog mislukt"
Hydra v9.5-dev (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-05-30 02:07:50
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 10000 login tries (l:1/p:10000), ~625 tries per task
[DATA] attacking http-post-form://127.0.0.1:5000/login:email=^USER^&password=^PASS^:Inlog mislukt
[STATUS] 473.00 tries/min, 473 tries in 00:01h, 9527 to do in 00:21h, 16 active
[5000][http-post-form] host: 127.0.0.1   login: 1234@1234.nl   password: 1234
[STATUS] 418.00 tries/min, 1254 tries in 00:03h, 8746 to do in 00:21h, 16 active

```
#### 5 cijfers
Hiervoor moest je weer de `-x` flag aanpassen. Dit had ik aangepast naar `5:5:1`. Hierbij weten natuurlijk weer van te voren dat wachtwoord 5 cijfers lang is.

**30 minuten**
```sh
1sabo@Macbook-Air:~/school/ss$ hydra -l 12345@12345.nl -x 5:5:1 127.0.0.1 -s 5000 http-post-form "/login:email=^USER^&password=^PASS^:Inlog mislukt"
Hydra v9.5-dev (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-05-30 02:11:17
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 100000 login tries (l:1/p:100000), ~6250 tries per task
[DATA] attacking http-post-form://127.0.0.1:5000/login:email=^USER^&password=^PASS^:Inlog mislukt
[STATUS] 459.00 tries/min, 459 tries in 00:01h, 99541 to do in 03:37h, 16 active
[STATUS] 435.00 tries/min, 1305 tries in 00:03h, 98695 to do in 03:47h, 16 active
[STATUS] 425.43 tries/min, 2978 tries in 00:07h, 97022 to do in 03:49h, 16 active
[STATUS] 423.93 tries/min, 6359 tries in 00:15h, 93641 to do in 03:41h, 16 active
[5000][http-post-form] host: 127.0.0.1   login: 12345@12345.nl   password: 12345

```

### Tot slot - opdracht 1
In deze eerste opdracht zijn er 3 aanroepingen gedaan op Hydra. Hierbij was van te voren al bekend hoe lang het wachtwoord was en dat het alleen uit cijfers bestaat. Nou heb ik natuurlijk niet de aller snelste laptop. Het genereren van wachtwoorden en verwerken van requests kost energie is dus niet de aller snelste. 

Volgens deze [website](https://www.security.org/how-secure-is-my-password/) zouden mijn wachtwoorden direct worden gekraakt. Dat valt niet te zien in de testen op mijn laptop. Maar in ideale omstandigheden is dit wel zo. Daarom zou ter aller tijden een wachtwoord van minimaal 12 tekens met letters, hoofdletters, cijfers en leestekens moeten gebruiken. Als je dat gebruikt zou het 400000 jaar duren voordat hij is gekraakt. 

Een goed en sterk wachtwoord gebruiken is het enige wat je als gebruiker altijd kan doen. 

Er zijn verschillende maatregelen die je als website host kan doen. 
Dit zijn onder andere: 
- 2FA: Dit voorkomt dat als je wachtwoord is geraden de gebruiker alsnog binnenkomt. Je moet dan alsnog toestemming geven via je telefoon. 
- Het bannen van IP adressen die heel veel requests maken. Hierdoor kan het brutefocen ook niet meer werken omdat de IP adressen worden gebanned als ze te veel requests hebben. 
- Ook zou een robot verificatie ook helpen. Om bij elke inlog te verivieren of het wel een mens is dat inlogt. 


Dit zijn naar mijn mening de beste oplossing die je kan toepassen om brute force te voorkomen.

### Opgave 2: Fuzzing met Radamsa
Het installeren ging hierbij met de commando's 

```sh
git clone https://gitlab.com/akihe/radamsa.git radamsa
cd radamsa
sudo make
sudo make install
```
Ook hierbij kon ik niet alles in mijn Command line plakken maar moest ik 1 voor 1 alles plakken. 

#### Testen
Na de installatie is het natuurlijk de vraag of redamsa werkt. 
```sh
sabo@Macbook-Air:~/school/ss$ echo "Dit is een teststring" | radamsa
Dit is een teststrinit is een teststring�gg
```

Hierin valt uit op te maken dat redamsa werkt. 

#### Voorbeeld 1
Voor het eerste voorbeeld heb ik eerst het bestand `examples/hello.txt` aangemaakt.
```
Test

12345
```

Nadat ik het commando: `radamsa examples/hello.txt` meerde malen heb uitgevoerd kreeg ik elke keer een andere output. 
```sh
sabo@Macbook-Air:~/school/ss$ radamsa examples/hello.txt


Test
0
Test
437
sabo@Macbook-Air:~/school/ss$ radamsa examples/hello.txt
T�dLe󠁼st

18446744073709551615󠁈5
sabo@Macbook-Air:~/school/ss$ 
```

#### Voorbeeld 2

> Gebruik -n voor het aantal varianten dat je wilt genereren door radamsa en geef daarnaast met -o het pad naar fuzz-cases op. Het commando ziet er dan zo uit: `radamsa -n 10 -o 'fuzz-cases/hello-%n.%s' examples/hello.txt` Ga naar de map fuzz-cases en bekijk hier de gefuzzde bestanden.

Nadat ik dit had uitgevoerd vonf ik 10 bestanden in de map `fuzz-cases`. Hierin zag je dat de groote van de alle bestanden niet overeen kwam.

```sh
sabo@Macbook-Air:~/school/ss$ radamsa -n 10 -o 'fuzz-cases/hello-%n.%s' examples/hello.txt
sabo@Macbook-Air:~/school/ss$ ll fuzz-cases/
total 48
drwxrwxr-x 2 sabo sabo 4096 mei 30 12:38 ./
drwxrwxr-x 5 sabo sabo 4096 mei 30 12:38 ../
-rw------- 1 sabo sabo   27 mei 30 12:38 hello-10.txt
-rw------- 1 sabo sabo    7 mei 30 12:38 hello-1.txt
-rw------- 1 sabo sabo   14 mei 30 12:38 hello-2.txt
-rw------- 1 sabo sabo   12 mei 30 12:38 hello-3.txt
-rw------- 1 sabo sabo    8 mei 30 12:38 hello-4.txt
-rw------- 1 sabo sabo   17 mei 30 12:38 hello-5.txt
-rw------- 1 sabo sabo   12 mei 30 12:38 hello-6.txt
-rw------- 1 sabo sabo   12 mei 30 12:38 hello-7.txt
-rw------- 1 sabo sabo   12 mei 30 12:38 hello-8.txt
-rw------- 1 sabo sabo   12 mei 30 12:38 hello-9.txt
```

### De opdracht
> a. Leer radamsa kennen. Ga er mee aan de slag en kijk wat het doet. Raadpleeg hiervoor ook aanvullende informatie op internet en ga in overleg met klasgenoten.

Het handigste om meer te leren over een programma op linux is via het `man` commando. Dit commanndo laat het manual zien van het programma. 

##### options
Hier een paar van de belangrijke options bij redamsa; 
- `-o` Output. Geef aan waar de data moet worden geschreven.
- `-n` Count. Hoe veel outputs redamsa moet generen
- `-r` Recursive. Maakt de code recursief
- `-v` Verbose. Laat alle stappen zien

>b. Kies een aantal bronnen om de fuzzer op toe te passen (minimaal 3). Radamsa kun je toepassen op tekstbestanden, afbeeldingen, codefragmenten etc.

##### Drie bronnen. 
1. Plaatje van een kitten. 
2. Text bestand met inhoud
3. Een stukje code. 

###### Plaatje van een kitten
Om goed te kijken wat de effecten zijn moet redamsa meerdere keren worden aangeroepen. Je kan de zelfde code gebruiken die je gekregen hebt in voorbeeld een. 
```sh
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ radamsa -n 10 -o  'kitten/fuzzed/kitten-%n.%s' kitten/kitten.jpg 
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ ls kitten/fuzzed/
kitten-10.jpg  kitten-2.jpg  kitten-4.jpg  kitten-6.jpg  kitten-8.jpg
kitten-1.jpg   kitten-3.jpg  kitten-5.jpg  kitten-7.jpg  kitten-9.jpg
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ ls kitten/fuzzed/ -l
total 1116
-rw------- 1 sabo sabo 112250 mei 30 13:27 kitten-10.jpg
-rw------- 1 sabo sabo 111719 mei 30 13:27 kitten-1.jpg
-rw------- 1 sabo sabo 114878 mei 30 13:27 kitten-2.jpg
-rw------- 1 sabo sabo 111666 mei 30 13:27 kitten-3.jpg
-rw------- 1 sabo sabo 111113 mei 30 13:27 kitten-4.jpg
-rw------- 1 sabo sabo 110373 mei 30 13:27 kitten-5.jpg
-rw------- 1 sabo sabo 112109 mei 30 13:27 kitten-6.jpg
-rw------- 1 sabo sabo 109879 mei 30 13:27 kitten-7.jpg
-rw------- 1 sabo sabo 112087 mei 30 13:27 kitten-8.jpg
-rw------- 1 sabo sabo 111075 mei 30 13:27 kitten-9.jpg
```
Zoals te zien in de grootte zijn ze niet allemaal hetzelfde. Als je probeert om de foto's te openen zijn ze allemaal anders. Veel kan je niet neer openen, de rest die je nog wel kan openen zijn niet meer goed. Er missen delen of ze zijn verkleurd of Kleiner gemaakt.

###### Textbestand met inhoud. 
Ook hier kan je weer hetzelfde commando als de vorige keer gebruiken:.
`radamsa -n 10 -o  'lorum/fuzzed/lorum-%n.%s' lorum/lorum.txt `

Ook nu valt weer te verwachten dat er 10 nieuwe bestanden zijn. 
```sh
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ ls lorum/fuzzed/ -l
total 56
-rw------- 1 sabo sabo   579 mei 30 13:35 lorum-10.txt
-rw------- 1 sabo sabo  2375 mei 30 13:35 lorum-1.txt
-rw------- 1 sabo sabo  1531 mei 30 13:35 lorum-2.txt
-rw------- 1 sabo sabo  2196 mei 30 13:35 lorum-3.txt
-rw------- 1 sabo sabo   474 mei 30 13:35 lorum-4.txt
-rw------- 1 sabo sabo 16757 mei 30 13:35 lorum-5.txt
-rw------- 1 sabo sabo  1168 mei 30 13:35 lorum-6.txt
-rw------- 1 sabo sabo   640 mei 30 13:35 lorum-7.txt
-rw------- 1 sabo sabo   672 mei 30 13:35 lorum-8.txt
-rw------- 1 sabo sabo  1329 mei 30 13:35 lorum-9.txt
```

###### De code:
Ook hiervoor gebruik je de zelfde manier als eerder. 
`radamsa -n 10 -o  'code/fuzzed/code-%n.%s' code/python.py `
Hierdoor krijg je weer 10 nieuwe bestanden. 
```sh
-rw------- 1 sabo sabo  310 mei 30 13:42 code-10.py
-rw------- 1 sabo sabo  469 mei 30 13:42 code-1.py
-rw------- 1 sabo sabo  638 mei 30 13:42 code-2.py
-rw------- 1 sabo sabo  346 mei 30 13:42 code-3.py
-rw------- 1 sabo sabo  244 mei 30 13:42 code-4.py
-rw------- 1 sabo sabo  615 mei 30 13:42 code-5.py
-rw------- 1 sabo sabo  482 mei 30 13:42 code-6.py
-rw------- 1 sabo sabo  365 mei 30 13:42 code-7.py
-rw------- 1 sabo sabo  359 mei 30 13:42 code-8.py
-rw------- 1 sabo sabo  311 mei 30 13:42 code-9.py
```

Van de code werkte heel veel niet meer op 3 na. Hierbij was dan alleen het print statement aangepast of het commentaar.
Hier de nog werkende en het orgineel.

```sh
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ python3 code/fuzzed/code-10.py 
['Mango', 'Grape', 'Orange', 'Guava', 'Banana']
The fruit list after delete:
['Mango', 'Grape', 'Orange', 'Banana']
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ python3 code/fuzzed/code-9.py 
The fruit list after insert:
['Mango', 'Grape', 'Orange', 'Guava', 'Banana']
['Mango', 'Grape', 'Orange', 'Banana']
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ python3 code/fuzzed/code-8.py 
The fruit list after insert:
['Grape', 'Mango', 'Orange', 'Guava', 'Banana']
The fruit list after delete:
['Grape', 'Mango', 'Orange', 'Banana']
sabo@Macbook-Air:~/school/ss/Fuzz_cases$ python3 code/python.py  #Het orgineel.
The fruit list after insert:
['Mango', 'Grape', 'Orange', 'Guava', 'Banana']
The fruit list after delete:
['Mango', 'Grape', 'Orange', 'Banana']
```

Helaas ben ik al mijn werk kwijtgeraakt schoolwerk kwijtgeraakt. Vandaar dat ik later helemaal opnieuw moest beginnen met de opdracht.




