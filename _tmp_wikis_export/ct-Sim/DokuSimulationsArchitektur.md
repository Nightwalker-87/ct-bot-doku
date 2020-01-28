**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Dokumentation Simulationsarchitektur

>> **Trac-2-Markdown Konvertierung:** *unchecked*

## Überblick

```ascii
    Subsystem für Simulation
 ______________________________
/                              \


 World
    |


 MasterSimulator                              SimulatedBot
    |                                           |
    | hat                                       | hat
    |                                           |
    v                                           v
  Simulatoren-Liste:                          BotComponent-Liste:
                             beeinflusst
  Licht-Simulator links    -------------->    Lichtsensor links
                             beeinflusst
  Licht-Simulator rechts   -------------->    Lichtsensor rechts

                                              LCD

                                              Fehlersensor
                             beeinflusst
  Encoder-Simulator links  -------------->    Encoder links
                             beeinflusst
  Encoder-Simulator rechts -------------->    Encoder rechts

  ...                                         ...
```

## Wo kommen simulierte Werte her?

Am Beispiel des Lichtsensors -- die anderen Sensoren funktionieren ähnlich.

```ascii
                      run() (1x pro Sim-Schritt)
                        |
                        |
                        |
          fragt         v           aktualisiert                    .------> Gui
World  <--------- Licht-Simulator ---------------> Lichtsensor -----|
                                                                    '------> TCP zum C-Code
```

* World: Komplexe Klasse. Weiß, wo Lichtquellen, Wände usw. sind. Kann daher für den Licht-Simulator ausrechnen, wieviel Licht er sieht.
* Licht-Simulator: Kurze Klasse. Besteht aus dem Code, der den Lichtwert von der Welt holt und an den Sensor durchreicht. Der Lichtwert ist ein int zwischen 0 (Sensor sieht soviel Licht wie er messen kann) und 1023 (Sensor sieht kein Licht). Weiß seine Position (gemessen vom Bot-Zentrum) und seine Blickrichtung.
* Licht-Sensor: Kurze Klasse. Ist nur ein Int, der sich anzeigen kann (Gui) und der sich ins TCP schreiben kann.

**Warum die extra Simulatoren?** Die alten Licht-Sensoren haben sich selber ihre Lichtwerte von der World geholt. Im neuen Sim ist das aufgeteilt in Simulator und Sensor. Der Grund ist, dass das Applet auch Sensoren braucht, aber keine Abhängigkeit zu Java 3D haben soll (J3D ist nötig fürs Berechnen der Lichtwerte). Mit dem neuen Ansatz kann das Applet einfach die Simulatoren nicht erzeugen und fertig.

**Code** des Licht-Simulators (etwas vereinfacht):

```java
private final Point3d distFromBotCenter = ...;
private final Vector3d headingInBotCoord = ...;
private final double OPENING_ANGLE_IN_RAD = 180°;

public void run() {
    lightSensor.set( // Setze Lichtsensor auf ...
        world.sensLight( // ... Helligkeit, die auf einen Sensor fällt
            distFromBotCenter, // Wo sitzt der Sensor?
            headingInBotCoord, // Wohin schaut der Sensor?
            OPENING_ANGLE_IN_RAD // Öffnungswinkel
        )
    );
}
```

### Wo kommt der MasterSimulator eines Bots her?

Wenn ein neuer Bot zur World hinzugefügt wird, ruft sie ihre Methode `createSimulator()` auf. Diese erzeugt für einen CtBotSimTcp einen MasterSimulator, für einen CtBotSimTest einen leeren Simulator, der nichts tut.
