**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# CPU-Erweiterung für den c't-Bot mit einem Raspberry Pi

## Einleitung

Die Standard-Hardware des c't-Bots lässt sich mit dem umfangreichen Software-Framework inzwischen nahezu vollständig ausreizen. Um weitere Features implementieren zu können, entstand deshalb die Idee, den c't-Bot um eine CPU-Erweiterung zu ergänzen, die (für das BeagleBoard auch im c't Sonderheft [c't Hardware Hacks](https://shop.heise.de/katalog/ct-hardware-hacks-1-2012) vorgestellt wird.

Diese Wiki-Seite soll einen Einblick in die neuen Möglichkeiten bieten und grundlegende Informationen liefern, wie sich ein c't-Bot mit einem Raspberry Pi erweitern lässt und welche Anpassungen an Hard- und Software dafür nötig sind.
Achtung, die Anleitung enthält keine einsteigerfreundlichen und vollständigen Schritt-für-Schritt-Anleitungen, da die CPU-Erweiterung den Bastel-Aspekt des c't-Bot Projekts in den Vordergrund stellt und aktuell keine abgeschlossene Baugruppe oder fertige Software umfasst. Vielmehr geht es darum, Ideen und Lösungsansätze zusammenzutragen, um die Erweiterung auf diese Weise auszubauen und zu optimieren.

## Idee

* Zusätzlich zur c't-Bot Hauptplatine ein Raspberry Pi (RPi) montieren (anstelle der offiziellen WLAN- / MMC-Erweiterung).
* ATmega des Bots führt low-level Code aus und kommuniziert mit RPi über eine serielle Schnittstelle (UART, SPI).
* RPi führt eine Linux-Distribution aus und ermöglicht so SSH Login und Filetransfer auf dem / zum Bot, Ausführen beliebiger Linux-Software, usw.
* RPi bietet weitere Schnittstellen (USB, LAN, I2C, Audio, GPIOs) für zusätzliche Hardware (WLAN USB-Stick, weitere Sensoren, Kamera, ...).
* Funktionalität des WiPorts wird mit on-board WLAN oder einem einfachen WLAN USB-Stick und socat bereitgestellt.
* RPi GPIO-Pin steuert auch Reset-Leitung des ATmegas.
* Erweiterung des c't-Bots um eine Kamera, die über dem Kamera-Port des RPis angeschlossen wird.

## Voraussetzungen

* Bastelinteresse in Hard- und Software.
* c't-Bot (oder kompatiblen Roboter / ähnliche Hardware).
* Cross-Toolchain nach ARM-Linux: verfügbar für Linux (getestet unter Fedora 23, auf anderen Distributionen vermutlich auch möglich), Mac OS X und Windows (mit Linaro Toolchain). Damit lässt sich der Bot-Code für ARM-Linux übersetzen.
* c't-Bot [Toolchain](../InstallationsanleitungR23/InstallationsanleitungR23.md) installiert.

## Hardware

* Die CPU-Erweiterung für den c't-Bot umfasst nicht nur das CPU-Board, sondern auch ein notwendiges Interface-Board, das die Verbindung zur c't-Bot Hardware herstellt und insbesondere eine Konvertierung der Signal-Spannungspegel von 3.3 V (RPi) auf 5.0 V (c't-Bot Hardware) vornimmt.

### Raspberry Pi

* [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/)
  * Vorteile
    * WLAN bereits on-board, Aufpreis ggü. RPi 2 geringer als übliche WLAN-USB Sticks
    * Maximale Performanz in der Raspberry Pi Familie
  * Nachteile
    * WLAN nur für 2.4 GHz Band
    * Bluetooth nicht nutzbar, wenn UART für die Kommunikation mit dem ATmega des c't-Bots verwendet werden soll
* [Raspberry Pi 2 Model B](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/)
  * Vorteile
    * Günstiger als Version 3
  * Nachteile
    * WLAN nur über USB-Stick, typischerweise mehr Stromverbrauch, Treiber müssen vorhanden sein, etc.
    * Geringere Performanz als Version 2 (je nach Einsatzzweck ver­nach­läs­sig­bar)

### Kamera

* [Raspberry Pi Kamera](https://www.raspberrypi.org/products/camera-module-v2/)
  * Vorteile
    * Performante Anbindung über Camera-Connector
    * Treiber / Software für Raspberry Pi verfügbar
    * Verwendet GPU-Ressourcen des Raspberry Pi zur Bildverarbeitung

### Interface-Board

Das Interface-Board bindet den Raspberry Pi an die Hardware des c't-Bots an. Alternativ lässt sich auch der USB-2-Bot Adapter verwenden, um die c't-Bot Hardware mit dem Raspberry Pi zu verbinden, dann ist kein Interface-Board erforderlich.

Derzeit umfasst das Interface-Board die folgenden Subsysteme:

* Pegelanpassung 3.3 V <-> 5.0 V der **UART-Signale**
* Pegelanpassung 3.3 V <-> 5.0 V für **GPIO-Pins** (z.B. für Reset-Leitung zum ATmega)
* Pegelanpassung 3.3 V <-> 5.0 V der **SPI-Signale**
* Pegelanpassung 3.3 V <-> 5.0 V der **I2C-Signale**
* **ATmega1284P**, der den originalen Prozessor des c't-Bots (IC1 @ Schaltplan c't-Bot) ersetzt. Unterschiede:
* 20 MHz Quarz / Takt
* Hardware-SPI Patch
* Anschluss für [BPS-Sensor](../Localization/Localization.md)
* Pullup für Servo
* Pulldowns für Motoren
* SPI-Anschluss für ISP oder externen MMC / SD-Slot
* **Power-Modul** mit leistungsfähigerem Spannungswandler und Überwachung des Batterie-Ladezustands

Hinweise zur derzeitigen Interface-Board Version:

* Die Anbindung des Maus-Sensors des Bots fehlt. Der Maussensor kann aktuell also nicht verwendet werden, wenn das Interface-Board installiert ist. Der Hintergrund ist, dass der Maus-Sensor den SPI-Port des ATMegas belegen würde. Alternativ ist die Anbindung des Maussensors an einen SPI-Port des RPis denkbar, erfordert aber zusätzliche Hardware.
* Es werden fast ausschließlich SMD-Bauteile verwendet, es lässt sich prinzipiell aber auch ohne aufbauen.

### Montage

* ATmega auf der Bot-Hauptplatine entfernen.
* Interface-Board anstelle des originalen Erweiterungsmoduls montieren, längere Abstandsbolzen verwenden, Kabel auf J4 bis J8 verbinden.
* Raspberry Pi auf Interface-Board montieren, elektrische Verbindung über RPi-Extension-Header.
* Display mit zusätzlichen Abstandsbolzen oberhalb des RPis anbringen.

## Toolchain

Siehe Abschnitt *Compiler für Raspberry Pi installieren* in der [Installationsanleitung](../InstallationsanleitungR23/InstallationsanleitungR23.md).

## Software

### Betriebssystem

Auf dem Raspberry Pi wird eine Linux-Distribution ausgeführt, die auf der SD-Karte installiert ist. Die folgende Anleitung verwendet das sehr schlanke [Fedberry Mini 24](http://fedberry.org), andere Distributionen wie Raspbian oder Ubuntu sind auch möglich, werden hier aber nicht beschrieben.

#### Installation / Konfiguration

* Für die Installation siehe [https://github.com/fedberry/fedberry/blob/master/README.md](https://github.com/fedberry/fedberry/blob/master/README.md)
* Konsole auf dem Uart des RPi deaktivieren, um es für die Kommunikation mit dem ATmega verwenden zu können:
  * In cmdline.txt: `console=ttyAMA0,115200` **entfernen**
  * getty-Service deaktivieren: `systemctl mask serial-getty@ttyAMA0.service`
* Geräte aktivieren in *config.txt* (auf Bootpartition)
  * I2C aktivieren: `dtparam=i2c_arm=on` und `dtparam=i2c1=on`
  * SPI aktivieren: `dtparam=spi=on`
  * Kamera aktivieren: `start_x=1` und `gpu_mem=128`
  * Kamera LED deaktivieren: `disable_camera_led=1`
  * UART Settings für Raspberry Pi **3**: `init_uart_clock=16000000` und `dtoverlay=pi3-miniuart-bt`
* Bei Verwendung des USB2Bot-Adapters
  * I/O Latenz reduzieren: `echo 1 > /sys/bus/usb-serial/devices/ttyUSB0/latency_timer`

### Raspberry Pi als WiPort-Ersatz

Ein Raspberry Pi mit WLAN (on-board oder USB-Stick) kann als günstiger Ersatz für die WiPort-Lösung des Erweiterungsmoduls verwendet werden. Hierzu tunnelt man einfach die UART-Verbindung zum ATmega mit Hilfe des Programms *socat* über eine TCP-Verbindung:
`socat -b1 TCP-LISTEN:10002,fork,reuseaddr /dev/ttyAMA0,raw,echo=0,ospeed=115200,ispeed=115200`. Anschließend kann man (wie bei Verwendung des WiPort) den c't-Sim auf die IP-Adresse des Raspberry Pi und Port 10002 verbinden und den c't-Bot fernsteuern, überwachen, usw.

### Low-level Bot-Code für ATmega

Der ATmega1284P auf dem Interface-Board führt den Low-level Code aus und stellt somit die Schnittstelle zur c't-Bot-Hardware bereit. Der Vorteil durch die Verwendung eines zusätzlichen Mikrocontrollers neben dem RPi besteht in der Kompatibilität zum originalen c't-Bot und der Wiederverwendbarkeit sämtlicher Treiber für die Bot-Hardware. Der Low-level Code besteht aus einer leicht modifizierten Untermenge des originalen c't-Bot Codes. Verzichtet wird dabei auf sämtlichen Verhaltenscode und weitere Features wie Kartographie oder Positionsspeicher, all das übernimmt der High-level Code, den die RPi-CPU ausführt. Zusätzlich implementiert ist eine CRC16-Prüfsumme, welche die Kommunikation mit dem RPi gegen Übertragungsfehler absichert. Um den Low-level Code zu aktivieren, muss in *ct-Bot.h* der Schalter `BOT_2_RPI_AVAILABLE` aktiviert werden.

### High-level Bot-Code für ARM

Der RPi führt den für die ARM-Linux Architektur compilierten High-level Code aus und übernimmt somit die Ausführung von Verhalten, Kartographie usw.

Um den c't-Bot Code für einen Bot mit RPi-Erweiterung zu übersetzen als Build-Konfiguration in Eclipse *Debug-ARM-Linux-RPi2* oder *Debug-ARM-Linux-RPi3* wählen und den Schalter `ARM_LINUX_BOARD` in *ct-Bot.h* aktivieren.

Die wesentlichen Unterschiede zum ct-Bot-Code für ATmega oder PC:

* CRC16-Prüfsumme für UART-Kommunikation
* Anpassungen für Kommunikation (Synchronisation, Anmeldung als realer Bot)
* Anpassungen für Auswertung der Distanzsensoren (Umrechnung gemäß Kennlinie erfolgt bereits im Low-level Code)
* Anpassungen für Motorsteuerung (1:1 Weitergabe der Geschwindigkeit)
* Anpassungen für RC5-Code (Toggle-Bit Auswertung)
