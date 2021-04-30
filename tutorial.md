# Step 1: GitHub Link kopieren 
https://github.com/echtelerp/IoT-Stack-tutorial

# Step 2: 
Github repository auf raspberry Pi clonen
dazu installieren wir zuerst git auf dem pi
wir loggen uns mittels 
> ssh pi@dockerPi 
am rasperry pi an.
dann:
> sudo apt-get install git

der clone befehl klont das git Repository in die location an der ihr euch im moment befindet. also das Home Verzeichnis. 
mit:
> git clone https://github.com/echtelerp/IoT-Stack-tutorial.git 

> ls -la lassen wir uns dieses anzeigen. 
 mit cd <muss ich noch einfügen>
 navigieren wir in das geklonte verzeichnis. 
 > noch ein ls -la 
 zeigt uns die struktur an. 

# Step 3: wir schauen uns die neue Struktur an

Ich mache bei allen meine Projekten die selbe Struktur.
Jeweils der container den ich einbinden will bekommt einen Ordner 
z.B. der Ordner nodered. 
In den Ordner lege ich leeres ein dockerfile. 
Im einfachsten Fall ist im file nur des Basis Image mittels FROM  Statemen eingebunden. Also im dockerfile: 

> FROM ...

Wie kommt man zu den basis images: 
dazu suchen wir die container auf dockerhub unter:
https://hub.docker.com

die verwendeten Seiten in diesem Tutorial sind folgende:

Grafana: https://hub.docker.com/r/grafana/grafana
NodeRed: https://hub.docker.com/r/nodered/node-red
MQTT Broker: https://hub.docker.com/_/eclipse-mosquitto
InfluxDB: https://hub.docker.com/_/influxdb

Ich habe also schon für jeden Serive den ich nutzen will genau das gemacht. 

# Step 4: 
Wir schauen uns die Docker Compose datei an. 

Jeder Container ist als ein Service deklariert. 
damit die Container untereinader und miteinander sprechen können gibt es die networks option. 
um sicherzustellen, dass die einstellungen persistent sind habe ich jeweils auch die volumes benannt. 
Der teil ports gibt an weleche ports aus dem container gemappt sind. 

nun da wir für jeden service einen ordner mit einem Dockerfile haben nutzen wir den build befehl um die container auch bauen zu lassen. Dies hat im späteren den vorteil, dass wir direkt konfigurationen etc. mit in den Container bauen können. 


# Step 5: 
> docker-compose up -d 

mit dem Befehl starten wir den gesamten Service Stack. 


jetzt testen wir das ganze: 

zuerst 
> docker ps

dann navigieren wir in einem browser zu
> dockerPi:1880 -> nodered
dann in einem neuen Tab zu: 
> dockerPi:3000 -> grafana

und spielen dort ein bisschen herum :-) 

umd den stack zu beenden in der Kmandozeile:

> docker-compose down

> docker volume prune
um die volumes zu löschen wenn wir diese nicht mehr benötigen, 

> docker image prune 
um die nicht mehr benötigten Images zu löschen, 

> docker network prune 
um die nicht mehr benötigten netzwerke zu löschen

wie wir nun individuelle einstellungen vornehmen an den Images, 
das gibt es im nächsten Video. 

Zum nachlesen zu Docker: 
http://docs.docker.com

