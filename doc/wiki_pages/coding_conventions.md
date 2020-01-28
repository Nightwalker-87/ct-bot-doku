# Richtlinien für Erweiterungen am c't-Bot und c't-Sim (coding conventions)

Fremden Code lesen kann ganz schön anstrengend sein - ein Variablenname, der dem einen selbsterklärend vorkommt, kann auf den anderen kryptisch wirken. Wenn du einen Patch schreibst und deinen Code möglichst verständlich programmierst und dokumentierst, steigen die Chancen, dass andere c't-Bot-Fans von deiner Arbeit ebenfalls profitieren. Als Hilfe haben wir ein paar Richtlinien zusammengestellt, die für Übersicht im c't-Roboter-Projekt sorgen sollen.

Zugegeben: Bislang erfüllt die offizielle Codebasis diese Richtlinie ebenfalls (noch) nicht bis ins letzte Detail - wir arbeiten aber daran, das zu ändern. Deshalb kommen uns Patches von deiner Seite sehr entgegen, welche die aufgestellten Regeln einhalten.

Damit Patches für den Code möglichst kompatibel zueinander sind und überschaubar bleiben, sollten sie schlank sein. Faustregel: Ein Patch pro Thema. Insbesondere Formatierungsänderungen usw. blähen den Patch stark auf und machen ihn im Zweifelsfall inkompatibel zu anderen.

## Allgemeine Richtlinien

* Namen von Variablen, Konstanten, Funktionen und alles, was direkt mit dem Quellcode zu tun hat, sollten rein englisch sein.
* Kommentare und Dokumentation sollen dagegen auf Deutsch verfasst werden. Bitte benutzen Sie hierbei keine Umlaute und kein 'ß', da diese Zeichen von Windows, Linux, Mac, Solaris, usw. unterschiedlich gehandhabt werden - sie tauchen bald nur noch als Zeichensalat im Code auf.
* Variablen, die in c't-Bot und c't-Sim die gleichen Werte haben, sollten auch die gleichen Namen bekommen. Das macht vieles einfacher und vermeidet Verwechselungen.
* Alle Funktionen und Methoden sollen vollständig kommentiert werden. Hierzu gehört eine kurze Beschreibung, WAS die Funktion tut (aber nicht zwingend, WIE sie das tut), eine Erläuterung von Übergabeparametern und Rückgabewerten sowie der im Java-Teil unter Umständen geworfenen Exceptions. Bei trivialen Methoden wie Konstruktoren oder get()- und set()-Methoden kann die Kurzbeschreibung oft auch weggelassen werden.
* Die Kommentare zu Klassen, Funktionen und Methoden sollen [Doxygen-](http://www.stack.nl/~dimitri/doxygen/docblocks.html) beziehungsweise [Javadoc](http://java.sun.com/j2se/javadoc/writingdoccomments)-konform gestaltet werden - auf diese Weise kann man aus dem Code bequem durchsuchbare HTML-Seiten generieren.
* Bei allen Änderungen bitte Einträge in die jeweilige Changelog-Datei nicht vergessen. Hier sollte neben dem Datum der Änderung, Ihrem Namen und der E-Mail-Adresse noch ein kurzer Text stehen, der darstellt, inwiefern Ihre Erweiterung den Roboter oder den Simulator verbessert. Wird der Patch (vorerst) nicht ins offizielle Release übernommen, sondern separat auf der Projektseite veröffentlicht, sollte dieser Text auch als Beschreibung des Patches tauglich sein.
* Der komplette Code - und damit auch jede Erweiterung - steht unter der GPL. Daher müssen neu hinzugefügte Dateien auch einen GPL-Header besitzen.

## c't-Bot

* Bitte verwende NICHT den Datentyp int - PC und MCU interpretieren diesen verschieden! Stattdessen stehen die Typen `int8_t`, `uint8_t`, `int16_t`, `uint16_t`, `int32_t` und `uint32_t` zur Verfügung. Hierbei steht die angehängte Zahl für die Bits, die zum Speichern des Integer-Werts verwendet werden, das vorangestellte 'u' steht für 'unsigned', diese Typen speichern nur positive Werte. Bitte prüfe sorgfältig, in welchem Bereich die Werte deiner Variable liegen werden und wähle entsprechend einen passenden Datentyp.

    Die Wertebereiche liegen im Einzelnen bei:
    ```C
    int8_t zwischen -128 und 127
    uint8_t zwischen 0 und 255
    int16_t zwischen -32.768 und 32.767
    uint16_t zwischen 0 und 65.535
    int32_t zwischen -2.147.483.648 und 2.147.483.647
    uint32_t zwischen 0 und 4.294.967.295
    ```

  * Den Datentyp char sollte ebenfalls nur verwendet werden, wenn es sich wirklich um ein Zeichen handelt. Ansonsten verwende bitte ebenfalls `uint8_t` oder `int8_t`.
  * Bei Programmieren von Verhaltensweisen für das c't-Bot-Framework gilt folgende Konvention:
    * Verhaltensweisen (Behaviours), die vom Framework bearbeitet werden, heißen `bot_xxx_behaviour`.
    * Die Botenfunktionen, die solche Verhaltensweisen aufrufen und aktivieren, heißen `bot_xxx`. Beispiel: Die Botenfunktion `bot_drive_distance()` ruft die Verhaltensweise `bot_drive_distance_behaviour()` auf.

## c't-Sim

* Alle Variablen und Konstanten, die sich auf Sensoren beziehen, beginnen mit `sens` oder `SENS`, alle Aktuator-Wert mit `act`. Auch in Methoden, die mit den Sensoren oder Aktuatoren zu tun haben, finden sich die Bezeichner `sens` und `akt` wieder (`getSensBorderPosition()`).
* Bitte beachte beim Programmieren auch die üblichen [Java-Coding-Conventions](http://java.sun.com/docs/codeconv), etwa:
  * Methodennamen sollten aus Verben bestehen und mit einem kleinen Buchstaben beginnen. Bestehen Namen aus mehreren Wörtern, werden diese direkt hintereinander geschrieben, wobei alle außer dem ersten mit einem Großbuchstaben beginnen (`senseGroundReflectionCross()`).
  * Für Variablennamen gilt die gleiche Schreibweise wie für Methoden (vorne mit einem kleinen und im Inneren mit großen ersten Buchstaben). Variablennamen sollten kurz, aber verständlich sein (`lightBG` für die BranchGroup der Lichtquellen im c't-Sim).
  * Variablennamen aus einem einzelnen Buchstaben sind zu vermeiden, Ausnahme sind Zählervariablen, die beispielsweise nur innerhalb einer Schleife existieren (`for (int i=0; i<10; i++) {...}`).
  * Konstanten sollen in Großbuchstaben geschrieben werden, die einzelnen Wörter zusammengesetzter Bezeichner werden mit Unterstrichen getrennt (`LIGHT_SOURCE_REACH`).

* Hast du an einer Datei etwas verändert (beispielsweise eine neue Methode hinzugefügt), kannst du dich unter dem Dokumentationstext der gesamten Klasse über das Tag `@author` mit Namen und E-Mail-Adresse verewigen.

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Benjamin Benz, Timo Sandmann, Nightwalker-87
