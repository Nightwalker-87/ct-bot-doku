# Übersicht der in `ct-Bot.h` aktivierbaren Optionen

Verfügbare Optionen lassen sich jeweils per #define ein- oder ausschalten. Das Dektivieren der jeweiligen Funktion erfolgt durch die Kommentarzeichen // am Anfang der Zeile.
Ausgeschaltete Optionen belegen keinen Platz im Flash-Speicher des Controllers.

**Achtung:** Das Ein- und Ausschalten von Funktionen aufgrund von internen Abhängigkeiten auch andere Optionen indirekt ein- und/oder ausschalten.

So bewirkt `MEASURE_MOUSE_AVAILABLE` beispielsweise, dass der Bot seine Positionsdaten mit Hilfe des Maussensors berechnet.
Schaltet man diese Funktion **aus**, sind weiterhin weiterhin Positionsdaten verfügbar, welche dann aber mit den Sensorwerten der Radencoder berechnet werden.

Im Folgenden sind alle in der Header-Datei _ct-Bot.h_ verfügbaren Optionen aufgelistet:

## Logging-Funktionen

Folgenden Optionen steuern ob und wenn ja, welche Log-Methode vorhanden ist (hierbei kann jeweils nur eine Log-Methode aktiv sein):

* `LOG_CTSIM_AVAILABLE`: Logging zum ct-Sim (PC und MCU)
* `LOG_DISPLAY_AVAILABLE`: Logging über das LCD-Display (PC und MCU)
* `LOG_MMC_AVAILABLE`: Logging in eine txt-Datei auf der MMC inkl. Displayausgabe mit Scrollfunktion
* `LOG_STDOUT_AVAILABLE`: Logging auf die Konsole (nur für PC)
* `LOG_UART_AVAILABLE`: Logging über UART (nur für MCU)
* `CREATE_TRACEFILE_AVAILABLE`: Aktiviert das Schreiben einer Trace-Datei (nur PC)
* `USE_MINILOG`: Schaltet auf vereinfachtes Logging um was Flash-Speicher und RAM spart, dafür aber z.B. nicht den Dateinamen der Quellcode-Datei mit ausgibt - gemäß dem Prinzip "manchmal ist weniger mehr".

## Kommunikation

