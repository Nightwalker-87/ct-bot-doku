**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Erweiterungen von Lesern

>>> **Trac-2-Markdown Konvertierung:** *incomplete*

>> **Trac-2-Markdown Konvertierung:** *unchecked*

> **Trac-2-Markdown Konvertierung:** *deprecated*

## Einleitung

Sowohl der Roboter c't-Bot als auch der Simulator c't-Sim sind "Work in Progress". Beide bieten aktiven Programmierern viele Möglichkeiten, den Code zu erweitern und die Systeme raffinierter arbeiten zu lassen.

Damit Erweiterungen und Verfeinerungen zur aktuellen Codebasis passen, steht diese in Form eines SVN-Archivs zur Verfügung, das für alle lesbar ist. Die Schreibrechte sind allerdings nicht allgemein freigegeben. Eigener Erweiterungscode sollte uns daher als Patch verpackt zugeschickt werden, damit wir ihn auf dieser Seite auch anderen Roboter-Enthusiasten zur Verfügung stellen können.

Ein solcher Patch besteht aus einer Textdatei, die alle Unterschiede zwischen der lokalen Kopie des Codes und dem aktuellen Stand des SVN-Repositories aufführt. Wie man sie einspielt und eigene Patches erstellt, wird weiter unten auf dieser Seite erklärt.

## Patches für das Teilprojekt c't-Bot

**Datum**: 27.07.2007
**Autor**: Frank Menzel
**Beschreibung**: Abbruchbedingung für solve_maze()
Solve_maze wird eine Abbruchfunktion übergeben, welche true liefert wenn eben
solve_maze beendet werden soll. Das kann der Fall sein in
map_go_destination, falls der Pfadplaner keinen Erfolg hatte. Dann
geht’s weiter mit solve_maze solange, bis laut Map der Weg zum Ziel frei
ist, was wiederum mittels map_way_freefields gecheckt wird...
**gegen Version**: 1188
**Patchfile**:
[solve_maze_cancel.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/solve_maze_cancel.patch)

**Datum**: 22.06.2007
**Autor**: Achim Pankalla
**Beschreibung**: EEPROM-Emulation für PC
**gegen Version**: 1160
**Patchfile**: [eeprom_emu_v1.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/eeprom_emu_v1.patch)
*Dieser Patch ist in erweiterter Form im devel-Zweig des SVN seit Version 1187 enthalten.*

**Datum**: 19.05.2007
**Autor**: Frank Menzel
**Beschreibung**: Pfadplanung
**gegen Version**: 1150
**Patchfile**: [pathplaning.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/pathplaning.patch)
*Dieser Patch ist im devel-Zweig des SVN seit Version 1163 enthalten.*

**Datum**: 16.07.2006
**Autoren**: Peter Jonas und Achim Pankalla
**Beschreibung**: Kalibrierung der Distanzsensoren über EEPROM-Tabelle entwickelt. Kleine Optimierungen und Fehlerbehebung. Anpassung des Codes an die Coderichtlinien. Anpassung an neue Parameter, Funktionen und Änderungen am Code, damit die Kalibrierung auch im ct-Sim funktioniert. Vorraussetzung dafür ist, das der c't-Sim echte Sensorwerte liefert, wie zum Beispiel der Wettbewerbssimulator oder der Sim in Version V_0_8 zusammen mit [ct-sim_07.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_07.patch). Einführung zweier Funktionen zum Schreiben und Lesen des EEPROM des c't-bot. Damit wurde der Hardwarezugriff abstrahiert und ein EEPROM ist nun auch beim simulierten Bot vorhanden. Das EEPROM wird durch eine Datei repräsentiert.
**gegen Version** : Stand im CVS vom 11.07.2006
**Patchfile** : [ct-bot_04.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-bot_04.patch)

**Datum**: 13.07.2006
**Autor**: Frank Menzel
**Beschreibung**: Korrekturen in sensor.c bezüglich Geschwindigkeitsberechnung mit Maus
**gegen Version**: Stand im CVS vom 11.07.2006
**Patchfile**: [ct-bot_03.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-bot_03.patch)

**Datum**: 21.06.2006
**Autor**: Achim Pankalla
**Beschreibung**: Aktiviert die Funktion sensor_abstand() auch bei simulierten Bots. Dies wird notwendig, wenn der Simulator dank des Patches ct-sim_07.patch keine Abstandswerte in Metern mehr liefert, sondern simulierte Distanzsensor-Werte.
**gegen Version**: Stand im CVS vom 13.06.2006
**Sonstige Voraussetzungen**: [ct-sim_07.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_07.patch)
**Patchfile**: [ct-bot_02.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-bot_02.patch)

**Datum**: 23.02.2006
**Autor**: Carsten Giesen
**Beschreibung**: Wenn man die Stop-Taste drückt, werden die Variablen sensEncL und sensEncR auf Null gesetzt. Dadurch kann man einen Gleichlauf der beiden Encoder testen.
**gegen Version**: Stand im CVS vom 23.02.2006, 13:40 Uhr
**Patchfile**: [ct-bot_01.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-bot_01.patch)

