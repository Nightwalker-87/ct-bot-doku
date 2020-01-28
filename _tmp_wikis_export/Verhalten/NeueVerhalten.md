**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Ideen und Diskussionen

## Für das Framework

*Derzeit kein Eintrag vorhanden.*

## Rund um neue [Verhalten](../Verhalten/Verhalten.md)

Die [Hardware](../ct-Bot-Hardware/ct-Bot-Hardware.md) des c't-Bots ist mittlerweile recht weit gediehen und auch das Framework sowie die Basisfunktionen stehen. An sinnvollen oder lustigen Verhalten mangelt es dem Bot jedoch noch. Hier ein paar Ideen und Anregungen, was man noch so alles mit dem Bot machen könnte. Fühlt Euch frei hier eigene Ideen Einzutragen, Pros und Contras zu sammeln oder Details der Implementierung zu beschreiben.

### Sumoringen

In der [Galerie](../Galerie/Galerie.md) Galerie findet sich bereits ein Video von zwei Bots beim [Sumoringen](http://youtube.com/watch?v=-AMo10Cc9L0). Der Code steht uns leider nicht zur Verfügung und er war vielleicht auch noch nicht ganz perfekt.

**Todo:**

* Regelwerk aufstellen
* Verhalten programmieren
* Sim anpassen
  * Bot-Bot-Kollisionen erkennen
  * Physik mit in die Simulation einbauen
    * Beeinflussung von Objekten untereinander (Stoß, schieben)
    * Widerstand beim Schieben (beim Bot abhängig von der Richtung)
    * Massenträgheit

**Contra:**

* Die realen c't-Bots sind an ihrer Front etwas sensibel, eigentlich will man sie nicht mit Full-Speed gegen ein Hidnerniss fahren lassen. Vielleicht einpacken in eine CD-Spindel und ein wenig polstern?
* Bei realen Bots braucht man immer zwei Stück
* Umbauten am Sim nötig

### Dosen sammeln

Man könnte in einem Labyrinth kleine Dosen verteilen, die der Bot dann suchen, aufnehmen und zu einem zentralen Punkt bringen muss.

**Pro:**

* [Teilverhalten](../Verhalten/Verhalten.md) bestehen schon, die man nutzen kann:
  * solve_maze() zum Durchfahren des Labyrinths
  * catch_pillar() zum Einfangen einer Dose im Nahbereich
  * map() legt eine Karte der Umgebung an
  * [bot_calc_wave()](../DokuPathplaning/DokuPathplaning.md) fährt einen Ort auf der Karte auf kürzestem Weg an
* Es entstehen neue Teilverhalten, die man für andere Dinge mit benutzen kann.

**Todo:**

* es bräuchte ein Explore Verhalten
* Sim um kleine bewegliche Objekte erweitern
* Sim um das Einfangen im Transportfach erweitern
  * Servo-Befehle auswerten
  * Klappe visualisieren
  * Transportfachsensor implementieren, um Dosen im Fach zu erkennen
    * Schritt 1: Genauere Kollisionserkennung. Momentan: Ganzer Bot kollidiert. Gewünscht: Unterscheiden, ob Transportfach (die 3 Innenwände vom Bot-Mund) kollidieren oder was von der restlichen Bot-Shape

### Weg freiräumen

Man könnte einen Parcours gestalten, bei dem der Weg zum vorher festzulegenden Zielpunkt durch diverse, einsammelbare Hindernisse ("Filmdosen") verstellt ist. Der Bot müsste den Weg dann freiräumen und anschließend zum Ziel fahren.

**Pro:**

* Verhalten bestehen zum Teil (catch_pillar(), unload_pillar(), map())
* Eignet sich gut, um die Genauigkeit der Sensorauswertung und damit der eigenen Kalibrierung zu prüfen, da der Bot viele Richtungsänderungen machen muss

**Todo:**

* Verhalten zum Erfassen von Hindernissen und Routing-Strategien
* Sim um kleine bewegliche Objekte erweitern
* Sim um das Einfangen im Transportfach erweitern
  * Servo-Befehle auswerten
  * Klappe visualisieren
  * Transportfachsensor implementieren, um Dosen im Fach zu erkennen
    * Schritt 1: Genauere Kollisionserkennung. Momentan: Ganzer Bot kollidiert. Gewünscht: Unterscheiden, ob Transportfach (die 3 Innenwände vom Bot-Mund) kollidieren oder was von der restlichen Bot-Shape

### Weitere Ideen

Ein paar weitere Ideen fanden auf der Mailingliste bereits [Erwähnung](http://www.heise.de/ct/newsletter/archiv/ct-bot-entwickler/msg11653.html).

## Zur Hardware

Siehe [Hardware-Erweiterungen](../ct-Bot-Hardware/ct-Bot-Hardware.md#Erweiterungen).
