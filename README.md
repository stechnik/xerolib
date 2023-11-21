# xerolib
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pt-br](https://img.shields.io/badge/lang-de-green.svg)](README.de.md)

Library for [TAPPS2](https://wiki.ta.co.at/TAPPS2) by Austrian [PLC](https://en.wikipedia.org/wiki/Programmable_logic_controller) manufacturer [Technische Alternative](https://www.ta.co.at/) making HVAC calculations easier. Made and maintained by [Schwab Technik GmbH](https://www.schwabtechnik.ch) the company behind [Xerovent](https://www.xerovent.ch/) energy efficient dehumidification.

This .bib library can be added to TAPPS2. It's content then appears in the program window left bottom section.

Currently the library contains:
- a function template for calculating saturation vapour pressure of water in air. The August-Roche-Magnus formula is used therefore based on [VDI/VDE 3514 Part 1](https://www.vdi.de/richtlinien/details/vdivde-3514-blatt-1-gasfeuchtemessung-kenngroessen-und-formelzeichen) with enhancement factors for humid air. The enhancement factors were taken from [Wikipedia](https://de.wikipedia.org/w/index.php?title=S%C3%A4ttigungsdampfdruck&oldid=236975950#Korrekturfaktoren_f%C3%BCr_feuchte_Luft)
- a set of functions to calculate basic properties of humid air such as
  -  specific humidity
  -  absolute humidity
  -  mixing ratio
  -  partial pressure of steam
  -  partial pressure of dry air
  -  density of dry and moist air
