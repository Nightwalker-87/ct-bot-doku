**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Software des c't-Bot

>> **Trac-2-Markdown Konvertierung:** *unchecked*

Diese Seite befasst sich mit der Software des c't-Bots. Für die meisten Punkte gilt: Es gibt keinen Unterschied zwischen simulierten und realen Bots. Dennoch richten sich ein paar Absätze hauptsächlich an Besitzer realer Bots

## Schnelleinstieg

Einen ersten Eindruck vom Projekt vermitteln die **[ersten Schritte](../Firststeps/Firststeps.md)**, **[allgemeine Infos und Anlaufstellen](../WikiStart/WikiStart.md#Anlaufstellen)** sind auf der Hauptseite verlinkt

## Vorraussetzungen

Soll es mit dem eigenen Code richtig losgehen, sind erst einmal ein paar Vorraussetzungen zu schaffen.

1. Bitte einmal die [Installationsanleitung](../InstallationsanleitungR23/InstallationsanleitungR23.md) durchgehen
1. Code aus dem Repositiory [holen](../GITUndEclipse/GITUndEclipse.md). Nun braucht man entweder einen [realen Bot](../ct-Bot-Hardware/ct-Bot-Hardware.md) oder einen laufenden [Simulator](../ct-Sim/ct-Sim.md).

## Erste Geh- und Modifikationsversuche mit der Demo-Firmware

Damit die hier beschriebenen Schritte Sinn ergeben, sollte man entweder einen **[realen Bot](../ct-Bot-Hardware/ct-Bot-Hardware.md)** **[aufgebaut](../ct-Bot-Hardware/ct-Bot-Hardware.md#Aufbau-und-Montage) und [erfolgreich getestet](../ct-Bot-Hardware/ct-Bot-Hardware.md#Test-eines-frisch-aufgebauten-ct-Bots)** haben. Solange die beschriebenen Testprogramme nicht einwandfrei laufen, handelt man sich mit unten beschriebenen Gehversuchen nur Ärger und Frust ein. Auch die empfohlenen **[Hardware-Mods](../ct-Bot-Modifikationen/ct-Bot-Modifikationen.md)** sollten eingebaut sein.
**Bitte beachten:** Die auf dem Display angezeigten absoluten Sensorwerte sind nicht korrekt, solange die Kalibrierung noch nicht durchgeführt wurde! Gleiches gilt für den Gleichlauf der Motoren.

Alle erwähnten Code-Optionen finden sich in *[ct-Bot.h](https://github.com/tsandmann/ct-bot/blob/master/ct-Bot.h)*. Siehe auch: [Übersicht der optionalen Codeteile](../../doc/wiki_pages/ct-bot_h.md)

Nach jeder Änderung am Code muss dieser übersetzt (ct-Bot.hex) und auf den Bot **[übertragen](../Flash/Flash.md)** werden. Zusätzlich muss auch das EEPROM-Abbild dort hin.

### Kalibrierung

Damit der Demo-Code korrekt arbeitet sind ein paar Anpassungen an den eigenen Bot und dessen Umgebung nötig:

1. Wenn noch nicht geschehen: Die Fernbedienung (falls das Modell *HQ RC Univers 29* verwendet wird) auf den Gerätecode **TV 334** (siehe beiliegende Anleitung) programmieren. Wer diese Fernbedienung mit vierstelligen Gerätecodes (siehe Anleitung) besitzt, sollte unseren [Support](../FirstSteps/FirstSteps.md#Support) kontaktieren - der Gerätecode 334 funktioniert hier nicht.
1. **[Abgrundsensoren](../ct-Bot-Software-Sensoren/ct-Bot-Software-Sensoren.md#Abgrundsensoren)** kalibrieren
1. Bei Bedarf **[Liniensensoren](../ct-Bot-Software-Sensoren/ct-Bot-Software-Sensoren.md#Liniensensoren)** kalibrieren
1. **[Distanzsensoren](../ct-Bot-Software-Sensoren/ct-Bot-Software-Sensoren.md#Distanzsensoren)** kalibrieren
1. Bei Bedarf: **[Maussensor tunen](../ct-Bot-Software-Sensoren/ct-Bot-Software-Sensoren.md#Maussensor)**
1. **[Motorregelung](../ct-Bot-Software-Aktuatoren/ct-Bot-Software-Aktuatoren.md#Motoren)** kalibrieren

### Und los geht es

Nun sind alle Sensoren kalibriert und man kann mit den Verhalten im Beispielcode spielen:

1. gewünschte Code-Optionen in *[ct-Bot.h](https://github.com/tsandmann/ct-bot/blob/master/ct-Bot.h)* ein- oder ausschalten: [Übersicht der optionalen Codeteile](../../doc/wiki_pages/ct-bot_h.md)
1. gewünschte Verhalten in *[include/bot-logic/available_behaviours.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-logic/available_behaviours.h)* auswählen: [Übersicht der verfügbaren Verhalten](../Verhalten/Verhalten.md)

### Erweiterungsmodul

Wenn das Erweiterungsmodul vorhanden ist:

1. MMC / SD-Karten Unterstützung aktivieren: im Bot-Code *[ct-Bot.h](https://github.com/tsandmann/ct-bot/blob/master/ct-Bot.h)* die Zeile `//#define MMC_AVAILABLE` einkommentieren. Danach prüfen, ob unter *[ui/available_screens.h](https://github.com/tsandmann/ct-bot/blob/master/ui/available_screens.h)* `#define DISPLAY_MMC_INFO` aktiviert ist und anschließend den Bot-Code neu kompilieren. Nach dem Flashen des Bots sollte die Bot-Display-Seite für die MMC-Display-Seite anzeigen, ob die Speicherkarte erkannt wird, andernfalls meldet die MMC-Display-Seite den Fehler `MMC not init (x)`, wobei `x` den Fehlercode darstellt.
1. Die SD-Karte mit FAT16 oder FAT32 formatieren.
    * Hinweise:
      * Die Abkürzung *MMC* wird im ct-Bot Kontext generell für *SD- oder Multimedia-Card* verwendet und meint explizit **nicht** [Multimedia Card](https://de.wikipedia.org/wiki/Multimedia_Card)-spezifische Dinge. Genau genommen hat das Erweiterungsmodul des ct-Bots einen [SD-Karten](https://de.wikipedia.org/wiki/SD-Karte)-Steckplatz, der abwärtskompatibel zu Multimedia Cards ist.
      * Die Fehlermeldung `MMC/SD not init (1)` ermöglicht keine Unterscheidung darüber, ob nur die SD-Karte nicht erkannt wird, oder aber auch die Erweiterungsplatine selbst nicht erkannt wird. Andere Fehlercodes als 1 deuten auf ein Problem mit der Erkennung der SD-Karte hin.
      * Die Optionen `MAP_AVAILABLE` sollte für den ersten Test **aus** sein.
      * Mögliche Fehlercodes (Stand: Release 25):
        * `1`: Die Karte antwortet nicht. Das kann auch bedeutet, dass gar keine Karte eingesteckt ist, die Verbindung unterbrochen ist oder ein anderer (elektrischer) Fehler auf dem Erweiterungsboard vorliegt.
        * `2`: Die Karte hat zwar geantwortet, die anschließende Initialisierung schlug aber fehl. Evtl. ist die Karte defekt oder inkompatibel.
      * Seit Release 25 werden auch (micro) SDHC und SDXC Karten unterstützt. Außerdem wird ein FAT16 und FAT32 Dateisystem unterstützt (das ehemalige `BOT_FS_AVAILABLE` wurde hier durch `SDFAT_AVAILABLE` ersetzt). SDXC Karten müssen auf jeden Fall mit FAT32 formatiert sein, exFAT wird nicht unterstützt. Karten > 64GB sind bisher ungetestet.

### Eigene Schritte

Wenn die Beispielverhalten funktionieren, kann man beginnen, eigene zu programmieren.

1. c't-Artikel: [Programmierung](https://www.heise.de/ct/artikel/Hohe-Schule-290392.html) des (virtuellen) c't-Bot
1. c't-Artikel: [Tutorial](https://www.heise.de/ct/artikel/Ausgang-gesucht-290460.html) für die Programmierung des c't-Bot
1. c't-Artikel: [Eigene Welten](https://www.heise.de/ct/artikel/Genesis-290480.html) für den c't-Sim
1. c't-Artikel: [Kartographie](https://www.heise.de/ct/artikel/An-der-naechsten-Ecke-links-290662.html) für den c't-Bot
1. [FAQ-Einträge](https://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html)

## Dokumentation

* Übersicht und Beschreibung der konfigurierbaren [Optionen](../../doc/wiki_pages/ct-bot_h.md) des Bot-Codes
* Übersicht der im Code verfügbaren [Roboterverhalten](../Verhalten/Verhalten.md)
* Funktionsweise und Kalibrierung der [Sensoren](../ct-Bot-Software-Sensoren/ct-Bot-Software-Sensoren.md) des c't-Bot
* Funktionsweise und Kalibrierung der [Aktuatoren](../ct-Bot-Software-Aktuatoren/ct-Bot-Software-Aktuatoren.md) des c't-Bot
* Dokumentation der [Remote-Calls](../RemoteCall/RemoteCall.md)
* Dokumentation zum [ct-Bot-Protokoll](../DokuProtocol/DokuProtocol.md)
* Dokumentation zur [Bot-2-Bot-Kommunikation](../DokuBot2Bot/DokuBot2Bot.md)
* Dokumentation zum [c't-Bot-Betriebssystem](../DokuOS/DokuOS.md)
* Dokumentation zum Verhalten [bot_line_shortest_way](../DokuLineShortestWay/DokuLineShortestWay.md)
* Dokumentation zum [Pfadplanungsverhalten](../DokuPathplaning/DokuPathplaning.md)
* Dokumentation zum Verhalten [bot_drive_area](../DokuDriveArea/DokuDriveArea.md)
* Dokumentation zur [Lokalisierung](../Localization/Localization.md)
* Dokumentation zur [Programmierung des c't-Bots in weiteren Programmiersprachen](../DokuScriptLanguages/DokuScriptLanguages.md)
* Dokumentation zum [Neuronalen Netz für den c't-Bot](../DokuNeuralnet/dok_bot_nn.htm)

### Deprecated Doku

* Alte [Installationsanleitung](../deprecated/Installationsanleitung/Installationsanleitung.md) vor Release 23
* Dokumentation zum [SD-Karten Dateisystem BotFS](../deprecated/DokuBotFs/DokuBotFs.md)
* Dokumentation zur [Virtuellen Speicherverwaltung](../deprecated/DokuMmcVm/DokuMmcVm.md) für SD-Karten
* Dokumentation zur [EEPROM-Emulation](../deprecated/DokuEepromEmu/DokuEepromEmu.md) für simulierte Bots

## Howto

* [Firmware](../Flash/Flash.md) auf den c't-Bot übertragen
* [Protokollieren](../../doc/wiki_pages/logging.md) von Messdaten vom c't-Bot aus
* [Hintergründe](../AVRToolchainInterna/AVRToolchainInterna.md) zur AVR-Toolchain
* [AVR-Tools und Tricks](../AVRToolchain/AVRToolchain.md#Nützliche Tools für AVR) für die (Bot-)Softwareentwicklung

## Ideen und mehr

* [Ideen und Diskussionen](../NeueVerhalten/NeueVerhalten.md) für neue Verhalten und Aufgaben
