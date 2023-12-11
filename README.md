# xerolib
[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/stechnik/xerolib/blob/main/README.md)
[![pt-br](https://img.shields.io/badge/lang-de-green.svg)](https://github.com/stechnik/xerolib/blob/main/README.de.md)

Library for [TAPPS2](https://wiki.ta.co.at/TAPPS2) by Austrian [PLC](https://en.wikipedia.org/wiki/Programmable_logic_controller) manufacturer [Technische Alternative](https://www.ta.co.at/) making HVAC calculations easier. Made and maintained by [Schwab Technik GmbH](https://www.schwabtechnik.ch) the company behind [Xerovent](https://www.xerovent.ch/) energy efficient dehumidification.

This .bib library can be added to TAPPS2. It's content then appears in the program window left bottom section.

Currently the library contains:
- a function template for calculating saturation vapour pressure of water in air. The August-Roche-Magnus formula is used therefore based on [VDI/VDE 3514 Part 1](https://www.vdi.de/richtlinien/details/vdivde-3514-blatt-1-gasfeuchtemessung-kenngroessen-und-formelzeichen) with enhancement factors for humid air. The enhancement factors were taken from [Wikipedia](https://de.wikipedia.org/w/index.php?title=S%C3%A4ttigungsdampfdruck&oldid=236975950#Korrekturfaktoren_f%C3%BCr_feuchte_Luft)
- an identical function template as above but in units of hPa with two decimal places
- a set of blocks to calculate basic properties of humid air such as
  -  specific humidity
  -  absolute humidity
  -  mixing ratio
  -  partial pressure of steam
  -  partial pressure of dry air
  -  density of dry and moist air
- a set of blocks to calculate mixing ratio alone
- a set of blocks to calculate enthalpy
- a set of blocks to calculate surface humidity (activity of water) out of a mixing ratio and a surface temperature
- a set of blocks to calculate surface humidity out of specific humidity and a surface temperature

## How to install
1. save the .lib-File on your local hard drive
2. open TAPPS2 and within TAPPS2 open a .tdw file or create a new one
3. on the bottom left part right-click ''own libraries''. Or click on the ``Add Library`` icon on the top left window corner.
4. in the dialog that appears, choose the .lib file from the location you saved it.

## How to use
Just drag the desired function block set from the library in the bottim left corner to your programming area.