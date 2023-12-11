# xerolib
[![de](https://img.shields.io/badge/lang-de-red.svg)](https://github.com/stechnik/xerolib/blob/main/README.de.md)
[![en](https://img.shields.io/badge/lang-en-green.svg)](https://github.com/stechnik/xerolib/blob/main/README.md)

Bibliothek für [TAPPS2](https://wiki.ta.co.at/TAPPS2) des Österreichischen [SPS](https://en.wikipedia.org/wiki/Programmable_logic_controller)-Herstellers [Technische Alternative](https://www.ta.co.at/) mit dem Ziel, typische Lüftungsberechnungen einfacher zu gestalten. Geschrieben und unterhalten von der [Schwab Technik GmbH](https://www.schwabtechnik.ch), der Firma hinter [Xerovent](https://www.xerovent.ch/), dem energieeffizienten Entfeuchtungsverfahren.

Diese .bib-Datei wird in TAPPS2 eingebunden. Dann erscheint ihr Inhalt links unten im Programmfenster.

Momentan enthält die Bibliothek:
- eine ausgefüllte «Kennlinienfunktion 2D», welche anhand einer Temperatur den Sättigungsdampfdruck des Wasserdampfes in der feuchten Luft berechnet. Dabei wird die Magnus-Formel anhand einer Tabelle interpoliert. Die Werte der Magnus-Formel entstammen [VDI/VDE 3514 Blatt 1](https://www.vdi.de/richtlinien/details/vdivde-3514-blatt-1-gasfeuchtemessung-kenngroessen-und-formelzeichen), die Enhancementfaktoren für feuchte Luft entstammen [Wikipedia](https://de.wikipedia.org/w/index.php?title=S%C3%A4ttigungsdampfdruck&oldid=236975950#Korrekturfaktoren_f%C3%BCr_feuchte_Luft). Werte in Pascal ohne Kommastellen.
- eine ausgefüllte «Kennlinienfunktion 2D» wie oben, aber mit Hektopascal auf zwei Kommastellen als Ausgabeeinheit
- ein Set an Funktionsblöcken, welche anhand einer Temperatur und relativen Feuchte die grundlegenden Eigenschaften feuchter Luft berechnen, die da wären:
  - Partialdruck des Wasserdampfes
  - Dampfdichte
  - Feuchtegrad
  - Partialdruck der trockenen Luft
  - Dichten der trockenen und feuchten Luft
  - spezifische Feuchte
- ein Set aun Funktionsblöcken, um nur den Feuchtegrad zu bestimmen
- ein Set aun Funktionsblöcken, um die Enthalpie der ungesättigten feuchten Luft zu berechnen
- ein Set aun Funktionsblöcken, um aus einem Feuchtegrad und einer Oberflächentemperatur die relative Feuchtigkeit an der Oberfläche zu berechnen
- ein Set aun Funktionsblöcken wie oben, aber mit der spezifischen Feuchte als Eingabegrösse

## Wie installieren
1. Speichern Sie die .lib-Datei auf Ihrer Festplatte
2. Öffnen Sie TAPPS2 und innerhalb TAPPS2 öffnen Sie eine .tdw-Datei oder erstellen Sie eine neue.
3. Rechtsklicken Sie im unteren linken Baum auf ``Bibliotheken``, alternativ klicken sie auf das Buch-Icon mit dem Plus am oberen linken Fensterrand.
4. Es öffnet sich ein Dialog, wo Sie die .lib-Datei auswählen können.

## Wie benutzen
Einfach den gewünschten Baustein im Auswahlbaum anklicken und auf den Programmier-Bereich ziehen.