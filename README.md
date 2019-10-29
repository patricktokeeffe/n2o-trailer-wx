# N2O Flux Trailer Weather Station

Simple data acquisition from Vaisala [WXT520](https://www.campbellsci.com/wxt520)
using a Campbell Scientific [CR1000](https://www.campbellsci.com/cr1000) to
support the N<sub>2</sub>O flux support tailer owned by [WSU LAR](lar.wsu.edu).

> **TO DO cover photo**


## Wiring

### Power System

The weather station and datalogger are powered from a 12V power supply/charge
regulator ([PS100](https://www.campbellsci.com/ps100), Campbell Scientific).
The charge regulator normally obtains power from a 19Vdc laptop power supply
and float charges a 7AH gel cell battery. If primary power is lost, the battery
continues to operate the logger and sensors for up to several hours.

> *The PS100 also supports telecommunications equipment (modem, WiFi, etc)
> so network clients can still deliver email alarms in the event of power loss
> at the site.*

### WXT510

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

### QUANTUM (PAR) sensor

The (very old) PAR sensor (LI-190SA; LI-COR Biosciences) requires an inverted
differential setup:

> *The multiplier is also negative, which produces a correct polarity signal.*

| Description  | Color | CR1000 |
|----------------------------------|:-----:|:-----:|
| 2290 Millivolt adapter, negative | blue  | DF1 H |
| 2290 Millivolt adapter, positive | green | DF1 L |
| *jumper to CR1000 DF 1L port*    | green | &#x23DA; |


### ~~Door switch~~

> **FUTURE enhancement pending hardware upgrades**

| Description | Color | CR1000 |
|-------------|:-----:|:------:|
| wire #1     | white | ~~5V~~     |
| wire #2     | white | ~~C8~~     |


## Operation

### To deploy the unit

1. Mount WXT520 oriented to True North; see user manuals under References below
2. Connect power/data cable to WXT520
3. Turn the PS200 power switch to *ON*


### To monitor in real time

Data can be viewed on the hand held keyboard display.


### To collect data

> To do: transition to FTP for data downloads...


## Data Products

The weather station internally produces 1-minute average values and the logger
samples those values at the start of each minute. A single data file is written
to CompactFlash memory card:

* Base name: `compost_WXT520`
* Record interval: 5 minutes
* Number of records: approximately 90 days on external memory card (up to 230
  days internal storage)
* Fill-stop settings: "ring" mode - overwrites oldest records when card is full

| Field name         | Units   | Description |
|--------------------|---------|-------------|
| power_in_Avg       | Vdc     | Battery voltage |
| WindSpeed_sclr_Avg | m/s     | Mean horizontal wind speed |
| WindSpeed_rslt_Avg | m/s     | Mean wind vector magnitude |
| WindDir_rslt_Avg   | degrees | Resultant mean wind direction |
| WindDir_sclr_Avg   | degrees | Standard deviation of wind direction calculated using Campbell Scientific's wind speed weighted algorithm (not recommended for straight-line Gaussian dispersion models, but OK for variable-trajectory transport models [ref](#ref1)) |
| Tmpr_Avg           | ºC      | Mean air temperature |
| RH_Avg             | %       | Mean relative humidity |
| Press_Avg          | hPa     | Mean barometric pressure |
| R_amt_Avg          | mm      | Mean rain amount |
| R_dur_Avg          | sec     | Mean rain duration |
| R_int_Avg          | mm/hr   | Mean rain intensity |
| WindSpeed_min_Avg  | m/s     | Mean minimum wind speed |
| WindSpeed_avg_Avg  | m/s     | Mean average wind speed |
| WindSpeed_max_Avg  | m/s     | Mean maximum wind speed |
| WindDir_min_Avg    | degrees | ^Mean minimum wind direction |
| WindDir_avg_Avg    | degrees | ^Mean average wind direction |
| WindDir_max_Avg    | degrees | ^Mean maximum wind direction |

**Notes:**
* **^** value is dubious


## Configuration Summary

Use the Vaisala WXT Configuration Tool to modify settings as follows:

* Device Settings
  * Enable heating
  * SDI-12 v1.3, continuous mode enabled
* sensors averaging interval = 60sec
* Message Settings
  * messages = all but hail and rain peak
* Sensor Settings
  *


## Licensing

* Original software contributions are licensed under [The MIT License](https://opensource.org/licenses/MIT). 
* Documentation, including images, are licensed under [CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/).(Creative Commons Attribution-ShareAlike 4.0 International)
* This work derived from [*Compost WXT520 Logger Program*](https://github.com/patricktokeeffe/compost-wxt520),
  which is also subject to The MIT License.


## References

* Campbell Scientific. *HMP45C Temperature and Relative Humidity Probe Instruction Manual.*
  Revision [03/09](http://web.archive.org/web/20180517103656/s.campbellsci.com/documents/us/manuals/hmp45c.pdf)
  Online: <https://s.campbellsci.com/documents/us/manuals/hmp45c.pdf>

* Campbell Scientific. *GPS16X-HVS GPS Receiver Instruction Manual.*
  Revision [9/15](http://web.archive.org/web/20191026023811/http://s.campbellsci.com/documents/ca/manuals/gps16x-hvs_man.pdf).
  Online: <https://s.campbellsci.com/documents/ca/manuals/gps16x-hvs_man.pdf>

* Campbell Scientific. *WXT510 Weather Transmitter Instruction Manual.*
  Revision [4/07](http://web.archive.org/web/20191025233109/https://s.campbellsci.com/documents/us/manuals/wxt510.pdf).
  Online: <https://s.campbellsci.com/documents/us/manuals/wxt510.pdf>

* LI-COR Biosciences. *Terrestrial Quantum Sensors Instruction Manual.*
  Build date [Thursday, May 23, 2019](http://web.archive.org/web/20191026023428/https://www.licor.com/documents/oo6v1v8bbtoxbd7o299u6a503g32w3g5).
  Online: <https://www.licor.com/documents/oo6v1v8bbtoxbd7o299u6a503g32w3g5>


-> LTAR program for the door switch code..

* O'Keeffe, Patrick. *Compost WXT520 Logger Program.*
  [Retrieved 2019-10-25](https://github.com/patricktokeeffe/compost-wxt520/commit/0e3ad20997b60249bfd563e00267422574ed0416).
  Online: <https://github.com/patricktokeeffe/compost-wxt520>

* Vaisala Oyj. *Vaisala HUMICAP&reg; Humidity and Temperature Probes User's Guide.*
  Revision [2006](http://web.archive.org/web/20190515162841/www.vaisala.com/sites/default/files/documents/HMP45AD-User-Guide-U274EN.pdf).
  Online: <https://www.vaisala.com/sites/default/files/documents/HMP45AD-User-Guide-U274EN.pdf>

* Vaisala Oyj. *Vaisala Weather Transmitter WXT510 User's Guide.*
  Revision [2006](http://web.archive.org/web/20180116043159/https://www.vaisala.com/sites/default/files/documents/WXT510_User_Guide_in_English.pdf).
  Online: <https://www.vaisala.com/sites/default/files/documents/WXT510_User_Guide_in_English.pdf>

