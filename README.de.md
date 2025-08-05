# xerolib
[![de](https://img.shields.io/badge/lang-de-red.svg)](https://github.com/stechnik/xerolib/blob/main/README.de.md)
[![en](https://img.shields.io/badge/lang-en-green.svg)](https://github.com/stechnik/xerolib/blob/main/README.md)

Bibliothek für [TAPPS2](https://wiki.ta.co.at/TAPPS2) des Österreichischen [SPS](https://en.wikipedia.org/wiki/Programmable_logic_controller)-Herstellers [Technische Alternative](https://www.ta.co.at/) mit dem Ziel, typische Lüftungsberechnungen der Gebäudetechnik einfacher zu gestalten. Geschrieben und unterhalten von der [Schwab Technik GmbH](https://www.schwabtechnik.ch), der Firma hinter [Xerovent](https://www.xerovent.com/), dem energieeffizienten Entfeuchtungsverfahren.

Diese .bib-Datei wird in TAPPS2 eingebunden. Dann erscheint ihr Inhalt links unten im Programmfenster.

Momentan enthält die Bibliothek:
- eine ausgefüllte «Kennlinienfunktion 2D», welche anhand einer Temperatur den Sättigungsdampfdruck des Wasserdampfes in der feuchten Luft berechnet. Werte in Pascal ohne Kommastellen.
- eine ausgefüllte «Kennlinienfunktion 2D» wie oben, aber mit Hektopascal auf zwei Kommastellen als Ausgabeeinheit
- ein Set aus Funktionsblöcken, welche anhand einer Temperatur und relativen Feuchte die grundlegenden Eigenschaften feuchter Luft berechnen, die da wären:
  - Partialdruck des Wasserdampfes
  - Dampfdichte
  - Feuchtegrad
  - Partialdruck der trockenen Luft
  - Dichten der trockenen und feuchten Luft
  - spezifische Feuchte
- ein Set aus Funktionsblöcken, um nur den Feuchtegrad zu bestimmen
- ein Set aus Funktionsblöcken, um aus einer Temperatur und einem Feuchtegrad die Enthalpie $h_{1+x}$ der ungesättigten feuchten Luft zu berechnen
- ein Set aus Funktionsblöcken, um aus einem Feuchtegrad und einer Oberflächentemperatur die relative Feuchtigkeit an der Oberfläche zu berechnen
- ein Set aus Funktionsblöcken wie oben, aber mit der spezifischen Feuchte als Eingabegrösse

## Wie installieren
1. Speichern Sie die .lib-Datei auf Ihrer Festplatte
2. Öffnen Sie TAPPS2 und innerhalb TAPPS2 öffnen Sie eine .tdw-Datei oder erstellen Sie eine neue.
3. Rechtsklicken Sie im unteren linken Baum auf ``Bibliotheken``, alternativ klicken sie auf das Buch-Icon mit dem Plus am oberen linken Fensterrand.
4. Es öffnet sich ein Dialog, wo Sie die .lib-Datei auswählen können.

## Wie benutzen
Einfach den gewünschten Baustein im Auswahlbaum anklicken und auf den Programmier-Bereich ziehen.

## Etwas Hintergrund zur Interpolation
Der Sättigungsdampfdruck wird für Wasserdampf in der feuchten Luft berechnet. Dabei wird die genaue Formel von Dietrich Sonntag von 1990 verwendet und ein konstanter Enhancementfaktor von 1.0047. Diese Formel ist genauer als [VDI/VDE 3514 Blatt 1](https://www.vdi.de/richtlinien/details/vdivde-3514-blatt-1-gasfeuchtemessung-kenngroessen-und-formelzeichen). Im Bereich von 200 bis 1100 hPa und -20 bis 68.9 °C beträgt die Standardabweichung der Formel weniger als ±0.15 Pa. Diese Genauigkeit ist hilfreich, wenn man mit kleinen Temperatudrifferenzen arbeitet.

Für die Interpolation werden die maximal möglichen 120 Stützpunkte verwendet. Dabei entfallen 119 auf den Bereich von -20 °C bis 68.9 °C. Die Druckwerte und Stützpunkte wurden gewählt, um den Interpolationsfehler zu minimieren. Das bedeutet, dass die Werte eines Stützpunktes geringfügig abweichen können, wenn dadurch die interpolierten Werte besser werden. Bei tiefen Temperaturen ist der relative Fehler am grössten, mit Spitzen von ±0.6 %. Bei höheren Temperaturen ist der absolute Fehler am grössten, wobei er ±2.5 Pa nicht überschreitet. Da TA keine Werte über 30000 Pa verarbeitet, ergibt sich eine maximale Anwendungstemperatur von 68.9 °C. Im Bereich zwischen -30 °C und -20 °C wird ein  Signal mit reduzierter Genauigkeit geliefert für selten erwartete Temperaturen. Die Abweichung beträgt in dem Bereich max. ±15 % oder ±6 Pa.

## Literatur
- Sonntag, Dietrich: _Important New Values of the Physical Constants of 1986, Vapor Pressure Formulations based on the ITS-90 and Psychrometer Formulae._ In: Zeitschrift für Meteorologie 70 (1990) 5, pp. 340–344