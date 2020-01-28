# Projekthistorie von c't-Bot und c't-Sim

Änderungen in den jeweiligen Releases finden sich in den Changelogs:

- [Changelog für den c't-Bot](https://github.com/tsandmann/ct-bot/blob/master/Changelog.txt)
- [Changelog für den c't-Sim](https://github.com/tsandmann/ct-sim/blob/master/Changelog.txt)

**18.10.2018** **Release 26** für den Bot- und Sim-Code

**29.03.2018** Die Projektdokumentation ist in das GitHub-Projekt [ct-bot-doku](https://github.com/Nightwalker-87/ct-bot-doku) umgezogen.

**17.01.2018** **Release 25.1** für den Bot- und Sim-Code

**01.10.2017** **Release 25** für den Bot- und Sim-Code

**12.03.2017** **Release 24** für den Bot- und Sim-Code

**15.10.2016** Unterstützung für den ATmega32 Mikrocontroller entfernt.

**09.07.2016** **Release 23** für den Bot- und Sim-Code

**26.10.2015** **Release 22** für den Bot- und Sim-Code

**29.02.2012** **Release 21** für den Bot- und Sim-Code

**03.02.2012** Dokumentation im Wiki wesentlich überarbeitet und aktualisiert.

**18.08.2011** **Release 20** für den Bot- und Sim-Code

**12.04.2011** **Release 19** für den Bot- und Sim-Code

**16.10.2010** **Release 18** für den Bot- und Sim-Code

**23.05.2010** **Release 17** für den Bot- und Sim-Code

**29.01.2010** Einige Code-Optimierungen (vor allem im Positions- und Map-Code) und Fehlerabschätzung bei der Positionsberechnung über die Option *MEASURE_POSITION_ERRORS_AVAILABLE*

**02.12.2009** Für den Bot-Code ist jetzt eine PDF-Dokumentation verfügbar.

**17.11.2009** Der Bot spielt Schach! Neues Schachverhalten *behaviour_drive_chess()* von Frank Menzel hinzugefügt.

**18.10.2009** Positionsspeicher können nun mit individueller Größe angelegt werden und sind außerdem per Bot-2-Bot-Kommunikation übertragbar.

**28.09.2009** Aktualisierung der Eclipse-Anleitung auf Version 3.5

**17.09.2009** Beta-Code zur Selbstlokalisierung des ct-Bots

**06.07.2009** **Release 16** für den Bot- und Sim-Code

**29.05.2009** Verbesserung des Verhaltens *bot_drive_area()*

**19.04.2009** Neues Video in der Galerie

**17.04.2009** Dokumentation zum BotOS

**13.03.2009** Per Bot-2-Bot-Kommunikation lassen sich nun auch RemoteCalls an einen anderen Bot schicken.

**06.03.2009** Aktualisierung und Neugestaltung des Wikis inklusive der Aufbauanleitungen

**02.03.2009** Der ct-Sim kann nun live die vom Bot erstellte Map anzeigen, sowohl von simulierten als auch von echten Bots.

**27.02.2009** In der Galerie wurden zwei neue Videos zum neuen Verhalten *bot_follow_line_enh()* hinzugefügt.

**26.02.2009** Neues Verhalten *bot_follow_line_enh()* von Frank Menzel (devel-Zweig)

**25.02.2009** Mit der SVN Revision #1554 gibt es etliche Verbesserungen der ct-Bot-Firmware.

**16.01.2009** Die Bot-2-Bot-Kommunikation unterstützt nun den Payload-Versand.

**13.01.2009** Neues Verhalten *bot_line_shortest_way()* von Frank Menzel (devel-Zweig)

**21.11.2008** ct-Sim kann die Map des Bots nun zur Laufzeit anzeigen. (devel-Zweig)

**29.10.2008** **Release 15** für den Bot- und Sim-Code

**05.04.2008** Kleinere Bugfixes im stable- und im devel-Zweig

**30.03.2008** SP03-Treiber Update (devel-Zweig)

**29.03.2008** Das Framework wurde um eine Bot-2-Bot-Kommunikation ergänzt. (devel-Zweig)

**29.02.2008** **Release 14** für den Bot- und Sim-Code

**30.11.2007** Der Treiber für das Sprachausgabemodul [SP03](http://www.robot-electronics.co.uk/htm/Sp03doc.shtml) von Harald W. Leschner befindet sich jetzt im SVN.
Damit lassen sich Strings als Sprache ausgeben; zurzeit nur auf dem echten Bot.
Weitere Informationen hierzu finden sich in _mcu/sp03.c_.

**12.11.2007** Frank Menzel hat ein neues Verhalten _behaviour_transport_pillar_ entwickelt:
Ein Bot fährt hier zwischen Start- und Zielposition hin und her und kann dabei Dosen einfangen und transportieren.

**11.11.2007** Unter contrib/tools sind zwei Scripte von Harald W. Leschner vorhanden, die eine einfache Speedlog-Auswertung mit Gnuplot und LaTeX ermöglichen.

**01.11.2007** Es gibt jetzt aktualisierte Test-Binaries, die auf dem aktuellen Code basieren.

**30.08.2007** Es gibt ein neues Verhalten *bot_follow_wall_behaviour* von Frank Menzel.

**13.07.2007** Die PC-EEPROM-Emulation von Achim Pankalla ist nun im SVN integriert.

**12.07.2007** Es gibt nun auch Delay_Routinen als Bot-Verhalten.

**26.06.2007** Das Pfadplanungsverhalten von Frank Menzel ist nun komplett mit Dokumentation im SVN zu finden.

**26.06.2007** Die Leserpatches sind nun auch ins Wiki umgezogen, wodurch man nun selbst neue Patches hochladen kann.

**04.05.2007** Zur Webseite des c't-Projektes gehört nun auch ein Trac-System.
Der Code ist nun offiziell ins SVN umgezogen.

**30.03.2007** Es gibt eine Wiki-Seite für Diskussionen, Ideen und Anregungen rund um neue Verhalten für den c't-Bot.

**29.03.2007** Ab sofort ist der Code aus dem alten Public-CVS im Subversion.

**07.03.2007** Ab sofort ist der Code aus dem alten (internen) CVS im Subversion.

**22.02.2007** **Release 13** für den Bot-Code:

Wichtigste Änderung dürfte das neue User-Interface sein.
Wir haben Ausgaberoutinen und Fernbedienungsabfragen in einem Verzeichnis ui/ gesammelt.
Dort kann man nun recht bequem nene Screens definieren und für jede Screen selbst die RC5-Kommandos abarbeiten.
Das entschlackt sowohl die Datei _rc5.c_ als auch _ct-Bot.c_ deutlich.
Welche Screens aktiv sein sollen steht in _available_sreens.h_.
Die Definition der Screens kann entweder in eigenen Dateien in ui/ via _misc.c_ erfolgen, oder aber an Ort und Stelle, wo sie inhaltlich hingehört (siehe _bot-logik.c_).
Wichtig ist nur, das man die neuen Screens auch am System anmeldet (siehe _gui.c_).

**22.02.2007** **Release 13** für den Sim-Code:

- Erste Version eines Applets, das man auf WLAN-Bot laden kann
- Reale Bots können sich wieder verbinden (per USB und per TCP für WLAN-Bots)
- Wettbewerbs-System, so wie es im Oktober verwendet wurde (ctSim.view.contestConductor)
- Remote-Calls
- Diverse Verbesserungen und Umstellungen

**Achtung**: Die _main()_-Methode des ctSim ist umgezogen.
Sie wohnt nicht mehr in _ctSim.controller.Controller_, sondern in _ctSim.controller.Main_.
Zum Starten des c't-Sim muss man also _Main_ laufenlassen und nicht _Controller_.
Alte "Run"-Profile in Eclipse müssen dementsprechend angepasst werden.

**21.02.2007** Die Java Virtual Machine [NanoVM](http://sourceforge.net/projects/nanovm) unterstützt seit der Version 1.5 auch den c't-Bot.
Wer möchte, kann seinen Robotersteuercode somit nun auch in Java schreiben.

**18.01.2007** Die bebilderte Aufbauanleitung für das Erweiterungsmodul ist online.
Die Auslieferung der Teilesätze beginnt in Kürze.

**17.01.2007** Wir haben dem Code-Archiv des c't-Bot nun einen Bootloader hinzugefügt.
Mit diesem kann man den Bot sehr schnell und bequem flashen.
Das Übertragen eines Hex-Files dauert nun nur noch 14 Sekunden.
Der Bootloader funktioniert sowohl mit RS-232-, USB-2-Bot-, LAN-, als auch WLAN-Verbindungen.
Sobald der Bootloader einmal auf dem Bot installiert ist braucht man den Programmieradapter nicht mehr.

**15.01.2007** Wir haben den c't-Bot-Code im CVS deutlich überarbeitet.
Der Code unbterstützt nun auch die Fähigkeiten des Erweiterungsmoduls.
Zu den wichtigsten Neuerungen gehören:

- Ein Verhalten, um einen Gegenstand einzufangen
- Ein Verhalten, um den Klappenservo zu kontrollieren
- Code zum Umgang mit MMC- und SD-Speicherkarten
- Kommunikation jetzt per Default mit 57600 Baud
- Mini-Speichermanager für den bequemen Zugriff auf Speicherkarten
- Mini-Fat Dateisystem für Speicherkarten
- Erweiterung der Kartographieroutinen auf dem Bot
- Remote-calls um von außen Verhalten auf dem Bot anzusprechen

Über weitere Details gibt die Changelog-Datei im Code Aufschluss.

**08.01.2006** Mit dem Erweiterungsmodul lernt der Bot nun auch die Kommunikation per LAN und WLAN.
Des Weiteren lässt sich der Speicher des Bots nun über MMC- oder SD-Karten stark erweitern.
Eine Klappe kann das Transportfach verriegeln.
Dazu kommen noch diverse Erweiterungen des Source-Codes für den Mikrocontroller.
Der überarbeitete c't-Sim kommuniziert nun einerseits wieder per USB-2-Bot mit dem Roboter, kann aber auch per LAN und WLAn die Statusinformationen von einem echten Bot empfangen.
Eine Erweiterung im Kommunikationsprotokoll schafft die Grundlagen um dem c't-Bot auch aus der Ferne komplexe Aufgaben zu übermitteln.

**24.11.2006** In der Linkliste finden sich nun auch Einträge auf Seiten von Lesern sowie einige Videos zum Bot.
Wer seine Seite dort vermisst, schickt uns einfach eine kurze Mail und wir nehmen sie gerne dort auf.

**06.11.2006** Alle Verhalten aus bot-logic.c haben nun eigene Dateien erhalten, sodass das Framework nun deutlich übersichtlicher ist.
Des Weiteren haben wir eine Referenzimplementation des Kartographiealgorithmus mit in den c't-Bot-Code gepackt.

**13.10.2006** Der c't-Sim-Wettbewerb wird ab dem 18.10.2006 live online ausgetragen.
Detailliertere Informationen zum Spielplan veröffentlichen wir kurz vorher.
Wie alles andere wird der Spielplan direkt über den eigenen Bereich in der zusätzlichen Navigation rechts zu erreichen sein, welche wir der inzwischen ziemlich umfangreichen Webseite zusammen mit einigen Aktualisierungen spendiert haben.

**18.09.2006** Der IRC-Kanal zum c't-Bot ist umgezogen und nun wie folgt erreichbar: Server: pizza.de.eu.blitzed.org, Port: 6667 Kanal: #ct-bot _(IRC-Kanal nicht mehr verfügbar)_

**08.09.2006** Die Anmeldefrist für den c't-Sim-Wettbewerb ist verstrichen.
Insgesamt haben sich über 100 Teilnehmer und Teams haben sich angemeldet!

Zum Anmeldeschluss wurde die bereits vor längerer Zeit im Forum diskutierte Änderung im Wettbewerbsablauf in die Wettbewerbsbedingungen aufgenommen:
Das Turnier wird jetzt in zwei Phasen abgewickelt.
Zunächst wird in einer Vorrunde jeder Bot einzeln durch einen Parcours geschickt und die benötigte Zeit gestoppt, was eine Rangliste ergibt.

In der Hauptphase kommt dann das K.o.-System zum Einsatz, d.h. dass sich jeweils der Gewinner eines Duells für das nächste qualifiziert.
Nur unter den vier besten werden alle Plätze ausgespielt.
Die Rangliste aus der Vorrunde ermöglicht Ausgewogenheit im Turnierplan der Hauptphase:
Die Spieler werden so platziert, dass sich der schnellste und der zweitschnellste Bot aus der Vorrunde erst im Finale begegnen können, der schnellste und der drittschnellste Bot erst im Halbfinale usw.
So werden allzu verzerrte Wettbewerbsergebnisse vermieden - gäbe es z.B. eine einfache Auslosung statt einer Vorrunde, könnten zufällig die beiden besten Implementierungen in der ersten Runde aufeinandertreffen.
Das würde heißen, dass einer der beiden Schnellsten Bots schon im ersten Durchgang ausscheidet, was seine tatsächliche Stärke verfälscht widerspiegelt.
Die Vorrunde soll das vermeiden und helfen, die Spannung bis zuletzt aufrechtzuerhalten.

Für die Hauptphase gilt: Treten nicht genügend Teams an, um alle Zweikämpfe des ersten Durchgangs zu füllen, erhalten möglichst viele Bots ein Freilos, das sie automatisch für die nächste Runde qualifiziert.
Im Extremfall findet somit in der ersten Runde des Turniers nur ein einziges Duell statt - dafür sind alle anschließenden Durchgänge voll besetzt.

Gleichzeitig mit dem Anmeldeschluss erfolgt der Feature Freeze an der Wettbewerbsversion des c't-Sim.
Einige besondere Eigenheiten des Simulators sollen an dieser Stelle noch einmal hervorgehoben werden:

- Der Simulator schickt bei Start eines Duells an beide Bots auf den Startfeldern jeweils das Fernbedienungssignal "5".
Das wird auch im Wettbewerb der Fall sein.
Die Referenzimplementierung aus dem CVS aktiviert auf dieses Signal hin das Wandfolgeverhalten.
Dieses kann man für den Wettbewerb durch einen eigenen Algorithmus ersetzen.
Alternativ kann Ihr Bot auch Signale der Fernbedienung ignorieren und einfach sofort bei Erzeugung im Simulator das von Ihnen programmierte Verhalten starten, das den virtuellen Roboter möglichst schnell durchs Labyrinth bringen soll.

- Das Licht von den vier Eckleuchten im Parcours hat eine Tragweite von einem Meter, was etwa 4 Rasterfeldern des Labyrinths entspricht.
Der Messwert der "Lichtsensoren" steigt linear mit abnehmender Entfernung zur nächsten Lichtquelle im Sichtbereich an.
Befinden sich zwei Lichtquellen im Sichtbereich, wird die weiter entfernte komplett ignoriert.
Die Sensoren haben einen Öffnungswinkel von 180 Grad und "schauen" auch durch Wände hindurch.

- Die Implementierung des Wandfolgers im CVS vermeidet keine Löcher.
Enthält ein Parcours auf dem Weg an der Wand entlang Fallgruben, erreicht unsere Referenzimplementierung ihr Ziel nicht.

**01.09.2006** Nur noch eine Woche bis zum Anmeldeschluss des c't-Sim-Wettbewerbs!
Nähere Informationen gibt es auf der Wettbewerbsseite.
Seinen Steuercode für den virtuellen Bot kann man noch bis zum 6. Oktober auf den c't-Server hochladen.

**29.08.2006** Einige Bugfixes sind in den letzten Tagen zum c't-Bot-Code hinzugekommen.
Wir raten daher allen Nutzern, die aktuelle Version auszuchecken.

**15.08.2006** Es steht ein neues Release von ct-Bot und ct-Sim im CVS zur Verfügung, welche identisch in den Versionen sind, die mit 'HEAD' und 'Wettbewerb' markiert sind.
Zahlreiche Eigenheiten und Bugs des Sim sollten damit behoben sein.
Details entnehmen Sie bitte dem Changelog.
Der Sim hat deutlich an Performance gewonnen und ist jetzt wieder mit detaillierteren Anzeigen und der lange vermissten Fernbedienung ausgestattet.
Die im Forum diskutierte Möglichkeit, den realistischen Kennlinien der Sensoren auf Seiten des Bot mit einem einfachen lookup-table zu begegnen, wird (leider ?) nicht mehr funktionieren.
In der neuen Version des Sim extrapolieren die Sensoren jedoch auch beliebige Zwischenwerte.
Im Wettbewerb muss der Steuercode des Bot also mit zweideutigen Werten umgehen können.

**20.07.2006** Achim Pankalla, Peter Jonas und Frank Menzel haben weitere Patches für den c't-Bot beigesteuert, die unter anderem auch simulierte Bots mit einem virtuellen EEPROM zur Kalibrierung der Distanzsensoren ausstatten.

**18.07.2006** Christian Isensee hat einen Fehler im Simulator gefunden und per Patch behoben:
Versehentlich wurden den Distanzsensoren des Bot - rechts wie links - der gleiche Abstandswert übergeben, welcher eigentlich nur für den linken Sensor gedacht war.
Das CVS enthält jetzt die korrigierte Version; wir bitten um Entschuldigung für diesen Fehler.

In diversen Foren-Threads wurden Stimmen laut, die zu bedenken gaben, dass beim K.o.-System im Wettbewerb die Gefahr besteht, dass "gute" Bots zu früh ausscheiden und "schlechte" weit kommen können.
Aus verschiedenen bereits diskutierten Gründen möchten wir weiterhin an dem gewählten Ausscheidungssystem festhalten.
Wir haben aber über die Anregungen unserer Leser nachgedacht und wollen daher eine Ergänzung des Systems wie folgt vornehmen:
Statt der ursprünglichen geplanten zufälligen Einsortierung in den Spielbaum des K.o.-Systems muss nun jeder Bot im Vorfeld des eigentlichen Wettbewerbs ein unbekanntes Qualifikationslabyrinth durchqueren.
In diesem starten die Bots einzeln und der c't-Sim stoppt die Zeit, die der Bot vom Start zum Ziel braucht.
Auch hier kann es, wie später in den Ausscheidungsrunden, zu einem Timeout kommen, wenn der Bot zu lange braucht.
Anhand der Ergebnisse dieser Vorrunde erfolgt dann die Verteilung der Bots in den eigentlichen Spielbaum:
Alle Bots werden so auf die Matches verteilt, dass sich der nach der Qualifikation schnellste und zweitschnellste Bot erst im Finale begegnen können.
Der erste/zweite Bot kann auf den dritten/vierten Bot erst im Halbfinale treffen.
Die eventuell vorhanden Freilose gehen an die Bots mit den kürzesten Zeiten.
Die restlichen Bots treten in solchen Paarungen gegeneinader an, dass zwischen zwei Konkurrenten in der ersten Runde immer gleich viele Plätze liegen.
Auch bei diesem Modus kann man natürlich mal Pech mit dem Labyrinth und/oder dem Gegner haben, aber dieses Risiko gehört zu solchen Wettbewerben dazu und macht das Turnier spannend.
Guter Robotercode zeichnet sich unter anderem dadurch aus, dass er mit vielen verschiedenen Randbedingungen klarkommt.

**07.07.2006** Die Redaktion schreibt das erste virtuelle Bot-Turnier aus!
Wer dort siegen will, muss im c't-Sim einen flotten Weg durch unbekanntes Gelände finden.
Einen realen Roboter braucht man nicht für die Teilnahme - den gibt es zu gewinnen.
Die Anmeldung läuft bis zum 8. September, ausgefochten wird der Wettkampf in der Woche vom 16. bis 20. Oktober.
Der Roboterwettbewerb der c't findet im Rahmen des Informatikjahrs statt.

Im Zuge der Wettbewerbsvorbereitung wurde der c't-Sim gründlich überarbeitet und mit einer neuen grafischen Oberfläche versehen.
Seinen virtuellen c't-Bot muss aber niemand komplett umprogrammieren - an den Schnittstellen zwischen Java- und C-Teil des Simulators hat sich wenig geändert, mit einer Ausnahme:
Die Distanzsensoren der neuen Version des c't-Sim besitzen Kennlinien, die an jene der GP2D12-Sensoren beim realen Bot angenähert sind.
Dadurch fallen Entfernungsmessungen möglicherweise zweideutig aus.
Details hierzu beschreibt der aktuelle c't-Artikel zum c't-Bot-Projekt.

Derzeit ist der aktuelle Code von c't-Bot und c't-Sim identisch mit den Programmversionen, die im Wettbewerb zum Einsatz kommen.
Wie man später gezielt von den Entwicklerversionen des Codes zu den Turniervarianten wechseln kann, beschreibt ein gesonderter Abschnitt der Installationsanleitung.
Die neuesten Versionen von c't-Bot und c't-Sim sind aktuell nur über das CVS erhältlich - fertige ausführbare Dateien und Zip-Archive mit dem Code werden in Kürze auf dieser Seite veröffentlicht.

**28.06.2006:** Achim Pankalla hat einen Patch eingereicht, der für realitätsnahe Messwerte bei den Abstandssensoren im c't-Sim sorgt.
Ein weiterer Patch sorgt dafür, dass der simulierte Bot mit Sensordaten dieser Art umgehen kann.

**14.06.2006** Torsten Evers hat einen Patch beigesteuert, der im Display auf Screen 5 den noch freien Arbeitsspeicher des Mikrocontrollers anzeigt (nur für Target MCU).

**10.06.2006** Der c't-Bot-Artikel in der c't 13/06 zeigt, wie man den Maussensor auswertet und aus seinen Daten eine Position errechnet.
Der Code im CVS-Archiv kennt nun auch eine Funktion _bot_gotoxy()_, die eine genaue Position anfährt.
Die ausgewerteten Daten der Sensoren und die Position stehen als globale Variablen zur Verfügung.
Ein überarbeitere Hardware-Modifikation beschreibt, wie man den Maussensor optimal montiert.
Des Weiteren hat der Linienfolger von Torsten Evers Einzug in den offiziellen Code gehalten.

**27.05.2006** Die RX/TX-Bibliothek für serielle Kommunikation erlaubt dem c't-Sim nun, über beliebige serielle Adapter mit dem realen Bot zu kommunizieren.

**22.05.2006** Die Roadmap ist wieder aktuell.

**19.05.2006:** Eine zusätzliche Hardware-Modifikation beschreibt, wie man Einstreuungen auf der seriellen Schnittstelle vermeidet.
Spendiert man den Abstandssensoren zusätzlich zu den schon vorgestellten Pufferkondensatoren noch jeweils einen großen Elko, verbessert das die Messgenauigkeit.

**13.05.2006** Der c't-Sim-Artikel in der c't 11/06 beschreibt, wie man eigene Welten für die Bots baut.
Außerdem können sich nun auch Zuschauer über das Internet auf einem c't-Sim einloggen und den Bots beim Rennen zuschauen.
Für die Verfeinerung der ClientViews brauchen wir noch tatkräftige Unterstützung.
Das Netzwerkprotokoll dürfte noch etwas Tuning vertragen und auch die Anzeige ist noch spartanisch.

**02.05.2006** In der FAQ gibt es nun auch ein paar Tipps zum Einstieg in die Programmierung eigener Verhalten.
Segor hat nun auch eine zum Bot passende RC5-Infrarotfernbedienung im Angebot, die wir demnächst als Standardmodell auch im c't-Sim nachbauen werden.

**29.04.2006** Passend zum Tutorial in c't 10/06 steht nun auch der Code zum Durchqueren eines Labyrinthes bereit.
Der c't-Sim hat diverse interne Änderungen erfahren. Details dazu stehen im Changelog und werden ausführlich Thema in der c't 11/06 sein.
So ist unter anderem die Möglichkeit neu, simulierte C-Bots per Knopfdruck zu starten, oder das Bild des Maussensors von einem realen Bot auszulesen und darzustellen.

**25.04.2006** Die Aufbauanleitung enthält nun auch Fotos der LEDs.
In der FAQ und der Link-Liste gibt es nun ein paar Tipps zur Netikette.
Im CVS befindet sich mittlerweile auch eine Batch-Datei zum Flashen mit dem STK200 unter Windows und es sind wieder ein paar neue Fernbedienungsdefinitionen hinzugekommen.

**21.04.2006** Auf der Patchsseite ist eine Code-Erweiterung von Carsten Giesen zu finden, die den c't-Sim mit allen Tasten der Fernbedienung Hauppauge MediaMPV ausstattet.

**13.04.2006** Mit der Drehzahlregelung fährt der c't-Bot nun mit definierten Geschwindigkeit in mm/s, die er auch ziemlich genau einhält.
Damit drehen sich die Motoren ebenfalls annähernd gleich, was den Geradeauslauf stark verbessert.

**11.04.2006** Dank Andreas Merkle zeigt der c't-Sim die Log-Ausgaben des Roboters in einem eigenen Log-Fenster an.
Es gibt nun eine Checkliste zum Einreichen eigener Patches.
In der FAQ gibt es neuerdings einen Tipp zum SMD-Löten.

**10.04.2006** Die Roadmap ist wieder aktuell.

**05.04.2006** Segor bietet nun auch die von Viktor Dirks entworfenen Rad-Encoder-Scheiben an.
Wer seinen Bot bereits erhalten hat, findet unter http://www.segor.de/L1Bausaetze/ct-robot.shtml _(Link nicht mehr verfügbar)_ Informationen, wie er günstig an seine Scheiben kommt.
Es gibt jetzt eine Aufbauanleitung für den USB-2-Bot-Adapter.
Des Weiteren stehen alle bisherigen c't-Bot-Artikel nun auch online in HTML-Form zur Verfügung.
Darüber hinaus haben wir eine neue Seite mit Code-Richtlinien für eigene Erweiterungen erstellt.
Ein neuer Patch von Johannes Dörnte ermöglicht es, im Simulator zwischen zwei Welten umzuschalten.

**04.04.2006** Eine ganze Reihe von Leser-Patches hat Eingang ins CVS gefunden.
Zu den deutlichsten Änderungen gehört der Patch von Carsten Giesen und Frank Menzel, der es erlaubt einzelne Verhalten per Fernbedienung zu aktivieren.
Außerdem gibt es jetzt ein Unterverzeichnis Documentation.
Dort liegt bereits eine erste Datei, die die Bedienung der oben genannten Features beschreibt.
In Zukunft würden wir hier gerne lieber HTML- als TXT-Content sehen.
Doku-Patches nehmen wir genauso gerne entgegen wie Code-Patches.

**21.03.2006** Dank eines Patches von Markus Lang zeigt der c't-Sim das Kontrollfenster und den Blick auf die Roboterwelt jetzt in einem gemeinsamen Rahmen (SplitPane) an.

**20.03.2006** Dank Michail Brzitwa kann man nun mehrere Fernbedienungen erfassen und muss nur noch per #define-Schalter eine Bedienung auswählen.
Patches mit weiteren RC5-Codes nehmen wir gerne entgegen.
Der reale c't-Bot nimmt nun auch Fernbedienungs-Kommandos vom c't-Sim an.
Der simulierte Bot erkennt nun auch den Maussensor.

**17.03.2006** c't-Bots trainieren jetzt Slalomfahrten – ganz ohne vorher wissen zu müssen, wie der Kurs sich drehen und wenden wird.
Am Beispiel dieser Aufgabe zeigt der neue Code für den c't-Bot, wie sich komplexes Verhalten in Anlehnung an das Subsumptionsprinzip des Robotik-Pioniers Rodney Brooks realisieren lässt.
An vielen Stellen und Parametern im Programm lässt sich noch herumschrauben, um das Verhalten des Bot weiter auszufeilen und an den eigenen echten c't-Bot anzupassen.
In den Kommentaren zum Code finden sich an einigen Stellen Hinweise darauf, wo es sich anbietet, Verhaltensweisen zu erweitern und zu verbessern.
Der Sourcecode steht wie immer im CVS und als ZIP-Verzeichnis zum Download bereit.
Auch der **Simulator** hat sich in wichtigen Details verändert, er liegt jetzt in **Version 0.3** vor und ist für den Einsatz der neuen USB-2-Bot-Verbindung (Artikel dazu in der c't 7/06) gerüstet.
Weitere Änderungen betreffen die innere Struktur des Simulators und die Modellierung des Bot:
So arbeiteten die vorigen Versionen des c't-Sim versehentlich mit der Zahl von 40 Encoder-Markierungen pro Radumdrehung.
In der Realität sind es dagegen 30 helle und 30 dunkle Felder, also 60 Wechsel pro Rotation.

**WICHTIG**: Der c't-Sim verwendet jetzt Konstrukte aus dem **Java-Standard 5.0** - Voraussetzung für den Betrieb ist also ein JDK, das diese Java-Version unterstützt.
In der Entwicklungsumgebung Eclipse muss zusätzlich im Menü Window/Preferences unter Java/Compiler/JDK Compliance die Standardeinstellung 1.4 auf 5.0 umgeschaltet werden.
Für den c't-Sim gibt es jetzt im CVS eine öffentlich zugängliche ToDo-Liste.

**10.03.2006** Für alle, die am Code von c't-Bot oder c't-Sim entwickeln, haben wir eine Mailingliste eröffnet.
An diese kann man sich auch mit Patches oder Problemen wenden.
Unter anderem soll diese Liste dazu dienen Patches mit einer breiteren Gruppe von Entwicklern zu diskutieren, bevor sie ins CVS einfließen.

**09.03.2006** Andreas Merkle hat den c't-Bot um diverse Logging-Funktionen erweitert.
Auch das Ausgeben von Strings auf das Display ist nun deutlich komfortabler.

**08.03.2006** Wir haben eine eigene Seite für Hardware-Modifikationen eingerichtet.
Dort sammeln wir sinnvolle Veränderungen am c't-Bot sowie Problemlösungen für widerspenstige Bots.

**04.03.2006** Im Forum und in der c't 06/06 haben wir es bereits angekündigt:
Auf der CeBIT werden wir dem c't-Bot eine kleine Veranstaltung widmen.
Am Samstag den 11.03.2006 sind ab 17:00 Uhr alle Interessierten herzlich eingeladen, sich mit uns am Heise-Stand zu treffen.
Nach einer kleinen Einführung in das Projekt wollen wir über Programmierung, Hardware-Erweiterungen, Einsatzmöglichkeiten virtueller und realer Roboter und vieles mehr mit Ihnen diskutieren.

**03.03.2006** Wie in der c't 06/06 beschrieben geht der c't-Bot nun sparsamer mit den Akkus um und linearisiert die Werte der Abstandssensoren.

**01.03.2006** Der c't-Bot kann nun alle Sensor- und Aktuatordaten per serieller Schnittstelle an den PC übertragen.
Eine geeignete Adapterschaltung (TTL-UART auf USB) werden wir voraussichtlich in einer der kommenden Ausgaben von c't vorstellen.
Die FAQ haben wir ebenfalls erweitert.

**28.02.2006** Um Messungen von Geschwindigkeiten zu ermöglichen, haben wir globale Zeitvariablen in den Code hinzugefügt.
Wir nutzen sie zum Beispiel für die neue Geschwindigkeitsmessung.
Für den c't-Bot-Code gibt es im CVS nun eine öffentlich zugängliche ToDo-Liste.
Alle Anpassungen des Roboters bzw. seines Verhaltenssystems sind nun in bot-local.h gesammelt.
Dort kann man sie per .cvsignore besser schützen.

**27.02.2006** Im CVS steht eine aktualisierte Firmware:
Dank Markus Hennecke kann man jetzt dem c't-Bot auf der Kommandozeile die IP-Adresse des Simualtors übergeben.
Torsten Evers hat sich des Linux-Flash-Skriptes angenommen.
Es prüft nun die Fuse-Bits vor dem Schreiben.
Außerdem gibt es eine neue Variable, die die letzte Drehrichtung des Motors speichert sowie ein wenig mehr Infos in sensor.h.

**23.02.2006** Es gibt ein neues Testprogramm im Download-Bereich und eine Erklärung dazu bei den FAQs.
Wir haben die Motordrehrichtung im Code jetzt so verändert, dass sie zur Aufbauanleitung passt.
Des Weiteren haben wir den Endian-Patch von Ansgar Esztermann und Markus Hennecke aufgenommen.
c't-Bots auf Macs, Sparcs, usw. sollten nun auch mit dem c't-Sim kommunizieren können.
Ein weiterer Leser-Patch findet sich auf der Patch-Seite.
Ein neuer Schaltplan der Maussensorplatine zeigt nun den selben Wert für R5 wie die Stückliste.

**22.02.2006** Carsten Giesen hat einen Patch beigesteuert, mit dem sich der Inhalt des Reset-Registers auf dem Display anzeigen lässt.
Im Schaltplan war der Widerstandswert von R6 fälschlicherweise mit 4k7 angegeben.
47k, so wie es in der Stückliste steht, ist hingegen korrekt.
Eine korrigierte Version des Schaltplans ist online verfügbar.

**21.02.2006** Wir haben eine eigene Seite für Code-Patches von Lesern zum Download eingerichtet.
Dort findet sich bereits eine Programmverfeinerung von Fabian Recktenwald für den c't-Sim.
Damit bestimmt der Simulator die neue Position eines Bot geometrisch korrekt und nicht, so wie bisher, lediglich in ausreichender Näherung.
Im CVS finden sich dank Torsten Evers jetzt auch Linux-Skripte zum Flashen und Fusen des Mikrocontrollers.

**20.02.2006** Weitere Leser-Patches haben Eingang ins CVS gefunden.
Rolf Ebert steuerte die Möglichkeit bei, das Display des Bot auch remote im Simulator anzuzeigen.
Andreas Staudenmayer hat Windows-Batch-Files zum Flashen und Setzen der Fuse-Bits eingeschickt.
Von Carsten Giesen stammt die Erweiterung, zwischen mehreren Display-Screens umschalten zu können.
Dank Fabian Recktenwald konnten wir einen kleinen Bug im Goto-System beheben.
Viele Lösungen für Probleme, die in den letzten Tagen im Forum auftauchten, haben wir in der FAQ gesammelt.

**18.02.2006** **Version 0.2** des c't-Sim ist da!
Der Simulator kommt jetzt mit mehreren virtuellen Robotern gleichzeitig klar, die sich gegenseitig als Hindernisse erkennen.
Die simulierten Bots verfügen über neue Sensoren, um Licht, Linien, Abgründe oder die eigene Bewegung über Grund zu erkennen.
Damit diese Sinne auch alle gefordert werden, enthält die Welt mehr Hindernisse als bisher - hinzugekommen sind Lampen, Linien und ein Loch im Boden.
Der Code für den c't-Sim und den c't-Bot ist wie immer im CVS erhältlich, vorkompilierte ausführbare Dateien gibt es auch auch als ZIP-Datei.

**WICHTIG**: Kommende Versionen des c't-Sim werden Methoden benutzen, die erst ab **Java 5.0** verfügbar sind.
Meldet Eclipse für den neuen Code Kompilierfehler, ist zu prüfen, ob die Java-Version innerhalb der Entwicklungsumgebung richtig gesetzt ist.
Für Eclipse muss im Menü Window/Preferences bei Java/Compiler/JDK Compliance die Version 5.0 eingeschaltet sein.

**13.02.2006** Eine korrigierte Aufbauanleitung, aktuelle Schalt- und Bestückungspläne sowie eine überarbeitete Stückliste sind online verfügbar.

**04.02.2006** Ab dem 06.02.2006 ist der c't-Bot verfügbar. eMedia bietet einen Platinensatz an, Segor Electronics des Weiteren alle Bauteile sowie die Mechanik.
Der c't-Bot-Code ist nun um die Mikrocontroller-Routinen erweitert.
Die neueste Version findet sich wie immer im CVS, einige vorkompilierte Testprogramme gibt es auch auch als ZIP-Datei.

**26.01.2006** Der erste von einem Leser eingesandte Patch für den c't-Sim hat Eingang in die offizielle Codebasis gefunden.
Der Simulator kann jetzt mittels eines neuen Schiebereglers auch in Zeitlupe betrieben werden. Die neueste Version des Codes ist im CVS erhältlich.

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Benjamin Benz, Hendrik Krauß, Timo Sandmann, Nightwalker-87
