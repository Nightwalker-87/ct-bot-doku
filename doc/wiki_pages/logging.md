# Logging vom c't-Bot aus

Die Log-Funktionen im Code bieten sich an wenn man herausfinden will,

* ob die Sensoren des Bots gut kalibriert sind,
* ob das eigene Verhalten alles richtig macht, oder
* was die Sensoren so detektieren.

Log-Ausgaben kann man entweder an den c't-Sim übertragen oder auf eine MMC-/SD-Karte schreiben.
Formatiert man die Ausgaben richtig, so kann man sie später leicht in gängigen Tabellenkalkulationsprogrammen wie beispielsweise Libre Office Calc importieren und grafisch darstellen.
Das kann dann z.B. [so](../../_tmp_trac_wiki_export/ct-Bot-Software-Sensoren/ct-Bot-Software-Sensoren.md#Analyse-des-Maussensors-und-der-Distanzsensoren) aussehen.

Im Code muss man lediglich an den Stellen, an denen man Daten ausgeben will solche Zeilen einfügen:

```C
LOG_DEBUG("\tMaus:\t%d\tSpeed:\t%d\tTime:\t%lu", (int16_t) x_pos, target_speed_r, TIMER_GET_TICKCOUNT_32);
```

Das erzeugt dann eine tabulatorgetrennte Ausgabe, welche sich mit jeder Tabellenkalkulation leicht importieren lässt.

Wohin die Log-Ausgaben gehen, stellt man in der Datei ct-Bot.h ein, indem man die Kommentarzeichen vor dem gewünschten Ziel entfernt:

```C
//#define LOG_CTSIM_AVAILABLE   /**< Logging ueber das ct-Sim (PC und MCU) */
//#define LOG_DISPLAY_AVAILABLE /**< Logging ueber das LCD-Display (PC und MCU) */
//#define LOG_UART_AVAILABLE    /**< Logging ueber UART (NUR fuer MCU) */
//#define LOG_STDOUT_AVAILABLE  /**< Logging auf die Konsole (NUR fuer PC) */
//#define LOG_MMC_AVAILABLE     /**< Logging in eine txt-Datei auf der MMC */
```

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Benjamin Benz, Timo Sandmann
