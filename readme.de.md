# xerolib
[![de](https://img.shields.io/badge/lang-de-red.svg)](/stechnik/xerolib/blob/master/README.de.md)
[![en](https://img.shields.io/badge/lang-en-green.svg)](/stechnik/xerolib/blob/master/README.md)

Bibliothek für [TAPPS2](https://wiki.ta.co.at/TAPPS2) des Österreichischen [SPS](https://en.wikipedia.org/wiki/Programmable_logic_controller)-Herstellers [Technische Alternative](https://www.ta.co.at/) mit dem Ziel, typische Lüftungsberechnungen einfacher zu gestalten. Geschrieben und unterhalten von der [Schwab Technik GmbH](https://www.schwabtechnik.ch), der Firma hinter [Xerovent](https://www.xerovent.ch/), dem energieeffizienten Entfeuchtungsverfahren.

Diese .bib-Datei wird in TAPPS2 eingebunden. Dann erscheint ihr Inhalt links unten im Programmfenster.

Momentan enthält die Bibliothek:
- eine fertige «Kennlinienfunktion 2D», welche anhand einer Temperatur den Sättigungsdampfdruck des Wasserdampfes in der Luft berechnet. Dabei wird die Magnus-Formel anhand einer Tabelle interpoliert. Die Werte der Magnus-Formel entstammen [VDI/VDE 3514 Blatt 1](https://www.vdi.de/richtlinien/details/vdivde-3514-blatt-1-gasfeuchtemessung-kenngroessen-und-formelzeichen), die Enhancementfaktoren für feuchte Luft entstammen [Wikipedia](https://de.wikipedia.org/w/index.php?title=S%C3%A4ttigungsdampfdruck&oldid=236975950#Korrekturfaktoren_f%C3%BCr_feuchte_Luft).
- ein Set an Funktionsblöcken, welche anhand einer Temperatur und relativen Feuchte die grundlegenden Eigenschaften feuchter Luft berechnen, die da wären:
  - spezifische Feuchte
  - absolute Feuchte
  - Mischungsverhältnis
  - Partialdruck des Wasserdampfes
  - Partialdruck der trockenen Luft
  - Dichten der trockenen und feuchten Luft