* `BOT_2_BOT_AVAILABLE`: Ermöglicht den Datenaustausch zwischen mehreren Bots und schaltet die Auswertung von Nachrichten anderer Bots ein. ([Dokumentation](../../_tmp_trac_wiki_export/DokuBot2Bot/DokuBot2Bot.md))
* `BOT_2_BOT_PAYLOAD_AVAILABLE`: Aktiviert die Möglichkeit Payloaddaten zwischen zwei Bots auszutauschen. ([Dokumentation](../../_tmp_trac_wiki_export/DokuBot2Bot/DokuBot2Bot.md#Übertragen-weiterer-Daten-als-Payload))
* `BOT_2_SIM_AVAILABLE`: Aktiviert die Kommunikation des realen Bots mit dem Sim, d.h. der Bot sendet seine Sensorwerte an den Simulator, wo sie angezeigt werden.
    * **Abhängigkeiten:** Das Einschalten dieser Option aktiviert die serielle Schnittstelle der MCU (`UART_AVAILABLE`), über die die Daten entweder per USB-2-Bot-Adapter oder per LAN / WLAN (wenn das Erweiterungsmodul vorhanden ist) an den Sim gesendet werden.
Natürlich ist diese Option nur für den realen Bot interessant, der Simulierte muss schließlich immer Daten mit dem Sim austauschen.

## Display-Funktionen

* `DISPLAY_AVAILABLE`: Aktiviert das Display.
* `DISPLAY_REMOTE_AVAILABLE`: Aktiviert neben der Übertragung der Sensorwerte an den Sim auch die Übertragung des Display-Inhalts, sodass dieser im Sim erscheint.
    * **Abhängigkeiten:** Diese Option benötigt `BOT_2_SIM_AVAILABLE`
* `KEYPAD_AVAILABLE`: Aktiviert die Möglichkeit mit der Fernbedienung Zeichen eingeben zu können (Handy- bzw. Telefontastatur).
* `WELCOME_AVAILABLE`: Anzeige eines kleinen Willkommensgrußes auf dem Display.

## Sensorauswertung

* `MEASURE_COUPLED_AVAILABLE`: Positions- und Geschwindigkeitsdaten werden aus Maussensor- und Radencoder-Werten ermittelt und gekoppelt.
Die Gewichtung lässt sich hierbei in [include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h) einstellen).
* `MEASURE_MOUSE_AVAILABLE`: Aktiviert die Positions- und Geschwindigkeitsberechnung aus den Maussensordaten.
Somit verwenden die Verhalten die Positions- und Geschwindigkeitsdaten des Maussensors anstelle der aus den Radencoder-Werten berechneten Positions- und Geschwindigkeitsdaten.
Das Deaktivieren dieser Option schaltet folglich wieder auf die Positionsbestimmung per Radencoder um.
* `MEASURE_POSITION_ERRORS_AVAILABLE`: Fehlerberechnungen bei der Positionsbestimmung
* `MOUSE_AVAILABLE`: Aktiviert den Code für die Auswertung des Maussensors.
    * **Abhängigkeiten:** Das Ausschalten dieser Option deaktiviert gleichzeitig `MEASURE_MOUSE_AVAILABLE` und `MEASURE_COUPLED_AVAILABLE`.
* `BPS_AVAILABLE`: Aktiviert die Auswertung des Sensors zur Lokalisierung (IR-Landmarken).
    * **Abhängigkeiten:** Sofern das Erweiterungsboard installiert ist und `EXPANSION_BOARD_AVAILABLE` in [include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h) gesetzt ist, wird der linke Helligkeitssensor (*LDRL*) automatisch deaktiviert. ([Dokumentation](../../_tmp_trac_wiki_export/Localization/Localization.md))
* `CMPS03_AVAILABLE`: Aktiviert die Auswertung des Kompassmoduls CMPS03. ([Dokumentation](../../_tmp_trac_wiki_export/HWErweiterungen/HWErweiterungen.md#CMPS03-Kompass))
* `SRF10_AVAILABLE`: Aktiviert den Code für den Ultraschallsensor SRF10.

## Motoransteuerung

* `ADJUST_PID_PARAMS`: Aktiviert die Einstellung der PID-Parameter für die Motorregelung zur Laufzeit per Fernbedienung.
Das ist zum manuellen Kalibrieren der Regelung einmalig nötig und sollte danach wieder ausgeschaltet werden, da diese Funktion ansonsten unnötig Rechenzeit beansprucht.
* `SPEED_CONTROL_AVAILABLE`: Aktiviert die Motorregelung. Damit diese Regelung zuverlässig funktioniert, muss sie zuvor einmalig kalibriert werden.
Mit Motorregelung kann der Bot die gewünschte Fahrtgeschwindigkeit auch genau einhalten, was zu einem guten Fahrverhalten sowie exakten Drehungen und Positionierungen führt.
Außerdem werden die Motoren in diesem Modus schonender betrieben. ([Dokumentation](../../_tmp_trac_wiki_export/ct-Bot-Software-Aktuatoren/ct-Bot-Software-Aktuatoren.md))
* `SPEED_LOG_AVAILABLE`: Zeichnet Debug-Infos der Motorregelung auf einer MMC (sofern vorhanden) auf, ist jedoch nur in Ausnahmefällen nötig. ([Dokumentation](../../_tmp_trac_wiki_export/ct-Bot-Software-Aktuatoren/ct-Bot-Software-Aktuatoren.md#Die-Logging-Funktion))

## Umgebungskarte

* `MAP_AVAILABLE`: Aktiviert die Kartographie. Die Karte kann auf zwei verschiedene Arten abgelegt werden:
    1. Auf dem realen Bot kann die Karte entweder auf der MMC (wenn `MMC_AVAILABLE` aktiv ist) oder im SRAM der MCU. Auf Grund des beschränkten Speichers macht in der Praxis allerdings nur eine Ablage der Daten auf der MMC Sinn.
    2. Beim simulierten Bot am PC kann die Karte entweder im RAM des PCs oder auf einer emulierten MMC gespeichert werden Bei letzterem handelt es sich um eine Datei auf der Festplatte, die auch beim Neustart des Bots erhalten bleibt.
* `MAP_2_SIM_AVAILABLE`: Sendet für simulierte und für echte c't-Bots die Map-Aktualisierungen sowie die aktuelle Bot-Position fortlaufend zur Anzeige an den Simulator.

## MMC / SD-Karte als Speichererweiterung (Erweiterungsmodul)

* `MMC_AVAILABLE`: Aktiviert die Treiber für eine MMC/SD-Karte, die dann z.B. von `MAP_AVAILABLE` verwendet werden kann.
* `BOT_FS_AVAILABLE`: Aktiviert das Dateisystem BotFS. ([Dokumentation](../../_tmp_trac_wiki_export/deprecated/DokuBotFs/DokuBotFs.md))
    * **Abhängigkeiten:** Diese Option wird für _uBasic_ (`BEHAVIOUR_UBASIC_AVAILABLE`) in [include/available_behaviours.h](https://github.com/tsandmann/ct-bot/blob/master/include/available_behaviours.h) benötigt
    und außerdem vom _Map-Code_ (`MAP_AVAILABLE`), sowie auch beim _Logging auf SD-Karte_ (`LOG_MMC_AVAILABLE`) verwendet.
> `MMC_VM_AVAILABLE` _(deprecated)_: Aktiviert das Virtual Memory Management mit MMC/SD-Karte oder PC-Emulation.
Damit kümmert sich der Bot selbst um das Ein- und Auslagern von Speicherseiten, die auf der MMC liegen und stellt somit einen einfach zu benutzenden und großen Speicherraum zur Verfügung.
Ebenso wird das Lesen und Schreiben von Dateien auf der MMC durch Caching optimiert.
Diese Funktion benötigt allerdings relativ viel RAM für den Cache und Flash-Speicher. Daher wird als Hardware mindestens ein ATMega644(P) empfohlen.
Beim simulierten Bot schaltet diese Option die emulierte MMC ein, welche die Daten für die Verhalten, die der Bot auf der MMC speichert, völlig transparent in eine Datei umleitet. _Diese Funktion wurde in Commit tsandmann/ct-bot@b1043b54aff0f8322014a9d1f6c5dc7cb93216b4 entfernt._

## Hardware-Treiber

* `ADC_AVAILABLE`: Aktiviert den Treiber für den A/D-Konverter.
* `ENA_AVAILABLE`: Aktiviert den Treiber für die Enable-Leitungen.
* `IR_AVAILABLE`: Aktiviert den Treiber für die Infrarot-Fernbedienung.
* `LED_AVAILABLE`: Aktiviert den Treiber für die LEDs.
* `RC5_AVAILABLE`: Aktiviert Key-Mapping für die Infrarot-Fernbedienung.
* `SHIFT_AVAILABLE`: Aktiviert den Treiber für die Shift Register.
* `SP03_AVAILABLE`: Aktiviert die Unterstützung für das Sprachausgabemodul SP03. ([Dokumentation](../../_tmp_trac_wiki_export/HWErweiterungen/HWErweiterungen.md#Sprachmodul-SP03))

## Sonstiges

* `BEHAVIOUR_AVAILABLE`: Aktiviert das Verhaltenssystem.
* `BOOTLOADER_AVAILABLE`: Aktiviert den Code für die einmalige Installation des Bootloaders. Ist der Bootloader einmal installiert, muss diese Option anschließend wieder auskommentiert werden. ([Dokumentation](../../_tmp_trac_wiki_export/Flash/Flash.md#Bootloader-des-ct-Bot))
* `ARM_LINUX_BOARD`: Code für das ARM-Linux-Board aktivieren, wenn beim Kompilieren des Codes das _ARM-Linux-RPi3_ Target ausgewaehlt wurde. Das ARM-Linux-Board führt den High-Level-Code und die Verhalten aus. ([Dokumentation](../../_tmp_trac_wiki_export/RaspberryPi/RaspberryPi.md))
* `BOT_2_RPI_AVAILABLE`: Kommunikation des ATmega Mikrocontrollers mit einem Linux-Board (z.B. Raspberry Pi) aktivieren. Diese Option führt auf dem ATmega den Low-Level-Code aus. ([Dokumentation](../../_tmp_trac_wiki_export/RaspberryPi/RaspberryPi.md))
* `OS_AVAILABLE`: Aktiviert ein Mini-Betriebssystem mit Threads und Scheduling. ([Dokumentation](../../_tmp_trac_wiki_export/DokuOS/DokuOS.md), sowie weitere Details in [mcu/os_thread.c](https://github.com/tsandmann/ct-bot/blob/master/mcu/os_thread.c))
* `POS_STORE_AVAILABLE`: Stellt einen globalen Speicher für Positionsdaten bereit, der von Verhalten benutzt werden kann. Die möglichen Policies sind FIFO und LIFO (Stack).

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Timo Sandmann, Nightwalker-87
