# V2X-Simulation-with-SUMO

**Önlab beszámolóm a részletesebb leírásért:** [OneDrive](https://1drv.ms/w/s!AjD91zSjiAZsiIdOOtHze_bp4kE-Xg)

Program grafikus felületén még nem minden funkció működik, hibakezelés sincsen még a különböző funkciókra.
A simulation/ mappa tartalmaz egy SUMO szimulációt.
A saved_maps/ mappa a kiszerializát térképet tartalmazza, ezt első indítás és betöltés után hozza létre.

# Indítás
Program indítását követően meg kell adni a SUMO konfigurációs fájlt, ez a simulation/map.sumo.cfg. Ez betölti a térképet, járműveket. Közben a gpsfake fülön elindítható a gpsfake, a listából ki kell választani a betöltött járművet, majd elindítani a gpsfkaket a "Run gpsfake" gombbal. A szövegdobozba beírt parancs jó a gpsfake elindításához, azt nem szükséges módosítani. Ha nem szükséges gpsfake a szimulációhoz, akkor nem kell indítani. Simulation fülön a "Start simulation"-el indítható a szimuláció, ez elindítja a SUMO-t. Csatlakozni a jármű-kommunikációs eszközzel jelenleg a 11111 porton lehet, telnettel ki lehet próbálni. A portot a config.yaml fájlban lehet módosítani. Jelenleg a jármű azonosítója a SUMO-beli azonosítóval megegyezik.
A parancsok JSON-ben TCP socketben lehet küldeni a Orchestrátornak, az a kiválasztott scenarió alapján feldolgozza, belerakja egy parancs queue-ba. Innen a szimulációt futtató szál kiveszi és az adott entitiás feldolgozza azt.
Kiadható parnacsokra példa:
- 	Jármű egy adott pozícióra irányítása: ```{"vehicleID":"555","command":"DST","destination":{"x":47.47363,"y":19.05289}}```
- 	Jármű sebességének megadása (m/s): ```{"vehicleID":"555","command":"SPEED","speed":10.5}```
-   Jármű útvonalának lekérése: ```{"vehicleID":"555","command":"ROUTE"}```
-   Jármű útvonala: ```{"command":"ROUTE","vehicleID":"555","route":["37392508","126765651",...]}```
# Vedd figyelembe
- A lejebb linkelt SUMO és opcionálisan gpsfake kell a program működéséhez
- GPSD miatt a program csak Linux alatt működik
- GUI-n a funkciók egy része nem működik, nem erre helyeztem a fókuszt, így nem működnek a következő, de remélem a közeljövőben meg tudom csinálni:
-- gpsfake példányok leállítása, újraindítása
-- Ha betöltöttél egy configurációs fájlt, de másikat szeretnél, akkor indítsd újra a programot, nem írja felül
- Szálak nagyrészére nincs megírva, hogy program leállításkor leálljon (IDE stop gomb)
- gpsfake indítás szintaktikáját és más szintaktikát is tartsd, mert a program nem ellenőrzi

# Külső programok
- SUMO [telepítés](http://www.sumo.dlr.de/userdoc/Installing.html)
- SUMO [wiki](http://sumo.dlr.de/wiki/Simulation_of_Urban_MObility_-_Wiki)
- Módosított [gpsfake](https://github.com/szzso/GPSD-with-management)