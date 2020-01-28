**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Installationsanleitung für den c't-Bot und den c't-Sim

>> **Trac-2-Markdown Konvertierung:** *unchecked*

Diese Anleitung gilt ab Release 23.

## I. Java und Eclipse installieren

1. Java
    * Linux: Aktuelles Java **JDK** am besten über die Paketverwaltung installieren
    * Mac / Windows: Aktuelles Java **JDK** [herunterladen](http://www.oracle.com/technetwork/java/javase/downloads/index.html) und installieren. Getestete Version: 8u121
    * **Hinweis**: Für Java 9 ist eine Eclipse Version ab 4.7.1a zwingend erforderlich.
1. Eclipse
    * Eclipse herunterladen und installieren, siehe [Anleitung zur Einrichtung von Eclipse](../EclipseInstallation/EclipseInstallation.md). Getestete Version: Eclipse Neon (4.6)

## II. Compiler für simulierte Bots (x86) installieren

* Linux: gcc über die Paketverwaltung installieren
* Mac: [Xcode](https://itunes.apple.com/de/app/xcode/id497799835?mt=12) installieren, im Terminal `xcode-select --install` ausführen um die Command Line Tools zu installieren.
* Windows
  1. msys2 installieren (siehe auch [msys2 Installationsanleitung](http://msys2.github.io))
     1. Installer [hier](http://msys2.github.io) herunterladen (*msys2-x86_64-*XYZ*.exe*) und ausführen
     1. Als Installationsordner `C:\msys64` verwenden (wie gehen hier von der 64-Bit Version aus)
  1. gcc von msys2 installieren
     1. *MinGW-w64 Win64 Shell* starten
     1. `pacman -Suy` ausführen, um msys2 zu aktualisieren
     1. `pacman -S mingw-w64-x86_64-gcc make` ausführen, um Compiler zu installieren
  1. Windows PATH-Eintrag in der Systemsteuerung [erweitern](http://techmixx.de/windows-10-umgebungsvariablen-bearbeiten/) um `C:\msys64\mingw64\bin` (sonst werden beim Start von ct-Bot.exe die nötigen Libraries nicht gefunden)
  1. PATH-Einträge in Eclipse erweitern um `C:\msys64\usr\bin;C:\msys64\mingw64\bin`
     1. In Eclipse `Window->Preferences->C/C++->Build->Environment` öffnen
     1. `Select...` -> `Path` -> `Edit...`
     1. Am **Anfang** hinzufügen: `C:\msys64\usr\bin;C:\msys64\mingw64\bin;`

## III. Compiler für reale Bots (ATmega) installieren

* Linux: **AVR Toolchain for Linux** [herunterladen](http://www.atmel.com/tools/ATMELAVRTOOLCHAINFORLINUX.aspx) (**8-bit** Version) und entpacken, z.B. nach `/usr/local/`. Getestete Version: 3.5.4
* Mac: **AVR Toolchain for Mac OS X** [herunterladen](http://distribute.atmel.no/tools/opensource/Atmel-AVR-GNU-Toolchain/3.5.4/) (derzeit *avr8-gnu-toolchain-osx-3.5.4.468-darwin.any.x86_64.tar.gz*) und entpacken nach `/usr/local/`. Getestete Version: 3.5.4
* Windows: **AVR Toolchain for Windows** [herunterladen](http://www.atmel.com/tools/ATMELAVRTOOLCHAINFORWINDOWS.aspx) und installieren. Das Installationsprogramm sollte man dabei explizit als Administrator ausführen (via Kontextmenü), sonst schlägt der Installer einen komischen Installationsort vor anstatt höhere Rechte anzufordern. Getestete Version: 3.5.4

1. Den Pfad zum avr-gcc (Unterverzeichnis `bin`) anschließend ebenfalls in Eclipse zum **PATH** hinzufügen:
   1. PATH-Einträge erweitern um `C:\Program Files (x86)\avr8-gnu-toolchain\bin` (Windows) bzw. `/usr/local/avr8-gnu-toolchain-linux_x86/bin` (Linux) oder `/usr/local/avr8-gnu-toolchain-darwin_x86_64/bin` (Mac) in Eclipse
   1. In Eclipse `Window->Preferences->C/C++->Build->Environment` öffnen
   1. `Select...` -> `Path` -> `Edit...`
   1. Am **Ende** hinzufügen: `;C:\Program Files (x86)\avr8-gnu-toolchain\bin` (Windows) bzw. `:/usr/local/avr8-gnu-toolchain-linux_x86/bin` (Linux) oder `:/usr/local/avr8-gnu-toolchain-darwin_x86_64/bin` (Mac)

## IV. Code für Bot und Sim importieren

Der Code steht im GIT-Repository zur Verfügung, siehe [Import des Codes von Github](../GITUndEclipse/GITUndEclipse.md)

## V. Installation Testen / weitere Schritte

### Hinweise

  1. Evtl. bekommt man in Eclipse Warnings ähnlich der Folgenden angezeigt: `Program "arm-linux-gnueabihf-g++" not found in PATH` Diese kann man ignorieren, wenn man das zugehörige Target nicht braucht (z.B. Build für Raspberry Pi im Falle von arm-linux-gnueabihf). Um die Warnings zu entfernen kann man die nicht benötigten Configurations in den Projekteinstellungen unter *C/C++ Build* -> *Manage Configurations...* löschen.

### ct-Sim und virtuelle Bots starten

1. c't-Sim starten. Hierzu gibt es zwei gleichwertige Möglichkeiten:
    * In Eclipse klickt man die Datei	ctSim/controller/Main.java rechts an und wählt "Run As/Application". (Tipp: Nach dem ersten "Run" startet Strg-F11 die zuletzt ausgeführte Datei.)
    * Von der Kommandozeile aus wechselt man in das Verzeichnis, in dem Eclipse das ctSim-Projekt aufhebt (ein Unterverzeichnis des Eclipse-Workspace, den man bei der Eclipse-Installation angegeben hat). Dort: `java ctSim.controller.Main`
1. Falls nicht schon geschehen, c't-Bot compilieren *(ct-Bot-Projekt markieren und "!Project/Clean" wählen)*
1. c't-Bot starten:
    * In Eclipse: Im ct-Bot-Projekt die Datei Debug-Linux_Mac/ct-Bot (Linux und Mac) bzw. Debug-W32\ct-Bot.exe doppelt anklicken
    * Auf der Kommandozeile: Wechsel in das Verzeichnis, in dem Eclipse das ct-Bot-Projekt aufhebt, und die genannte Datei ausführen

Hinweis: Die Datei ct-Bot.exe bzw. ct-Bot beendet sich zügig wieder, wenn sie keinen Simulator findet, der auf ihren Versuch einer TCP/IP-Verbindung antwortet. Daher ist die Reihenfolge "zuerst Sim, dann Bot" wichtig.

## VI. Compiler für Raspberry Pi installieren (optional)

### Für Raspberry Pi 2

* Linux (x86_64):
  1. Toolchain verfügbar auf [Github](https://github.com/tsandmann/arm-toolchain-linux)
  1. `sudo git clone --depth=1 https://github.com/tsandmann/arm-toolchain-linux.git /usr/local/arm-unknown-linux-gnueabihf`
* Mac (x86_64):
  1. Toolchain verfügbar auf [Github](https://github.com/tsandmann/arm-toolchain-mac)
  1. `sudo git clone --depth=1 https://github.com/tsandmann/arm-toolchain-mac.git /usr/local/arm-unknown-linux-gnueabihf`
* Windows:
  1. Linaro Toolchain `gcc-linaro-7.1.1-2017.05-i686-mingw32_arm-linux-gnueabihf.tar.xz` herunterladen von [https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/arm-linux-gnueabihf/](https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/arm-linux-gnueabihf/): [direktlink](https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/arm-linux-gnueabihf/gcc-linaro-7.1.1-2017.05-i686-mingw32_arm-linux-gnueabihf.tar.xz)
  1. Entpacken nach `C:\Program Files (x86)\arm-linux-gnueabihf`
* Den Pfad zum arm-gcc (Unterverzeichnis `bin`) anschließend ebenfalls in Eclipse zum **PATH** hinzufügen:
   1. PATH-Einträge erweitern um `C:\Program Files (x86)\arm-linux-gnueabihf\bin` (Windows) bzw. `/usr/local/arm-unknown-linux-gnueabihf/bin` (Linux / Mac) in Eclipse
   1. In Eclipse `Window->Preferences->C/C++->Build->Environment` öffnen
   1. `Select...` -> `Path` -> `Edit...`
   1. Am Ende hinzufügen: `;C:\Program Files (x86)\arm-linux-gnueabihf\bin` (Windows) bzw. `:/usr/local/arm-unknown-linux-gnueabihf/bin` (Linux / Mac)

### Für Raspberry Pi 3

* Linux (x86_64):
  1. Toolchain verfügbar auf [Github](https://github.com/tsandmann/armv8l-toolchain-linux)
  1. `sudo git clone --depth=1 https://github.com/tsandmann/armv8l-toolchain-linux.git /usr/local/armv8l-unknown-linux-gnueabihf`
* Mac (x86_64):
  1. Toolchain verfügbar auf [Github](https://github.com/tsandmann/armv8l-toolchain-mac)
  1. `sudo git clone --depth=1 https://github.com/tsandmann/armv8l-toolchain-mac.git /usr/local/armv8l-unknown-linux-gnueabihf`
* Windows:
  1. Linaro Toolchain `gcc-linaro-7.1.1-2017.05-i686-mingw32_armv8l-linux-gnueabihf.tar.xz` herunterladen von [https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/armv8l-linux-gnueabihf/](https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/armv8l-linux-gnueabihf/): [direktlink](https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/armv8l-linux-gnueabihf/gcc-linaro-7.1.1-2017.05-i686-mingw32_armv8l-linux-gnueabihf.tar.xz)
  1. Entpacken nach `C:\Program Files (x86)\armv8l-unknown-linux-gnueabihf`
* Den Pfad zum arm-gcc (Unterverzeichnis `bin`) anschließend ebenfalls in Eclipse zum **PATH** hinzufügen:
   1. PATH-Einträge erweitern um `C:\Program Files (x86)\armv8l-unknown-linux-gnueabihf\bin` (Windows) bzw. `/usr/local/armv8l-unknown-linux-gnueabihf/bin` (Linux / Mac) in Eclipse
   1. In Eclipse `Window->Preferences->C/C++->Build->Environment` öffnen
   1. `Select...` -> `Path` -> `Edit...`
   1. Am Ende hinzufügen: `;C:\Program Files (x86)\armv8l-unknown-linux-gnueabihf\bin` (Windows) bzw. `:/usr/local/armv8l-unknown-linux-gnueabihf/bin` (Linux / Mac)
