# N2O Flux Trailer Weather Station

Simple data acquisition from Vaisala [WXT520](https://www.campbellsci.com/wxt520)
using a Campbell Scientific [CR1000](https://www.campbellsci.com/cr1000) to
support the N<sub>2</sub>O flux support tailer owned by [WSU LAR](lar.wsu.edu).

> **TO DO cover photo**

Future sensors:
* GPS 16X
* PAR sensor
* thermocouple or old HMP45AC for interior temp (/RH)
* magnetic switch (door) sensor


## Wiring

### Power System

The weather station and datalogger are powered from a 12V power supply/charge
regulator ([PS200](https://www.campbellsci.com/ps200), Campbell Scientific).
The charge regulator normally obtains power from 120Vac mains, and switches to
a 7AH gel cell battery for backup power.

> *The charge regulator also supports the trailer telecommunications equipment
> (modem, router, wireless access point, etc) so research site clients can
> still communicate email error reports in the event of site power loss.*


### WXT520 

The cable used does **not** match either vendor or manufacturer color
conventions. Refer to this table exclusively for wiring the WXT520:

| Description    | Color  | M8 conn. pin | CR1000 |
|----------------|--------|:------------:|:------:|
| power input    | brown  | 2            | 12V    |
| power ground   | green  | 8            | G      |
| cable shield   | bare   | -            | G      |
| SDI-12 data Tx | yellow | 7            | C7     |
| SDI-12 data Rx | black  | 1            | C7     |
| SDI-12 ground  | white  | 3            | G      |
| heater (+)     | blue   | 4            | SW12V  |
| heater (-)     | orange | 6            | G      |
| *not used*     | red    | 5            | -      |


## Configuration Summary

Use the Vaisala WXT Configuration Tool to modify settings as follows:

* SDI-12 v1.3, continuous mode enabled
* sensors averaging interval = 60sec
* messages = all but hail and rain peak



## Licensing

* Original software contributions are licensed under [The MIT License](https://opensource.org/licenses/MIT). 
* Documentation, including images, are licensed under [CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/).(Creative Commons Attribution-ShareAlike 4.0 International)
* This work derived from [*Compost WXT520 Logger Program*](https://github.com/patricktokeeffe/compost-wxt520),
  which is also subject to The MIT License.


## References

* Campbell Scientific. *WXT510 Weather Transmitter Instruction Manual.*
  Retrieved [2019-10-25](http://web.archive.org/web/20191025233109/https://s.campbellsci.com/documents/us/manuals/wxt510.pdf).
  Online: <https://s.campbellsci.com/documents/us/manuals/wxt510.pdf>

* O'Keeffe, Patrick. *Compost WXT520 Logger Program.*
  [Retrieved 2019-10-25](https://github.com/patricktokeeffe/compost-wxt520/commit/0e3ad20997b60249bfd563e00267422574ed0416).
  Online: <https://github.com/patricktokeeffe/compost-wxt520>

* Vaisala Oyj. *Vaisala Weather Transmitter WXT510 User's Guide.*
  [Revision 2006](http://web.archive.org/web/20180116043159/https://www.vaisala.com/sites/default/files/documents/WXT510_User_Guide_in_English.pdf).
  Retrieved 2019-10-25. Online:
  <https://www.vaisala.com/sites/default/files/documents/WXT510_User_Guide_in_English.pdf>

