**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Tricks, Tipps und Hotkeys für Eclipse

>> **Trac-2-Markdown Konvertierung:** *unchecked*

## Tastenkombinationen

| Aktion | Shortcut |
|--------|----------|
| Java-Klasse finden, und zwar extrem schnell | Strg-Shift-T (für __t__ype) |
|Beliebige Datei finden|Strg-Shift-R (für __r__esource)
|Member finden in einer Java-Datei|Strg-O (für __o__utline)
|Klasse unterm Cursor: Superklassen zeigen|Strg-T
|Klasse unterm Cursor: Subklassen zeigen|Strg-T zweimal drücken
|Vom Methodenaufruf zur Methodendefinition springen|F3 oder Strg-Klick
|Alle Stellen, wo die markierte Methode aufgerufen wird|Strg-Alt-H
|Details anzeigen an der Textcursor-Position (bei Methode: Javadoc, bei Fehler: Details)|F2
|Javadoc im Browser öffnen|Shift-F2
|Wort löschen (auch in javaTypischenNamen)|Strg-Backspace, Strg-Entf
|Zeile löschen|Strg-D (für __d__elete)
|Zeile eins nach oben / unten schieben|Alt-Hoch / -Runter
|Zeile kopieren|Strg-Alt-Hoch / -Runter
|Was man zuletzt laufen hatte starten|Strg-F11
|Was man zuletzt laufen hatte debuggen|F11
|Aktuelle Datei ausführen (Applikation, Applet, Ant-Datei, ...)|Alt-Shift-X (für e__x__ecute)
|Zu einem View springen (Package Explorer, Outline, ...)|Alt-Shift-Q
|Zum Editor springen|F12
|Tastenbelegung zeigen|Strg-Shift-L
|Blockauswahlmodus ein / aus|Alt+Shift+A / Option+Command+A

## Einstellungen

| Setting | Ort |
|---------|-----|
|CVS-Update-Fenster und Co. halten nicht mehr den Betrieb auf|*Window / Preferences / General / Always run in background*
|Tastenkombination: Im aktuellen Block Zeilenumbruch machen (ideal fürs Doku-Schreiben)|*Window / Preferences / General / Keys*, Modify, Category: Source, Name: Format Element (nicht zu verwechseln mit "Format", das formatiert die ganze Datei). Dann Key Sequence / Name auf die gewünschte Kombination (z.B. Strg-Shift-F) und *Add*.
|Quelltext der Java-Plattform-Klasse einbinden (manchmal hilft's, wenn man genau weiß was da vorgeht)|Im Package Explorer *JRE System Library* aufklappen, auf *rt.jar* rechte Maustaste / Properties. Als *Java Source Attachment* den Pfad zur *src.zip* wählen, die zum Lieferumfang des JDK zählt (bei Windows etwa `C:\Programme\Java\jdk1.5.0_08\src.zip`)

## Spezielles

1. Zeitspanne bis zum Erscheinen der Tooltips (diese zeigen z.B. Informationen über Variablen, Klassen usw. an, sobald sich der Mauszeiger über einem Bezeichner befindet) reduzieren (nur für *Eclipse 3.5 (Galileo) Cocoa* oder neuer unter macOS):
1. Im Terminal folgenden Befehl ausführen: `defaults write org.eclipse.eclipse NSInitialToolTipDelay -int 1000`
1. Eclipse neustarten

Die Zahl am Ende des Befehls gibt die Zeitspanne in ms an, der Standardwert beträgt 2000 (2 Sekunden).
