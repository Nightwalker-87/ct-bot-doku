**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# EEPROM Emulation für PC

> **Trac-2-Markdown Konvertierung:** *deprecated*

<p style="margin-bottom: 0cm; font-family: Times New Roman;" align="center"><font size="+1"><b>EEPROM Emulation für
PC</b></font></p>

<p style="margin-bottom: 0cm; text-align: center;"><font size="3"><b><small>Version 1.1 17-Sep-2007</small></b><br>

Achim Pankalla
(achim.pankalla@gmx.de)</font></p>

<p style="margin-bottom: 0cm; height: 0px;"><br>
</p>
<p style="margin-bottom: 0cm; font-style: normal; text-align: justify;"></p>

<div style="text-align: center;"><b>Beschreibung</b><br>
<div style="text-align: justify;">Die
EEPROM Emulation für den PC stellt das EEPROM des <i>Atmel
MEGA32(644) Prozessors</i> auch dem ct-Sim zur Verfügung.
Der Zugriff auf dieses EEPROM erfolgt über gleichnamige
Funktionen, wie sie auch die avr-libc bereitstellt und auch die
Variablendefinition erfolgt über die gleichen Konstrukte. Eine
Unterscheidung über <span style="font-style: italic;">#ifdef</span>'s ist also nicht notwendig.<br>

Durch
diese EEPROM-Emulation ist der ct-Sim dem realen Bot einen Schritt
näher gekommen und Programme mit EEPROM-Zugriffe können mit
der Simulation getestet werden. Mehr noch, Sie können auch den
Inhalt des emulierten EEPROM auf den ct-Bot übertragen oder das
EEPROM vom
ct-Bot laden und für die Emulation nutzen.</div>
</div>

<p style="margin-bottom: 0cm;" align="left"><br>
</p>

<p style="margin-bottom: 0cm; text-align: center;"><b>Implementierung</b><br>
</p>

<div style="text-align: justify;">Alle Funktionen und Einstellungen der
EEPROM Emulation findet Sie in den Dateien <i>pc/eeprom-emu_pc.c</i>
und <i>include/eeprom-emu.h</i>. Das EEPROM selbst wird durch eine
binäre Datei (genau 1 KB bzw. 2 KB groß) repräsentiert&nbsp;und
kann so mit einen HexEditor bearbeitet werden. Der Pfad mit Dateinamen befindet sich in den
Konstanten MCU_(PC_)<span style="font-style: italic;">EEPROM_FN</span> in der C-Datei. Standard Pfad ist das Heimatverzeichnis des
ct-Bots.&nbsp;<font face="Times New Roman, serif"></font><br>

Die
Datei wird automatisch neu angelegt, wenn sie noch nicht existiert,
dann wird die Datei automatisch mit den aktuellen Zuweisung der
EEPROM-Variablen initialisiert (mit Hilfe von ct-Bot.eep). Ist schon
eine <span style="font-style: italic;">eeprom.bin</span> vorhanden, so wird diese nicht verändert, ausser die ct-Bot.exe wird mit dem Parameter <span style="font-style: italic;">-i</span> gestartet, dann wird auch eine schon vorhandene Datei mit den vorhandenen Zuweisungen überschrieben.<br>

Damit die
EEPROM-Funktionen des PC korrekt auf die Datei zugreifen können
darf nur ein Adressraum von 0 bis 1023 (bzw. 2047) entstehen.&nbsp;Die
Emulation muss also wissen welche Speicheradresse die
erste Variable im EEPROM hat, um diesen Wert von allen anderen
abzuziehen. Dafür bedarf es bei
der PC Implementierung (mit PC ist allgemein der Code für den
ct-Sim gemeint, mag das OS nun Win, Linux oder Mac OS X heißen)
eines Tricks.&nbsp;<br>

Dafür gibt es die beiden Variablen
<i>_eeprom_start1__</i> und <i>_eeprom_start2_</i><span style="font-style: normal;">_
in </span><i>1st_init.S</i><span style="font-style: normal;">. Diese
stehen dort, damit sie auf jeden Fall vor der ersten EEPROM Variable
definiert werden und damit ihre Sections (.</span><i>s1eeprom</i> <span style="font-style: normal;">+
.</span><i>s2eeprom</i><span style="font-style: normal;">) auf jeden
Fall vor der Section .</span><i>eeprom</i> <span style="font-style: normal;">liegen.</span><br>

