# xerolib
[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/stechnik/xerolib/blob/main/README.md)
[![de](https://img.shields.io/badge/lang-de-green.svg)](https://github.com/stechnik/xerolib/blob/main/README.de.md)

Library for [TAPPS2](https://wiki.ta.co.at/TAPPS2) by Austrian [PLC](https://en.wikipedia.org/wiki/Programmable_logic_controller) manufacturer [Technische Alternative](https://www.ta.co.at/) making HVAC calculations easier. Made and maintained by [Schwab Technik GmbH](https://www.schwabtechnik.ch) the company behind [Xerovent](https://www.xerovent.com/) energy efficient dehumidification.

This .bib library can be added to TAPPS2. It's content then appears in the program window left bottom section.

Currently the library contains:
- a function template for calculating [saturation vapour pressure](https://en.wikipedia.org/wiki/Vapor_pressure) of water vapour over water — over supercooled water at sub-zero temperatures.
- an identical function template as above but in units of hPa (mbar) with two decimal places
- a set of blocks to calculate basic properties of humid air such as
  -  partial pressures of steam and dry air
  -  [absolute humidity](https://en.wikipedia.org/wiki/Humidity#Absolute_humidity)
  -  [mixing ratio](https://en.wikipedia.org/wiki/Mixing_ratio)
  -  density of dry air
  -  [specific humidity](https://en.wikipedia.org/wiki/Humidity#Specific_humidity)
- a set of blocks to calculate mixing ratio alone
- a set of blocks to calculate enthalpy $h_{1+x}$ out of a temperature and a mixing ratio
- a set of blocks to calculate surface humidity (activity of water) out of a mixing ratio and a surface temperature
- a set of blocks to calculate surface humidity out of specific humidity and a surface temperature
- a block to calculate the relative humidity at a location B out of the relative humidity at a location A and the saturation vapour pressures at A and B, e.g. at a colder surface. It assumes the air holds the same amount of water vapour at both locations.

## How to install
1. save the .lib-File on your local hard drive
2. open TAPPS2 and within TAPPS2 open a .tdw file or create a new one
3. on the bottom left part right-click ''own libraries''. Or click on the ``Add Library`` icon on the top left window corner.
4. in the dialog that appears, choose the .lib file from the location you saved it.

## How to use
Just drag the desired function block set from the library in the bottom left corner to your programming area. Depending on the hardware version, [MTx2](https://www.ta.co.at/en/x2-operation-interfaces) displays have a built-in air pressure sensor whose signal can be used to calculate the mixing ratio. Alternatively, a fixed value adjusted to the sea level of the location can be used; the resulting error is negligible for most building technology applications.

TA specifies the absolute humidity and dew point directly with its humidity sensors (MTx2, [RAS-CT4](https://www.ta.co.at/en/sensors/raumsensor-mit-touch-display) [RAS](https://www.ta.co.at/en/sensors/room-sensor-with-remote-display), [RFS](https://www.ta.co.at/en/sensors/humidity-sensor)). However, both values change when air flows through a heat exchanger. Therefore, when comparing air of different temperatures, the mixing ratio should generally be used.

## Some background on interpolation
The saturation vapour pressure over water is calculated with the exact formula of Dietrich Sonntag from 1990. It is more accurate than [VDI/VDE 3514 Sheet 1](https://www.vdi.de/richtlinien/details/vdivde-3514-blatt-1-gasfeuchtemessung-kenngroessen-und-formelzeichen); over the temperature range used here, its own deviation is orders of magnitude smaller than the error of the curve interpolation and therefore negligible. This accuracy is helpful when working with small temperature differences.

The possible maximum of 120 support points is used for the interpolation, covering the range from -30.0 °C to 69.0 °C without a gap. The pressure values and reference points were selected to minimise the interpolation error. This means that the pressure values at a reference point may differ slightly from the true value if this improves the interpolated values. At low temperatures, the relative error is greatest, but it stays below ±0.35 %. At higher temperatures, the absolute error is greatest, but does not exceed ±1.5 Pa. Since TA does not process values above 30000 Pa, the maximum application temperature is 69.0 °C. There is no longer a range with reduced accuracy; the curve is equally accurate throughout.

## Enhancement factor
In humid air the saturation vapour pressure is slightly higher than over pure water, because the other gases affect the vapour. The enhancement factor $f$ describes this difference. It depends mainly on air pressure: according to the WMO it is 1.0044 at 900 hPa, 1.0047 at 1013 hPa and 1.0048 at 1050 hPa.

The curves give the saturation vapour pressure over pure water, without the factor. The blocks that convert between relative humidity and partial pressure use a fixed factor of 1.0047. Compared to the pressure-dependent value, the error stays below ±0.04 % in the usual pressure range and is therefore negligible. Where only two saturation vapour pressures are put in relation, as for surface humidity, the factor cancels out.

## What changes compared to previous versions
### Compared to the version of August 2026
- The enhancement factor of 1.0047 is back, but only where relative humidity and partial pressure are converted into each other: absolute humidity and mixing ratio in the set for the basic properties of humid air («feuchte Luft»), partial pressure in the set for mixing ratio alone («nur Feuchtegrad»), and both sets for surface humidity («Umkehrf. Feuchtegrad», «Umkehrf. spez. Feuchte»). The curves remain without the factor.
- For the same relative humidity, partial pressure, absolute humidity, mixing ratio and specific humidity are therefore about 0.47 % higher. For the same mixing ratio, the surface humidity sets return a relative humidity 0.47 % lower, so they once again return exactly the relative humidity originally measured.
- If you already use the surface humidity sets in a program, you have to copy the new constants there by hand.
- New block for surface humidity (see above).
- The curves are now named «Sättigungsdampfdruck H2O Pascal» and «Sättigungsdampfdruck H2O hPa» instead of «… H2O-Luft …».
- Units are written as text where TA has no unit of its own.

### Compared to versions before August 2026
- At sub-zero temperatures the saturation vapour pressure is now calculated over supercooled water instead of over ice, matching how the sensors report their relative humidity. Only temperatures below 0 °C are affected; there the results are higher: about +5 % at -5 °C, +10 % at -10 °C, +22 % at -20 °C and +34 % at -30 °C. From 0 °C upwards nothing changes.
- The enhancement factor of 1.0047 is no longer part of the curve but of the blocks. The curves therefore return values 0.47 % lower; the results of the blocks stay the same above 0 °C.
- A faulty support point at 30.5 °C was corrected; it was about 22 % too low.
- The curve now extends to 69.0 °C instead of 68.9 °C and is equally accurate throughout. The reduced-accuracy section between -30 °C and -20 °C is gone.

If you have parametrised limits or setpoints based on the previous blocks, review them after updating — especially for applications below 0 °C.

## Literature
- Sonntag, Dietrich: _Important New Values of the Physical Constants of 1986, Vapor Pressure Formulations based on the ITS-90 and Psychrometer Formulae._ In: Zeitschrift für Meteorologie 70 (1990) 5, pp. 340–344
- World Meteorological Organization: _Guide to Instruments and Methods of Observation (WMO-No. 8), Volume I, Annex 4.B: Formulae for the computation of measures of humidity._