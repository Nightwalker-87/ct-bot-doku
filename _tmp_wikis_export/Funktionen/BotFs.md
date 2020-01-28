**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# SD-Karten Dateisystem BotFS

> **Trac-2-Markdown Konvertierung:** *deprecated*

Stand: SVN Rev. 1892

## Einleitung

Um von der SD-Karten-Ansteuerung, der Formatierung und weiteren Details zu abstrahieren, existiert das SD-Karten Dateisystem *BotFS* im c't-Bot Framework. Es ist deutlich schlanker als ein FAT16 Dateisystem, verhindert die Fragmentierung von Dateien (wichtig für die Echtzeitfähigkeit der Kartographie) und abstrahiert vollständig von der Zielplattform, so dass für simulierte und reale Bots dieselbe Programmierschnittstelle bereitsteht.

Das Dateisystem befindet sich komplett in einer Image-Datei (*botfs.img*), die bei realen Bots den gesamten Speicherplatz einer FAT16-Partition auf der SD-Karte einnehmen muss (damit keine Fragmentierung auftritt) und für simulierte Bots automatisch im Arbeitsverzeichnis des Bots angelegt wird.

Das BotFS-Dateisystem wird derzeit von der Map, den [Skriptsprachen](../DokuScriptLanguages/DokuScriptLanguages.md) *ABL* und *uBasic*, dem [Speedlog](../ct-Bot-Software-Aktuatoren/ct-Bot-Software-Aktuatoren.md#Die-Logging-Funktion) und der Log-2-MMC Funktion genutzt.

## Einmalige Einrichtung

### PC

Es sind keine Vorbereitungen nötig, ist kein Volume vorhanden, wird es automatisch angelegt und dazu eine Datei mit dem in `BOTFS_IMAGE_FILENAME` festgeleten Namen angelegt, standardmäßig *botfs.img*. Achtung, dieses Volume hat dann nicht die für MCU benötigte Größe (s.u.). Möchte man Daten zwischen MCU und PC austauschen, kopiert man die Datei von der MMC / SD-Karte ins Bot-Verzeichnis und überschreibt damit eine eventuell automatisch angelegte Datei.

### MCU

Um BotFS auf MCU mit MMC / SD-Karte nutzen zu können, muss die Karte einmalig dafür vorbereitet werden. Es gibt dazu drei mögliche Varianten:

#### Variante 1: Vorgefertigtes Disk-Image auf die SD-Karte übertragen

* \+ SD-Karte braucht nicht manuell partioniert werden
* \+ Nur ein Arbeitsschritt nötig
* \- Löscht die komplette SD-Karte
* \- unter Windows externes Tool nötig

#### Variante 2: Manuelle Partionierung, anschließende Einrichtung mit Hilfsprogramm

* \+ volle Kontrolle über die Partitionierung
* \+ Partions- und Imagegröße anpassbar (max. 32 MByte)
* \- mehrere Arbeitsschritte nötig
* \- Partionierung unter Windows eventuell umständlich
* \- Wert von `first_block` in *pc/botfs-low_pc.c* muss angepasst werden, wenn man BotFS-Dateien am PC erzeugen und auf dem echten Bot verwenden möchte

#### Variante 3: vollständig manuelle Einrichtung

* \+ volle Kontrolle über alle Schritte
* \- recht umständlich
* \- Wert von `first_block` in *pc/botfs-low_pc.c* muss angepasst werden, wenn man BotFS-Dateien am PC erzeugen und auf dem echten Bot verwenden möchte

#### Durchführung Variante 1

Übertragen des vorgefertigten Disk-Images (befindet sich in *contrib/BotFS/sd.img.zip*):

* unter Linux:
  1. Device-Node des Kartenlesers ausfindig machen, z.B. `/dev/sdb` wie im Folgenden
  1. Eventuell vorhandene Partitionen auf der SD-Karten unmounten
  1. `sudo gunzip -c sd.img.zip | dd of=/dev/sdb bs=4k`
 *`/dev/sdb`*
  1. `sync`

* unter Mac OS X:
  1. Disk-Nummer des Kartenlesers ausfinden machen (Festplatten-Dienstprogramm -> Info oder diskutil list), im folgenden Beispiel `disk3`
  1. `sudo diskutil unmountDisk /dev/rdisk3`
  1. `sudo gunzip -c sd.img.zip | dd of=/dev/rdisk3 bs=4k`
 *`/dev/rdisk3`*
  1. `sync`

* unter Windows:
  1. physdiskwrite + PhysGUI von [https://m0n0.ch/wall/physdiskwrite.php](http://m0n0.ch/wall/physdiskwrite.php) herunterladen und entpacken
  1. *sd.img.zip* entpacken, erzeugt die Datei *sd.img*
  1. PhysGUI.exe (als Administrator) starten
  1. Rechtsklick auf den Eintrag des Kartenlesers -> Image laden -> Öffnen -> *sd.img* auswählen -> OK -> Ja
  1. Hardawre sicher entfernen -> auswerfen ausführen

#### Durchführung Variante 2

* Einrichtung mit Hilfsprogramm BotFS Helper: Das Programm legt auf einer maximal 32 MB grossen FAT16-Partition einer SD-Karte ein BotFS-Image an.
* Zunächst legt man auf der Karte eine FAT16-Partition an, die maximal 32 MByte groß ist. Diese muss die erste Partition auf der Karte sein, weitere Partitionen können problemlos folgen. Auf der SD-Karte muss unbedingt eine *MBR*-Partitionstabelle verwendet werden, GPT wird nicht unterstützt! Um durch Rechenweise und Aufrundungen des verwendeten Partitionstools nicht die 32 MByte-Grenze zu überschreiten, empfiehlt es sich, eine Partition von 30 MByte anzulegen - wichtig ist, dass die Größe der erzeugten Partition 32 MByte, also 32 * 2^20^ Byte, nicht überschreitet. Auf der angelegten Partition müssen unbedingt alle Dateien (auch eventuelle Versteckte) gelöscht werden, so dass die gesamte Partitionsgröße als freier Speicher verfügbar ist. Anschließend ruft man das Hilfsprogramm aus *contrib/BotFS* wie folgt auf:
  * Linux: `./ct-Bot-botfshelper ABSOLUTER_PFAD_ZUR_SD-KARTE` also z.B. `./ct-Bot-botfshelper /media/SD`
  * Mac: `./ct-Bot-botfshelper ABSOLUTER_PFAD_ZUR_SD-KARTE` also z.B. `./ct-Bot-botfshelper /Volumes/SD`
  * Windows: `ct-Bot-botfshelper.exe ABSOLUTER_PFAD_ZUR_SD-KARTE` also z.B. `ct-Bot-botfshelper.exe e:\`
* Es bietet sich an, auf der SD-Karte auch eine zweite Partition (Größe und Typ beliebig) anzulegen und dort eine Kopie der Datei *botfs.img* zu speichern. Möchte man einmal das komplette Dateisystem für den Bot leeren oder wurde es durch einen Fehler beschädigt, kopiert man einfach dieses Backup zurück auf die erste Partition und muss die obigen Schritte nicht wiederholen.
* Wenn man BotFS-Dateien am PC erzeugen und auf dem echten Bot verwenden möchte, sollte man den Wert von `first_block` in *pc/botfs-low_pc.c* anpassen, damit das Alignment von Dateien (zur Performanzsteigerung z.B. für die Map) stimmt. `first_block` muss dazu auf den ersten Datensektor der FAT16-Partition gesetzt werden.

#### Durchführung Variante 3

Anlegen der Partition wie unter Variante 2. Anschließend ermittelt man die exakte Größe der Partition (je nach Betriebssystem findet sich diese in den Eigenschaften / Informationen des Laufwerks) in Byte und notiert sie. Auf der angelegten Partition müssen unbedingt alle Dateien (auch eventuelle Versteckte) gelöscht werden, so dass die gesamte Partitionsgröße als freier Speicher verfügbar ist. Die notierte Größe teil man noch durch 1024 und erhält so die gewünschte Image-Größe in KByte. Nun startet man den für PC (mit `BOT_FS_AVAILABLE`) compilierten Bot-Code mit dem Parameter *-f*, also `ct-Bot(.exe) -f`, um die BotFS-Verwaltung aufzurufen. Dort gibt man `create volume` ein und bestätigt das Kommando mit Enter. Als Dateinamen wählt man anschließend einen Namen wie `botfs.img`, eine solche Datei darf aber noch nicht existieren.  Eine komplette Pfadangabe ist auch möglich, ansonsten wird die Datei im aktuellen Arbeitsverzeichnis erstellt. Als Volume-Name gibt man dann einen Beliebigen ein, wie z.B. `BotFS-Volume`, als Größe danach die eben Ermittelte (in KByte). Jetzt kann die Verwaltung mit dem Kommando `q` beendet werden und die erzeugte Datei als *botfs.img* (wichtig: auf der SD-Karte muss die Datei unbedingt *botfs.img* heißen!) auf die SD-Karte (erste Partition) kopiert werden.

Wenn man BotFS-Dateien am PC erzeugen und auf dem echten Bot verwenden möchte, sollte man den Wert von `first_block` in *pc/botfs-low_pc.c* anpassen, damit das Alignment von Dateien (zur Performanzsteigerung z.B. für die Map) stimmt. `first_block` muss dazu auf den ersten Datensektor der FAT16-Partition gesetzt werden.

## Benutzung

* Der Map-Code ist jetzt (mit `BOT_FS_AVAILABLE`) nicht mehr darauf angewiesen, dass eine Map-Datei (MiniFAT) auf der SD-Karte bereits vorhanden ist. Sobald das BotFS-Volume einmal auf der SD-Karte eingerichtet ist (s.o.), regelt der Map-Code den Rest automatisch. Insbesondere das Löschen einer alten Map (beim Start) geht mit `BOT_FS_AVAILABLE` dann auch deutlich schneller.
* Möchte man Daten zwischen dem echten und einem simulierten Bot austauschen, kann man die *botfs.img*-Datei beliebig zwischen diesen kopieren, oder den simulierten Bot mit dem Parameter *-i* und der Image-Datei (z.B. auch direkt von der eingelegten SD-Karte) starten.
* In der BotFS-Verwaltung (über `ct-Bot(.exe) -f [Pfad zur Image-Datei]` aufzurufen) zeigt das Kommando `help` eine Übersicht aller verfuegbaren Tools an. Wird im Normalbetrieb aber eigentlich nicht benötigt.