Durch diesen Trick
kann die Speicheradresse der ersten EEPROM Variable auch ohne
Linkerscript ermittelt werden und auch verschiedene
Section-Alignments (im Moment bei MinGW und Linux unterschiedlich)
haben keine Auswirkung.<br>

Auch beim
Generieren einer neuen Datei ct-Bot.exe/elf wird eine EEP mit den
Initialisierungen der EEPROM-Variablen im Post-Build angelegt. Diese
Datei kann&nbsp; die EEPROM-Emulation auch als Initialisierung für die <span style="font-style: italic;">eeprom.bin</span> im MCU-Modus benutzen. Sollte keine <span style="font-style: italic;">eeprom.bin</span> existieren, wird sie auch dafür genutzt. Arbeitet man im PC-Modus, kann diese Datei auch in eeprom.bin umbenannt werden.<br>

Damit die Emulation möglichst effektiv und schnell arbeiten kann, wird nach dem Start die gesamte Datei <span style="font-style: italic;">eeprom.bin</span> im Hauptspeicher gecached und nach jedem Schreibzugriff komplett neu geschrieben.<br>

Damit man die EEPROM-Datei auch auf den ct-Bot einspielen kann, oder
einen EEPROM Abzug &nbsp;des ct-Bot als emuliertes EEPROM nutzen kann,
werden Post-Builds benötigt, die die Adressen der einzelnen
Variablen auf ct-Bot und ct-Sim aufzeigen. Der EEPROM Manager wird beim
Start eines Bots im ct-Sim dann eine (Adress)Konvertierungstabelle
erstellen, um die Zugriffe auf das EEPROM anzupassen. Diese Tabelle
wird nach aufsteigenden Adressen des ct-Sim sortiert und nur im
MCU-Modus genutzt.</div>
<p style="margin-bottom: 0cm;"></p>

<div style="text-align: center;"><b>Nutzung der EEPROM Emulation</b><br>
<div style="text-align: justify;">Die EEPROM-Emulation unterscheidet
sich nur in ein paar Details von den Funktionen der avr-libc für den realen ct-Bot.
Natürlich hat der PC kein EEPROM, dieses wird durch
eine&nbsp;Datei im Binärformat emuliert. Der Dateinamen und der Pfad
wird über die Konstanten MCU_EEPROM_FN und PC_EEPROM_FN in <i>eeprom</i>-<i>emu</i>_<i>pc</i>.<i>c</i> festgelegt,
je nach Modus wird die entsprechende Datei angelegt. So kann man auch
am Dateinamen den Aufbau des EEPROMs erkennen. Wechselt der Modus, wird
die vorherige Datei gelöscht. Dadurch liegen immer die
initialsierten EEPROM-Variablen an der richtigen Stelle und ein
Fehlverhalten der Bots in der Simulation wird vermieden.<br>

Ein weiterer Unterschied ist, dass beim avr-gcc über
ein DEFINE der Prozessortyp festgelegt wird, entweder ATMega32 oder
ATMega644. Dieses DEFINE ist beim PC Compiler normalerweise nicht
gesetzt. Standardmäßig wird von einem ATMega32 mit
1024 Byte EEPROM ausgegangen, Die Emulation kennt aber die Konstante
für den ATMega644 und erhöht den EEPROM Speicher auf 2048
Bytes. Sollte schon eine 1 KB Datei fürs EEPROM bestehen, so muss
diese gelöscht werden, damit die Größere angelegt
wird. Wird direkt die erstellte <i>ct-bot.eep</i> Datei im PC-Modus genutzt, ist
dies natürlich nicht notwendig. <br>