## Patches für das Teilprojekt ct-Sim

**Datum**: 21.06.2006
**Autor**: Achim Pankalla
**Beschreibung**: Eine neue Funktion "watchGP2D12Obstacle" sorgt dafür, dass der
Simulator keine metrischen Distanzen mehr liefert, sondern ähnliche Werte wie die
GP2D12-Sensoren des echten Bot. Dafür benutzt sie eine Annäherungsfunktion, die
schon in [c't 6/06](http://www.heise.de/ct/06/06/264/) beschrieben wurde
und passt diese durch die Parameter a und b mehrfach an eine real ausgemessene
Sensorkurve an. a und b wurden durch Ausprobieren so bestimmt, das die berechneten
Analogwerte nah an der Kurve lagen. Jeder kann selbst die Kurve seines Bots
aufnehmen und die Werte entsprechend anpassen -- beim Referenzbot wurde die
Spannungsversorgung durch je zwei Kondensatoren mit 100nF und 10?F direkt am Sensor
stabilisiert. Um die Werte, wie auch beim realen Bot, etwas schwanken zu lassen,
wird ein Zufallswert addiert. Die Parameter a und b findet man in der Quelldatei
ctbotsim.java im Pfad ctSim-Model.Bots und dort in der Zeile 418. Die Werte für
rechts und links sind getrennt. Der Zufallswert wird in Zeile 446 hinzugezählt und
liegt im Moment bei 5. Das ist ein Kompromiss - streng genommen sollte dieser Wert
im steilen Bereich der Kennlinie größer sein als im flachen Endteil. Damit der für
den Simulatorbetrieb übersetzte C-Bot auch beim höchsten Kurvenwert den richtigen
Abstand anzeigt, ist es eventuell notwendig, die Datei sensor_correction.h im
ct-bot-Quellcode anzupassen. Der Wert der Konstanten SENSDISTSLOPE für den PC kann
nach folgender Formel berechnet werden: SENSDISTSLOPE = (Sensormaxwert - 3) *
Abstand bei Ho"chstwert in mm. Dieser Wert wird für rechts und links berechnet und
gemittelt.
**gegen Version**: Stand im CVS vom 14.06.2006
**Sonstige Voraussetzungen**: [ct-bot_02.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-bot_02.patch)
**Patchfile**: [ct-sim_07.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_07.patch)

**Datum**: 21.04.2006
**Autor**: Carsten Giesen
**Beschreibung**: Stattet den c't-Sim mit allen Tasten der Fernbedienung Hauppauge MediaMPV aus.
**gegen Version**: 0.3 (vom 10.04.2006)
**Patchfile**: [ct-sim_06.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_06.patch)

**Datum**: 05.04.2006
**Autor**: Johannes Dörnte
**Beschreibung**: Wählen der Welt in world.java über eine Konstante. Man kann zwischen dem Labyrinth aus c't 5/06 und dem Hindernis-Parcours aus 7/06 wechseln
**gegen Version**: 0.3
**Patchfile**: [ct-sim_05.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_05.patch)

**Datum**: 14.03.2006
**Autor**: Stefan Geuken
**Beschreibung**: LCDisplay mit Foto des Originaldisplays als Hintergrundbild auf der Kontrolltafel im c't-Sim
**gegen Version**: 0.2 (vom 05.03.2006)
**Patchfile**: [ct-sim_04.zip](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_04.zip)

**Datum**: 12.03.2006
**Autor**: Markus Lang
**Beschreibung**: Vereint die beiden Fenster (Kontrollfenster und WorldView) des c't-Sim mittels einer JSplitPane zu einem großen Fenster.
**gegen Version**: 0.2 (vom 05.03.2006)
**in Codebasis ab Version**: voraussichtlich 0.4
**Patchfile**: [ct-sim_03.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_03.patch)

**Datum**: 21.02.2006
**Autor**: Fabian Recktenwald
**Beschreibung**: Basierend auf der verbesserten Positionberechnung ([Patch 1](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_01.patch)), korrigiert dieser Patch die Werteberechnung für den Maussensor. Dies setzt voraus, dass der Maussensor in gerader Linie hinter dem Mittelpunkt des Bot sitzt (SENS_MOUSE_ABSTAND_X==0).
**gegen Version**: 0.2
**Sonstige Voraussetzungen**: [ct-sim_01.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_01.patch)
**in Codebasis ab Version**: voraussichtlich 0.4
**Patchfile**: [ct-sim_02.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_02.patch)

**Datum**: 21.02.2006
**Autor**: Fabian Recktenwald
**Beschreibung**: Dieser Patch ersetzt die genäherte Positionsberechnung des Bot in der Funktion updateStats() (siehe [c't 03/06](http://www.heise.de/ct/06/03/186/)) durch eine mathematisch korrekte Positionsbestimmung.
**gegen Version**: 0.2
**in Codebasis ab Version**: voraussichtlich 0.4
**Patchfile**: [ct-sim_01.patch](http://www.heise.de/ct/projekte/machmit/ctbot/attachment/wiki/Patches/ct-sim_01.patch)

## So spielen Sie einen Patch von dieser Seite ein

Wählen Sie in Eclipse unter "Team/Apply Patch" den Ordner des Projekts aus, das der Patch erweitert (z.B. ct-Sim). Den Pfad zur Patch-Datei können Sie entweder per Hand einfügen oder Sie suchen die Datei über "Browse...". Wird Ihnen im nächsten Schritt gemeldet, bestimmte zu erweiternde Dateien würden nicht existieren, ist wahrscheinlich der falsche Ordner ausgewählt. "Finish" schließt den Vorgang ab. Weitere Details lassen sich in der Hilfe von Eclipse ("Working with Patches") nachlesen.

## So erzeugen Sie selbst einen Patch, um ihn bei uns einzureichen

Haben Sie an einem oder mehreren Source-Files etwas geändert, so stellen Sie zunächst über "Team/Synchronize with Repository" sicher, dass Eclipse der aktuelle Zustand des Codes im SVN bekannt ist. Um Ihre lokalen Änderungen in einen Patch zu verpacken, wählen Sie "Team/Create Patch..." Anschließend wählen Sie einen sprechenden Dateinamen für Ihren Patch (z.B. "zeitlupe.patch") und suchen sich einen Ort zum Speichern auf Ihrem System aus. Das "Diff output format" sollte "Unified" und der Patch projektbasiert (also kein "Workspace-Patch") sein, das erleichtert hinterher anderen Nutzern, Ihren Patch zu übernehmen.

Damit die Patches möglichst kompatibel zueinander sind und überschaubar bleiben, sollten sie schlank sein — Faustregel: Ein Patch pro Thema. Insbesondere Formatierungsänderungen usw. blähen den Patch stark auf und machen ihn im Zweifelsfall inkompatibel zu anderen.

Wir empfehlen dazu, das Repository zweimal aus dem SVN in Eclipse zu importieren: Einmal für eigene Experimente, einmal, um die fertigen Ergebnisse zum Export vorzubereiten.

Im "privaten" Repository kann man dann nach Belieben basteln und experimentieren. Dann erstellt man einen Patch und spielt ihn in sein "Export"-Repository ein. Dabei kann man sehr einfach und detailliert auswählen, welche Teile man übernehmen will. Am Ende erstellt man aus dem "Export"-Repository wieder einen neuen Patch, den man bei uns einreicht. Patch-Dateien sind übrigens reine ASCII-Files, man kann zur Not auch mit einem Texteditor noch Teile löschen.

Dokumentieren Sie Ihren Patch ausführlich und beachten Sie dabei bitte unsere Code-Richtlinen — so fällt es uns und den anderen Lesern leichter zu verstehen, inwiefern Ihre Erweiterung den Simulator oder den Bot verbessert. Zusätzlich sollten Sie einen kurzen Text von zwei bis drei Sätzen beilegen, der oben auf dieser Seite als Beschreibung veröffentlicht werden kann und sich auch im Changelog wiederfindet.

Wer das Eclipse-Plugin *!AnyEdit* verwendet, schaltet vor der Dateibearbeitung bitte unbedingt die Option *Convert tabs <> spaces* *aus*.

Die Datei *.cproject* gehört nicht mit in den Patch, in ihr befinden sich z.B. die Compiler-Pfadangaben, die systemabhängig sind.

**Checkliste** für eigene Patches:

Bevor Sie einen Patch einreichen, sollten Sie folgende Dinge prüfen. Patches, die folgende Checkliste nicht bestehen, können wir leider nicht bearbeiten.

* Ist der Patch sorgfältig in allen Projektkonstellationen (PC und MCU, c't-Sim) **getestet**?
* Wurde der Patch gegen die **aktuelle Version des SVN** erstellt?
* Enthält der Patch einen **Changelog-Eintrag**?
* Sind alle Funktionen und globalen Variablen **doxygen-konform dokumentiert** (bitte einmal Doxygen durchlaufen lassen und prüfen, ob es auch keine Warnungen mehr wirf)?
* Falls ein neues Verhalten hinzugefügt wurde, wurde das #define im **Doxygen-File** aktiviert?
* Falls neue Quellcode-Dateien hinuzgefügt wurden, wurde auch das **Makefile** entsprechend aktualisiert?
* Enthält der Patch keine Änderungen, die nur beim Debuggen nötig waren? ([siehe FAQ](https://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html))
* Befolgt der Patch alle Anforderung der [Coding-Richtlinien](../../doc/wiki_pages/coding_conventions.md)?
* Ist der Quellcode passend zum Projekt **formatiert**? Hier hilft die automatische Formatierung von Eclipse, die über *Sources -> Format* zu erreichen ist.
* Benötigt der Patch zusätzliche **Dokumentation** hier im Wiki?
* Wenn der Patch Code von Dritten enthält: Ist geprüft, ob deren Code in einem GPL-Projekt veröffentlicht werden darf? Sind die Namen der ursprünglichen Autoren genannt?
* Enthält die Mail zum Einreichen des Patches folgende **Informationen**: Zweck und Motivation des Patches, den Patch selbst (als eine komprimierte Zip-Datei) und eine Beschreibung der durchgeführten Tests?
