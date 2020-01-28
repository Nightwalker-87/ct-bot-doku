# Erweiterungsmodul für den c't-Bot

Das Erweiterungsmodul ergänzt den c't-Bot um einen Steckplatz für SD- oder MMC-Karten (Massenspeicher), einen zum [USB-2-Bot-Adapter](usb-2-bot.md) pinkompatiblen Steckverbinder und um eine Netzwerk-Schnittstelle.
Letztere wird über den Embedded Wireless Device Server [WiPort](https://www.lantronix.com/products/wiport/) von Lantronix realisiert. _(externer Link)_
Zu dessen Funktionsumfang gehört unter anderem ein WLAN Accesspoint nach dem Standard 802.11 b/g und eine 10/100 Mbit Fast Ethernet Netzwerk Schnittstelle.
Das Netzwerk-Modul ist über die serielle Schnittstelle mit dem Mikrocontroller auf der Hauptplatine verbunden und erlaubt so eine Kommunikation des c't-Bots per LAN oder WLAN.

Bei der Netzwerk-Schnittstelle, inklusive der zugehörigen Komponenten (Netzwerkmodul und RJ45-Buchse), handelt es sich um eine Bestückungsoption, welche die Funktion des übrigen Erweiterungsmoduls nicht beeinträchtigt.
Entsprechend kann je nach individuellem Wunsch auf die Bestückung dieser Teile auch verzichtet werden.

Eine detaillierte Beschreibung des gesamten Erweiterungsmoduls findet sich im c't-Artikel
[c't 2/2007, S.184 ff](https://www.heise.de/ct/artikel/Aussendienstler-290830.html): "Außendienstler - Funkmodul, Massenspeicher und Klappe für den c't-Bot".


## Schaltplan & Bestückungsplan

* [Schaltplan Erweiterungsplatine](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/schematics/05_extensionboard.pdf)
* [Bestückungsplan Erweiterungsplatine](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/pcb-layout/05_pcb_extensionboard.pdf)


## Elektronik-Komponenten & Stückliste Erweiterungsplatine

| Bauteil            | Bezeichnung                                                  | Bemerkungen                                                               |
| :---               | :---                                                         | :---                                                                      |
| C1, C2             | Elektrolyt-Kondensator 470 uF                                | Polung beachten                                                           |
| C3 - C7, C9        | Keramik-Kondensator 100 nF                                   | Stempelung 104                                                            |
| D1 - D5            | Diode 1N4148                                                 | Polung beachten                                                           |
| IC1                | WLAN-Modul WiPort (WP2001000G)                               | _Bestückungsoption_                                                                          |
| IC2                | Spannungsregler LM3940IT-3,3                                 |                                                                           |
| IC3                | Dual Flip-Flop, D-Type 74HC74                                |                                                                           |
| IC4                | 4-fach Pegelwandler 74HCT125                                 |                                                                           |
| IC5, IC6           | 3-fach 2-Kanal Multiplexer 74HCT4053                         |                                                                           |
| J4 - J7            | Buchsenleisten (8x1)                                         | Bestückung erfolgt von unten                                              |
| J10                | SD-Kartenschacht                                             |                                                                           |
| J11                | Einzelstift, gewinkelt                                       |                                                                           |
| J12                | Stiftleiste (8x1), gewinkelt                                 |                                                                           |
| J14                | Buchsenleiste (3x2), gewinkelt                               | Bestückung erfolgt von unten; _falsche Platinen-Beschriftung als "ST5"_   |
| J15                | Stiftleiste (8x2), doppelreihig                              | optional: unbestückt                                                      |
| P1                 | RJ45-Buchse                                                  | mit Ferrit & Status-LEDs; _Bestückungsoption_                             |
| R4, R6, R8         | Widerstand 1,8 kΩ 1%                                         | Farbring-Kennung: braun-grau-schwarz-braun-braun                          |
| R5, R7, R9         | Widerstand 3,3 kΩ 1%                                         | Farbring-Kennung: orange-orange-schwarz-braun-braun                       |
| R10, R11           | Widerstand 220 Ω 1%                                          | Farbring-Kennung: rot-rot-schwarz-schwarz-braun                           |
| R12, R13, R16, R17 | Widerstand 10 kΩ 1%                                          | Farbring-Kennung: braun-schwarz-schwarz-rot-braun                         |
| R15                | Widerstand 4,7 kΩ 1%                                         | Farbring-Kennung: gelb-violett-schwarz-braun-braun                        |
| ST5                | 6-poliger Wannenstecker, gewinkelt                           | _falsche Platinen-Beschriftung als "J14"_                                 |
| SW2                | Kippschalter                                                 |                                                                           |


# Aufbauanleitung für das Erweiterungsmodul

Bei der Bestückung sollte mit den Buchsenleisten begonnen werden.
Zu beachten ist hier, dass die Buchsenleisten (J4, J5, J6, J7 und J14 (**Achtung: falsche Beschriftung als "ST5"!**)) von unten eingelötet werden:

![Image: 'extensionboard_01.jpg'](../images/extensionboard/extensionboard_01.jpg)

Anschließend sollte zunächst mit den kleinen Bauteilen fortgefahren werden.
Der SD/MMC-Kartenschacht (J10) muss plan auf der Platinenoberfläche aufliegen und in die Führungslöcher einrasten, bevor man ihn festlötet.

**Hinweis:** Vor dem Aufbau ist unbedingt zu prüfen, ob der dem Bausatz der Erweiterungsplatine beiligende SD-Kartenslot einen "Hebel" aufweist, der zum Auswerfen der Karte dient.
Dieser kollidiert mit dem dahinter liegenden IC und verhindert so ein korrektes Einsetzen einer SD-Karte (was später nicht sofort ersichtlich ist).
Allerdings kann der keine Hebel mit einer Zange zerstörungsfrei entfernt werden.
Die Bilder im Wiki zeigen diesen Auswurfmechanismus nicht, da die neuere Ausführung des Kartenschachts wahrscheinlich erst später im Zuge eines Herstellerwechsels den originalen Slot ersetzt hat.

Sobald alle Kleinteile ihren Platz auf der Platine gefunden haben, folgen die großen Komponenten.

**Hinweis:** Der Programmierstecker auf dem Erweiterungsmodul (ST5) (**Achtung: falsche Beschriftung als "J14"!**) ist aufgrund eines Fehlers im Design leider verdreht.
Um ihn mit der korrekten Pinbelegung zu verwenden muss das Flachbandkabel um 180 Grad gedreht eingesteckt werden.
Pin 1 zeigt dann nach vorne, in Richtung Transportfach des Bots.
Hierzu ist die kleine Nase am Flachbandstecker vorsichtig mit einem Teppichmesser zu entfernen.

Die RJ45-Netzwerkbuchse (P1) sollte ebenfalls möglichst eben auf der Platine aufsitzen, wozu die Federlaschen etwas wegzubiegen sind.

Die fertig bestückte Baugruppe sollte nach Abschluss der Arbeiten wie folgt aussehen:

![Image: 'extensionboard_02.jpg'](../images/extensionboard/extensionboard_02.jpg)

Auf die von unten eingelöteten Buchsenleisten (J4, J5, J6, J7 und J14 (**Achtung: falsche Beschriftung als "ST5"!**)) werden nun jeweils zwei weitere Reihen an Buchsenleisten aufgesteckt,
damit die Pins lang genug werden um die Hauptplatine stabil zu kontaktieren.

![Image: 'extensionboard_03.jpg'](../images/extensionboard/extensionboard_03.jpg)

Beim Einschrauben der WiPort-Antennenleitung auf die Platine sollte man nur eine der beiden mitgelieferten Federscheiben verwenden.
Diese sollte oberhalb der Platine eingefügt werden, damit die Buchse muss so hoch wie möglich sitzt.
**Das empfindliche Antennenkabel darf zu keinem Zeitpunkt geknickt oder starken Zugbelastungen ausgesetzt werden.**

![Image: 'extensionboard_04.jpg'](../images/extensionboard/extensionboard_04.jpg)

Für die Anbindung des Maussensors an das Erweiterungsmodul ist Pin 4 aus dem zehnpoligen Stecker für den Kabelstrang zum Maussensor zu entfernen.
Der Widerhaken, der den Kontakt im Stecker fixiert, lässt sich mit einer Nadel oder einem kleinen Schraubendreher leicht lösen.
Den an das kabelende gecrimpten Metallstift schneidet man ab und lötet stattdessen einen einzelnen Buchsenpin an das Kabelende an.

Dieser einzelne Pin wird später auf den Steckpin (J11) des Erweiterungsmodul gesteckt:

![Image: 'extensionboard_05.jpg'](../images/extensionboard/extensionboard_05.jpg)


### Einbau des Erweiterungsmoduls

Nun ist es an der Zeit die drei zehnpoligen Stecker wieder auf die Hauptplatine zu stecken.
Hier empfiehlt sich die Kabel mit Kabelbindern so festzuzurren, dass der Klappenarm der Transportfach-Erweiterung (sofern vorhanden) nicht daran schleift.

Die Erweiterungsplatine wird von oben auf die drei neuen Abstandsbolzen gesetzt, welche die Hauptplatine darunter in Position halten.
Bevor man das Erweiterungsmodul mit den drei Schrauben fixiert, die vor dem Umbau die Hauptplatine verschraubten, ist zu überprüfen, ob auch alle Stecker (J4, J5, J6, J7 und J14) sauberen Kontakt haben.

![Image: 'extensionboard_06.jpg'](../images/extensionboard/extensionboard_06.jpg)

Dabei sollte nochmals darauf geachtet werden, dass das WiPort-Antennenkabel weder abknickt noch starke Zugbelastungen erfährt.

**Sofern das optionale LCD-Display aus dem Bausatz verwendet wird, ist bei dessen Montage nun darauf zu achten, dass dieses die RJ45-Netzwerkbuchse nicht berührt.**

Der Umbau ist abgeschlossen, wenn das Display (sofern vorhanden) wieder montiert und das modifizierte Kabel des Maussensors auf den Steckpin (J11) des Erweiterungsmoduls gesteckt ist.

![Image: 'extensionboard_07.jpg'](../images/extensionboard/extensionboard_07.jpg)


### Konfiguration des WiPort-Moduls

**Hinweis:** Bei den WLAN-Einstellungen des WiPort-Moduls ist Vorsicht geboten, da man sich ansonsten auch leicht selbst aus dem Netzwerk und seiner Konfiguration aussperren kann.

Die Netzwerk-Konfigurationsseite sieht wie folgt aus:

![Image: 'wiport_01.jpg'](../images/extensionboard/wiport_01.jpg)

Der WiPort unterstützt sowohl statische IP-Adressen als auch DHCP:

![Image: 'wiport_02.jpg'](../images/extensionboard/wiport_02.jpg)

Damit der c't-Bot von sich aus eine Verbindung zum Sim aufnimmt, muss man den Verbindungsmodus "Active Connection" auswählen und aktivieren:

![Image: 'wiport_03.jpg'](../images/extensionboard/wiport_03.jpg)

Zudem bietet der WiPort die Möglichkeit bei einer eingehenden Verbindung alte Daten zu verwerfen ("Flush Mode"):

![Image: 'wiport_04.jpg'](../images/extensionboard/wiport_04.jpg)

Diese Einstellung verhindert, dass der Bootloader Daten sieht, die der Bot vor dem Reset in den Puffer gelegt hat.

Für den Fall, dass man sich auf dem LAN- oder WLAN-Interface des WiPorts ausgesperrt hat, verbleibt der Zugang über eine serielle Verbindung als einzige Möglichkeit um das Modul zurückzusetzen.

Hierzu wird der USB-2-Bot-Adapter und ein Terminalprogramm benötigt:

![Image: 'wiport_05.jpg'](../images/extensionboard/wiport_05.jpg)

Notwendig sind hierfür die folgenden Terminal-Einstellungen:
* Baudrate: 9600
* Parity & Stop-Bits: 8N1
* Flow-Control: none

Mit dieser Konfiguration startet der WiPort ein textbasiertes Setup-Menü, wenn das Modul während des Boot-Vorgangs unmittelbar nach dem Einschalten drei "x"-Zeichen empfängt.

Das vollständige Benutzerhandbuch für den WiPort kann als [PDF-Datei](http://www.lantronix.com/wp-content/uploads/pdf/WiPort_UG.pdf) vom Hersteller Lantronix bezogen werden. _(externer Link)_


# Transportfach-Erweiterung für den c't-Bot

## Aufbau und Montage der Transportfach-Erweiterung

Wer den c't-Bot schon aufgebaut hat, muss für die Integration der Transportfach-Erweiterung zuerst das Display abschrauben und entfernen.
Die Bolzen für das Display bleiben dabei stehen.
Nun zieht man die drei 10-poligen Stecker von der Hauptplatine ab und löst die drei Befestigungsschrauben von derselben.
Als Nächstes ist der dreipolige Stecker am rechten Distanzsensor (GP2D12) abzuziehen.

Da die Transportfach-Klappe mit diesem Stecker und seiner zugehörigen Buchse am Sensor kollidieren würde, müssen beide Teile entfernt werden.
Hierfür lötet man die Steckerbuchse am Distanzsensor aus und knipst den Stecker am dreipoligen Sensorkabel ab.
Die drei Kabel sind stattdessen direkt einzulöten:

![Image: 'compartment_door_01.jpg'](../images/compartment_door/compartment_door_01.jpg)


## Servo-Motor

### Variante 1: Servo Futaba S3107

Den Servo, der später die Transportfachklappe bewegen wird, steckt man kopfüber von oben in die zentrale rechteckige Aussparung der Hauptplatine
und schraubt ihn mit zwei Schrauben (M3x8) unter Verwendung der Gummilager aus dem mitgelieferten Servozubehör fest.
Die Achse des Servos zeigt dabei in Richtung des U-förmigen Ausschnitt für das Transportfach.
Zu Beachten ist auch die Orientierung des Steckers auf der hierfür vorgesehen Pinleiste J1.
Hier muss Pin 1 (rotes Kabel) zur U-förmigen Aussparung für das Transportfach zeigen.

![Image: 'compartment_door_02.jpg'](../images/compartment_door/compartment_door_02.jpg)

Vom Servozubehör braucht man nur den runden Betätiger, die kleine Befestigungsschraube und die beiden Gummilager.
Voriger wird mit zwei Schrauben und zwei Muttern mit dem Tragarm verschraubt.

![Image: 'compartment_door_03.jpg'](../images/compartment_door/compartment_door_03.jpg)


### Variante 2: Servo Tower Pro SG90

Alternativ zu obigem Servo-Motor kann auch das Modell SG90 von Tower Pro verwendet werden.
An diesem Servo-Aktor sind für den Einbau allerdings einige Anpassungen erforderlich.
Es folgt ein Beispiel für einen Futaba-kompatiblen Einbau des SG90-Servos und die zugehörige Montage des Tragarms:

Hierbei wird der Tragarm auf der Servo-Halterung liegend eingebaut, damit er am Ende nicht zu tief sitzt und die Transportfachklappe gut an der Außengeometrie entlang gleitet.
Entsprechend ist das Loch des Tragarms leicht aufzubohren, damit die Halterung des Servos in das Loch des Tragarms passt.

![Image: 'servo_SG90_mod_01.jpg'](../images/compartment_door/servo_SG90_mod_01.jpg)

Auch die Löcher für die Befestigung des Servos sind für die Verschraubung auf der Hauptplatine aufzuweiten.

| ![Image: 'servo_SG90_mod_02.jpg'](../images/compartment_door/servo_SG90_mod_02.jpg) | ![Image: 'servo_SG90_mod_03.jpg'](../images/compartment_door/servo_SG90_mod_03.jpg) |
| ---                                                                                 | ---                                                                                 |

![Image: 'servo_SG90_mod_04.jpg'](../images/compartment_door/servo_SG90_mod_04.jpg)

In den weißen runden Kronen-Aufsatz des Servozubehörs bohrt man mit dem 2mm-Bohrer aus dem Bausatz zwei Löcher, wobei der Tragarm als Schablone dient.

Anschließend werden Klappenarm und Betätiger mit zwei M2x6-Schrauben und den zugehörigen Muttern verschraubt; so wie es in den nachfolgenden Bildern aus unterschiedlichen Perspektiven gezeigt ist.

| ![Image: 'servo_SG90_mod_05.jpg'](../images/compartment_door/servo_SG90_mod_05.jpg) | ![Image: 'servo_SG90_mod_06.jpg'](../images/compartment_door/servo_SG90_mod_06.jpg) | ![Image: 'servo_SG90_mod_07.jpg'](../images/compartment_door/servo_SG90_mod_07.jpg) |
| ---                                                                                 | ---                                                                                 | ---                                                                                 |

Aufgrund der Symmetrie des Klappenarms spielt die Orientierung hierbei keine Rolle.

Im nächsten Schritt erfolgt die Montage des Klappenarms auf der Getriebe-Krone des eingebauten Servos:

![Image: 'servo_SG90_mod_08.jpg'](../images/compartment_door/servo_SG90_mod_08.jpg)

Zu beachten ist hier, dass der Servo in den obigen Bilder noch nicht hochgesetzt worden ist so wie es im nachfolgenden Bild zu sehen ist:

![Image: 'servo_SG90_mod_09.jpg'](../images/compartment_door/servo_SG90_mod_09.jpg)

Falls der Klappen-Sensor Probleme haben sollte den Tragarm zu erkennen, kann die Höhe des Tragarms an der Halterung des SG90 unter Verwendung von Kunststoff-Muttern nachjustiert werden.

**Hinweis:** Die Pin-Belegung des SG90-Steckers entspricht _nicht_ der Pinbelegung von J1 auf der Hauptplatine, was eine _Korrektur des Pinouts erforderlich_ macht.
Hier müssen die Kabel im Stecker so vertauscht werden, sodass sich die untenstehende Belegung ergibt.
Am Besten eignet sich hierfür eine Stecknadel, mit der sich die kleinen Kunststoff-Widerhaken des Steckers entriegeln lassen.
Die neue Stecker-Belegung lautet:

| Pin | Kabelfarbe | Funktion |
| --- | ---        | ---      |
|   1 |        rot |      VCC |
|   2 |      braun |      GND |
|   3 |     orange |      PWM |

| ![Image: 'servo_pinout_orig.jpg'](../images/compartment_door/servo_pinout_orig.jpg) | ![Image: 'servo_pinout_new.jpg'](../images/compartment_door/servo_pinout_new.jpg)         |
| ---                                                                                 | ---                                                                                       |
| Originale Steckerbelegung des SG90-Servomotors                                      | Erforderliche Steckerbelegung für den c't-Bot (typische Belegung für Futaba-Servomotoren) |


## Einbau des Tragarms und Verlöten von Tragarm und Klappe

Nun ist es an der Zeit die Sensorkabel der rechten Sensorplatine durch den Klappenarm zu fädeln und den Klappenarm lose auf den Servo zu stecken.
Bevor dieser jedoch festschraubt wird, legt man die Hauptplatine auf und prüft den Schwenkbereich.
Eventuell ist der Klappenarm nochmal vom Servo ab- und in einem anderen Winkel aufzustecken um den Aktionsradius zu optimeren.
Der Tragarm sollte dabei so auf der Servoachse sitzen, dass er in in geöffneter Stellung von innen an die rechte vordere Stütze des Bots
und bei geschlossener Klappe von außen an die einzelne hintere Stütze anschlägt.
In geschlossener Position steht der Tragarm genau unterhalb des Klappensensors auf der Unterseite der Hauptplatine.
Sobald diese optimale Position gefunden ist, mit der die Klappe alle vorgesehenen Positionen erreichen kann, sollte der Betätiger mit der Krone des Servomotors verschraubt werden.

![Image: 'compartment_door_06.jpg'](../images/compartment_door/compartment_door_06.jpg)

Da sowohl der Tragarm als auch die Klappe mit Kupfer beschichtet sind, lassen sich beide Teile einfach miteinander verlöten.
Dazu bietet es sich an zuerst das rechteckige Stück Metallblech für die Transportklappe in die richtige Form zu biegen.
Nun dreht man den Tragarm in die geschlossene Stellung (gegen den Uhrzeigersinn bis auf Anschlag) und fixiert dann die Klappe mit zwei kleinen Lötpunkten.
Letztere sollte dabei weder einen der beiden Abstandssensoren abdecken noch auf der Grundplatte aufstehen.
Für den Fall, dass die Klappe in geöffnetem Zustand den rechten Sensor blockiert, muss sie nochmals verschoben werden.
Steht die optimale Position fest, verbinden zwei dicke Zinnspuren die Klappe oben und unten mit dem Tragarm.

| ![Image: 'compartment_door_04.jpg'](../images/compartment_door/compartment_door_04.jpg) | ![Image: 'compartment_door_05.jpg'](../images/compartment_door/compartment_door_05.jpg) |
| ---                                                                                     | ---                                                                                     |

Wer beide Teile nur mit Handschuhen anfasst und diese nach dem Löten reinigt und mit einer dünnen Schicht Klarlack besprüht, erhält deren Glanz dauerhaft.

Zum Abschluss schraubt man noch je zwei Abstandsbolzen (3x12) ineinander und erhält dadurch drei lange Bolzen mit denen man die Hauptplatine wieder auf den Stützen des Roboters festschraubt.


# Sonstiges optionales Zubehör

* [LCD-Display](ct-bot_display.md)
* [USB-UART-Adapter](usb-2-bot.md)
* für den Batteriebetrieb: 5x AA-Mignon-Akkus (Typ: IEC HR6; empfohlene Kapazität: ≥ 2400 mAh)
* Infrarot-Fernbedienung: Universal-Fernbedienung "RC_Univers_29"

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Benjamin Benz, Peter Recktenwald, anonybot, Nightwalker-87