Alle wichtigen Informationen werden
beim Start von ct-Bot.exe/elf im Log-Fenster angezeigt, vorrausgesetzt es ist in <span style="font-style: italic;">ct-bot.h</span> aktiviert ist (zusätzlich bitte in <span style="font-style: italic;">eeprom-emu_pc.c</span> die Konstante <span style="font-style: italic;">DEBUG_EEPROM</span>
aktivieren), dort sieht man
auch alle eventuellen Fehler, den erreichten Emulationsmodus und ob die
Emulation ordnungsgemäß
arbeiten kann. Es erfolgt kein Beenden bei
Problemen, die Funktion des EEPROMs ist dann aber nicht gegeben. Bei
Auffälligkeiten sollte man dann die LOG Funktion aktivieren.</div>
</div>

<p style="margin-bottom: 0cm;">Generell unterscheidet die Emulation
zwei Modi:</p>

<ol>
	<li>
    <p style="margin-bottom: 0cm;">PC-Modus<br>
In diesen Modus entspricht die
	<span style="font-style: italic;">eeprom.bin</span> nicht dem EEPROM des realen ct-Bots und darf deshalb auch
	nicht auf ihn aufgespielt werden. Dieser Modus wird ohne jedes Zutun erreicht.
	Er benötigt keine weiteren Einträge im Post-Build.&nbsp;Wenn eine <span style="font-style: italic;">ct-bot.eep</span> im Binärformat erstellt wird,
	so kann diese direkt benutzt werden.</p>
	</li>
  <li>
    <p style="margin-bottom: 0cm;">MCU-Modus<br>

Ist dieser Modus erreicht, kann man
	als EEPROM-Datei einen EEPROM Abzug vom ct-Bot verwenden.
	Voraussetzung ist natürlich, dass der Bot auch mit zuletzt
	erstelltem Programm bespielt ist. Natülich kann man auch die
	EEPROM-Datei <span style="font-style: italic;">eeprom.bin</span> auf dem ct-Bot aufgespielen.<br>

Der MCU-Modus kann nur erreicht
	werden, wenn sowohl beim avr-gcc als auch unter dem ct-Sim
	eine map-Datei erstellt wird, dafür müssen im Post-Build die Befehle aus dem Kommentarkopf aus <span style="font-style: italic;">eeprom-emu_pc.c</span> ausgeführt werden.</p>

In den Projekteinstellungen im SVN sind die nötigen Post-Build-Einstellungen für alle Betriebssysteme bereits gemacht.
	<br>
  </li>
</ol>

<p style="margin-bottom: 0cm; text-align: justify;">Möchte man die vorhandene EEPROM-Datei mit den Daten aus der EEP-Datei
initialisieren, so muss man die ct-Bot.exe/elf mit dem Parameter <i>-i
</i>starten, dabei spielt es keine Rolle in welchen Modus die
Emulation arbeitet. Der Pfad der EEP-Datei wird in der Konstante
<font color="#000000"><font face="Courier New, monospace"><font size="2">EEP_PC</font></font></font> und die Pfade für die MAP-Dateien werden in den Konstanten EEMAP_PC und EEMAP_MCU eingetragen.<br>

Die Variable MAX_VAR legt die Größe der Tabelle fest und
beschrängt damit die maximale Anzahl der Variablen. Sollte die
Fehlermeldung auftreten, dass es zu viele Variablen gibt, muss man
diesen Wert nur erhöhen. <br>
</p>

Für
das Debuggen von Zugriffen auf das EEPROM stehen unter anderem die
DEFINES LOG_STORE und LOG_LOAD zur Verfügung, die im MCU Modus
sogar den Variablennamen anzeigen. Andere Variationen sind auch noch
denkbar.
<p style="margin-bottom: 0cm;"></p>

