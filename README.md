# xerolib
[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/stechnik/xerolib/blob/main/README.md)
[![pt-br](https://img.shields.io/badge/lang-de-green.svg)](https://github.com/stechnik/xerolib/blob/main/README.de.md)

Library for [TAPPS2](https://wiki.ta.co.at/TAPPS2) by Austrian [PLC](https://en.wikipedia.org/wiki/Programmable_logic_controller) manufacturer [Technische Alternative](https://www.ta.co.at/) making HVAC calculations easier. Made and maintained by [Schwab Technik GmbH](https://www.schwabtechnik.ch) the company behind [Xerovent](https://www.xerovent.com/) energy efficient dehumidification.

This .bib library can be added to TAPPS2. It's content then appears in the program window left bottom section.

Currently the library contains:
- a function template for calculating saturation vapour pressure of steam in air.
- an identical function template as above but in units of hPa with two decimal places
- a set of blocks to calculate basic properties of humid air such as
  -  specific humidity
  -  absolute humidity
  -  mixing ratio
  -  partial pressure of steam
  -  partial pressure of dry air
  -  density of dry and moist air
- a set of blocks to calculate mixing ratio alone
- a set of blocks to calculate enthalpy $h_{1+x}$ out of a temperature and a mixing ratio
- a set of blocks to calculate surface humidity (activity of water) out of a mixing ratio and a surface temperature
- a set of blocks to calculate surface humidity out of specific humidity and a surface temperature

## How to install
1. save the .lib-File on your local hard drive
2. open TAPPS2 and within TAPPS2 open a .tdw file or create a new one
3. on the bottom left part right-click ''own libraries''. Or click on the ``Add Library`` icon on the top left window corner.
4. in the dialog that appears, choose the .lib file from the location you saved it.

## How to use
Just drag the desired function block set from the library in the bottom left corner to your programming area.

## Some background on interpolation
The saturation vapour pressure is calculated for water vapour in humid air. The exact formula used is that of Dietrich Sonntag from 1990, with a constant enhancement factor of 1.0047. This formula is more accurate than [VDI/VDE 3514 Sheet 1](https://www.vdi.de/richtlinien/details/vdivde-3514-blatt-1-gasfeuchtemessung-kenngroessen-und-formelzeichen). In the range from 200 to 1100 hPa and -20 to 68.9 °C, the standard deviation of the formula is less than ±0.15 Pa. This accuracy is helpful when working with small temperature differences.

The possible maximum of 120 support points is used for the interpolation. Of these, 119 are in the range from -20 °C to 68.9 °C. The pressure values and reference points were selected to minimise the interpolation error. This means that the pressure values at a reference point may differ slightly from the true value if this improves the interpolated values. At low temperatures, the relative error is greatest, with peaks of ±0.6%. At higher temperatures, the absolute error is greatest, but does not exceed ±2.5 Pa. Since TA does not process values above 30000 Pa, the maximum application temperature is 68.9 °C. In the range between -30 °C and -20 °C, a signal with reduced accuracy is provided for rarely expected temperatures. The deviation in this range is max. ±15 % or ±6 Pa.

## Literature
- Sonntag, Dietrich: _Important New Values of the Physical Constants of 1986, Vapor Pressure Formulations based on the ITS-90 and Psychrometer Formulae._ In: Zeitschrift für Meteorologie 70 (1990) 5, pp. 340–344