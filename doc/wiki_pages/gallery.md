# Bild- und Video-Gallerie: Der c't-Bot in Aktion

## Videos

Videos von eax:

* [Video](https://www.cety.de/ctbot/pfadplanung_real.html), welches die Verwendung der Pfadplanung auf dem echten Bot demonstriert. Der Kern der Sache in diesem Szenario liegt darin, dass der Rückweg zum Startpunkt nicht entlang der Wand erfolgt, also der Bereich zwischen den beiden Hindernisse gar nicht erst angefahren wird. Stand 19.04.2009.
* [Video](https://www.cety.de/ctbot/maptest_real.html) der Map-Anzeige (Map-2-Sim) des echten Bots. Die Anzeige der Map erfolgt in diesem Video noch mit relativ großer Verzögerung. Inzwischen ist der Code deutlich verbessert worden, wodurch die Verzögerung minimiert wurde. Stand 02.03.2009.
* [Video](https://www.cety.de/ctbot/follow_line_enh.html) des Verhaltens bot_follow_line_enh() auf dem echten Bot. Die Map dazu nach [einer](follow_line_enh.png) "Runde" und nach [zwei](follow_line_enh_2.png) "Runden". Stand 26.02.2009.
* [Video](https://www.cety.de/ctbot/drive_area_way_free.mov) zur Veranschaulichung von map_way_free(). Stand 15.02.2009
* [Video](https://www.cety.de/ctbot/map-2-sim.html) der ersten Map-2-Sim-Version in Aktion. Stand 27.11.2008
* [Video](https://www.cety.de/ctbot/follow_stack.html) des Verhaltens `bot_follow_object_behaviour()` im Zusammenspiel mit `bot_drive_stack()`. Stand 06.04.2008.
* [Video](https://www.cety.de/ctbot/solve_maze_real.html), das den echten Bot beim Lösen eines Labyrinths (folgen der Außenwand) zeigt. Der Lösungsalgorithmus ist mit Hilfe einer Skriptsprache umgesetzt (bot_abl_behaviour()). Stand 07.01.2008.
* [Video](https://www.cety.de/ctbot/wall.html) des Verhaltens `bot_follow_wall_behaviour()`. Stand 09.09.2007.
* [Video](https://www.cety.de/ctbot/follow.html) des Verhaltens `bot_follow_object_behaviour()`. Stand 03.08.2007.
* [Video](https://www.cety.de/ctbot/tevers_follow_line_wo_speedcontrol_cc-by-sa.avi) des Bots beim Linienverfolgen (`bot_follow_line_behaviour()`) ohne Motorregelung von Torsten Evers.
* [Video](https://www.cety.de/ctbot/tevers_follow_line_w_speedcontrol_cc-by-sa.avi) des Bots beim Linienverfolgen (`bot_follow_line_behaviour()`) mit Motorregelung von Torsten Evers.
* [Video](https://www.cety.de/ctbot/tevers_solve_maze_cc-by-sa.mpg) des c't-Bot beim Lösen eines kleinen Labyrinths mit `bot_solve_maze_behaviour()` von Torsten Evers.


## Bilder

* Karte zur Messung der Genauigkeit im ct-Sim.
Dargestellt ist eine fünfmalige Fahrt durch den Testparcours. Im Vergleich zur älteren Karte ist der Fehler hier sehr gering und nicht wachsend. (Datum: 17.08.2007):

![Image: 'map_accuracy.jpg'](../images/_gallery/map_accuracy.jpg)

* Eine Karte mit Testmuster bei der Fahrt durch ein Labyrinth.
Sie zeigt dank der Hilfslinien sehr gut den internen Aufbau der Karte in kleine quadratische Sections und riesige Macroblöcke. (Datum: 16.08.2007):

![Image: 'map_with_testpattern.jpg'](../images/_gallery/map_with_testpattern.jpg)

* Eine Karte, die zeigt, wo die Grenzen der Genauigkeit bei der Positionierung des Bots liegen.
Aufgenommen mit einem leicht modizierten Wandfolger (regelmäßige 360 Drehungen) im testparcours2.xml, in dem die Lampen und das Zielfeld entfernt wurden. (Datum: 06.04.2007):

![Image: 'map_borders.jpg'](../images/_gallery/map_borders.jpg)

* Eine Karte, die mit einem echten Bot auf einer MMC aufgezeichnet wurde.
Hier dreht sich ein Bot zwischen aufgestellten Büchern. (Datum: 23.03.2007):

![Image: 'map_real_bot.jpg'](../images/_gallery/map_real_bot.jpg)

* Zwei Karten die ein Bot beim Wandfolger-Verhalten aufgezeichnet hat (Datum: 23.03.2007):

| ![Image: 'map_follow_wall_01.jpg'](../images/_gallery/map_follow_wall_01.jpg) | ![Image: 'map_follow_wall_02.jpg'](../images/_gallery/map_follow_wall_02.jpg) |
| ---                                                                           | ---                                                                           |

* Zwei Karten die ein Bot beim Linienfolger-Verhalten aufgezeichnet hat:

| ![Image: 'map_follow_line_enh_01.jpg'](../images/_gallery/map_follow_line_enh_01.jpg) | ![Image: 'map_follow_line_enh_02.jpg'](../images/_gallery/map_follow_line_enh_02.jpg) |
| ---                                                                                   | ---                                                                                   |

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Benjamin Benz, Torsten Evers, Timo Sandmann, Morphi2k1, Nightwalker-87