<div style="text-align: center;"><b>Grenzen der
Implementierung</b><br>
<div style="text-align: justify;">Im Moment erstellen gleiche Compilerversionen (zu überprüfen
mit --version) auch (fast) gleiche EEPROM-Sections. Damit es
auch mit verschiedenen Compiler Version geht (und ich mich auch nicht
auf die gleichen Versionen verlasssen will) habe ich die
Adresskonvertierung eingeführt, damit dies kein Problem mehr
ist. Es gibt aber keine Garantien dafür, dass zukünftige Compiler
Versionen nicht die Reihenfolge der Variablen im Code ändern.
<span style="color: rgb(0, 0, 0);">Ein Einfügen neuer EEPROM Variablen kann auch zu Verschiebungen
der Adressen führen. Nach solchen änderungen (auch ein ändern der Compilerversion) ist man nur
auf der sicheren Seite, wenn das EEPROM initialisiert wird (sprich,
Sie Ihre alte </span><span style="font-style: italic; color: rgb(0, 0, 0);">eeprom.bin</span><span style="color: rgb(255, 0, 0);"><span style="color: rgb(0, 0, 0);"> bzw. auf dem Atmel das EEPROM löschen) und für MCU und ct-Sim neue Exe generiert werden</span>.</span>
Einmal erstellte Werte sind dann natürlich futsch. Wenn man den
Einfluss von Codeergänzungen kontrollieren will, kann man dies
vor und nach der änderung mit <span style="font-style: italic;">objdump</span> machen (oder falls Sie
die Befehle für die MAP-Dateien im Post-Build benutzen, schauen
Sie in die MAP-Dateien), mit den richtigen Parametern kann man sich
die Adressverteilung anzeigen lassen. Sie können dann sehen, ob
die neuen Variablen nun hinten angehängt wurden (dann brauch das
EEPROM nicht gelöscht werden) oder sie dazwischen gelandet sind
(dann sind die alten Daten unbrauchbar), dafür sollten sie aber
vorher in Eclipse <span style="font-style: italic;">Projekt-&gt;clean</span> aufrufen.<br>

Der Compiler kann aufgrund der Implementierung
des EEPROMs auf dem PC nicht kontrollieren, ob mehr als 1024/2048 Bytes
für die Variablen benötigt werden, er kennt diese Begrenzung
nicht. Der EEPROM-Manager meckert dann aber
im LOG. </div>
</div>

<p style="margin-bottom: 0cm;"></p>

<div style="text-align: center;"><span style="font-weight: bold;">Verschiedenes</span><br>
<div style="text-align: justify;">Ein besonderer Dank an dieser Stelle
an Timo Sandmann unter anderem für das Testen unter MacOSX und
für verschiedene Anpassungen, Optimierungen und für den
Assemblercode in 1st_init.S ohne den wohl ständige Probleme
unvermeidlich gewesen wären.<br>

Dank auch an alle anderen für konstruktive Kritik, die die
jetzige, ich denke annehmbare, Lösung erst möglich machte und
meiner Familie für ihre unendliche Geduld. <br>

Möge sich jeder eingeladen fühlen etwas zu verbessern oder erweitern.<br>
</div>
</div>

<p style="margin-bottom: 0cm;"><b>Funktionen</b><br>
init_eeprom_man() - Erledigt alle Arbeiten zur Aktivierung der EEPROM-Emulation<br>
</p>

<p style="margin-bottom: 0cm;"><b>Nur in eeprom-emu_pc.c sichtbare
Funktionen</b></p>
conv_eeaddr() - Wandelt PC Adresse in
ct-Bot Adresse<br>

create_ctab() - Erstellt
Adresskonvertierungstabelle<br>

check_eeprom_file() - Erstellt leeres
EEPROM, wenn nötig und initialisiert es, wenn gewünscht<br>

flush_eeprom_cache() - Schreibt veränderte Daten in eeprom.bin<br>

<p style="margin-bottom: 0cm;"><b>Zugriffsfunktionen für den PC
(identisch zu denen der avr-libc)</b><br>
eeprom_read_byte()<br>
eeprom_write_byte()<br>
eeprom_read_word()<br>
eeprom_write_word()<br>
eeprom_write_block()<br>
eeprom_read_block()</p>

<p style="margin-bottom: 0cm;"><b>Dateien</b><br></p>

<div style="text-align: center;">
<div style="text-align: left;">eeprom-emu.h - Headerdatei mit den Deklarationen<br>
eeprom-emu_pc.c - Implementierung der Funktionen
für ct-Bot &amp; ct-Sim<br>
1st_init.S - Sorgt für das korrekte Anlegen der Hilfsvariablen in der Exe</div>
</div>

Autor: Achim Pankalla
