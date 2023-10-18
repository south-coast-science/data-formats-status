[docs](https://github.com/south-coast-science/docs/wiki) >
[data formats](https://github.com/south-coast-science/data-formats/wiki) >
[topic: gases](https://github.com/south-coast-science/data-formats/wiki/Topic:-gases) 
***


Version 2 is backwards-compatible with versions 0 and 1 for raw electrochemical and T / rH values. It provides a different data structure to its predecessors for interpreted ("exg") gas concentrations. 

Actual fields will vary, depending on the device's sensor configuration. Note that electrochemical sensors have auxiliary electrodes, whereas PIDs (used to sample VOCs) do not.

Depending on device configuration, the sensor used as the source of temperature and humidity data may or may not be the same as that for climate.

#### JSON example
> {"rec": "2021-10-11T10:59:40Z", "tag": "scs-be2-3", "ver": 2.0, "src": "AFE", "val": {"NO2": {"weV": 0.29057, "aeV": 0.29544, "weC": 0.00131, "cnc": 20.9, "vCal": 15.41}, "Ox": {"weV": 0.40101, "aeV": 0.39969, "weC": 0.00235, "cnc": 55.7, "vCal": 6.61, "xCal": -0.390731}, "CO": {"weV": 0.44069, "aeV": 0.30213, "weC": 0.16795, "cnc": 685.4, "vCal": 562.256}, "sht": {"hmd": 52.9, "tmp": 21.9}}, "exg": {"src": "vB20", "val": {"NO2": {"cnc": 19.3}}}}

#### CSV example
> rec, tag, ver, src, val.NO2.weV, val.NO2.aeV, val.NO2.weC, val.NO2.cnc, val.NO2.vCal, val.Ox.weV, val.Ox.aeV, val.Ox.weC, val.Ox.cnc, val.Ox.vCal, val.Ox.xCal, val.CO.weV, val.CO.aeV, val.CO.weC, val.CO.cnc, val.CO.vCal, val.sht.hmd, val.sht.tmp, exg.src, exg.val.NO2.cnc  

> 2021-10-11T10:59:40Z, scs-be2-3, 2.0, AFE, 0.29057, 0.29544, 0.00131, 20.9, 15.41, 0.40101, 0.39969, 0.00235, 55.7, 6.61, -0.390731, 0.44069, 0.30213, 0.16795, 685.4, 562.256, 52.9, 21.9, vB20, 19.3  


#### Major fields
| Path | Meaning |
|:--------|---|
| tag | the unique ID of the sensing equipment |
| rec | an ISO 8601 localised datetime of the sensing operation |
| ver | 2.N (where N is a sub-version) |
| src | the sensor architecture (AFE or SD1) |
| val | data, as reported by the sensors |
| exg | interpreted gas concentrations |


#### val fields
_The cnc fields in this group should only be used where no equivalent exg.val.XXX.cnc field is present._  
  
XXX is the name of a gas. It can be one of CO, CO2, H2S, NO, NO2 Ox, SO2, or VOC. Note the use of Ox to represent ozone.

| Path | Meaning | Unit |
|:--------|---|---|
| val.XXX.aeV | auxiliary electrode voltage | Volts |
| val.XXX.weV | working electrode voltage | Volts |
| val.XXX.weC | temperature-compensated working electrode voltage | Volts |
| val.XXX.cnc | gas concentration, based on Alphasense Application Note 803 | parts per billion (CO2 is parts per million) |
| val.XXX.vCal | sensor output, adjusted for calibrated gain and zero offset | parts per billion |
| val.XXX.xCal | sensor output, adjusted for calibrated gain for NO2 cross-sensitivity and zero offset (Ox sensor only) | parts per billion |
| val.sht.hmd | relative humidity | % |
| val.sht.tmp | temperature | Centigrade |


#### exg fields
Supplied by one interpretation algorithm, as specified on the device.

| Path | Meaning | Unit |
|:--------|---|---|
| exg.src | the name of the interpretation algorithm | |
| exg.val.XXX.cnc | interpreted concentration for gas XXX | parts per billion |

#### Sampling intervals
For each individual device, sampling intervals may be changed at any time. The following are the factory-set defaults:

| Device | Interval |
|:-------|----------|
| Praxis/Handheld | 10 seconds |
| Praxis/OPCube | 10 seconds |
| Praxis/Urban | 10 seconds |

#### See also
[scs_dev/gases_sampler](https://github.com/south-coast-science/scs_dev/wiki/gases_sampler)  
[scs_mfr/schedule](https://github.com/south-coast-science/scs_mfr/wiki/schedule)  

#### Resources

https://en.wikipedia.org/wiki/ISO_8601
