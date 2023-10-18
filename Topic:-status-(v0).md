[docs](https://github.com/south-coast-science/docs/wiki) >
[data formats](https://github.com/south-coast-science/data-formats/wiki) >
[topic: gases](https://github.com/south-coast-science/data-formats/wiki/Topic:-gases) 
***


_Deprecated as of October 2021. This version continues to be supported by the South Coast Science data infrastructure, but is no longer available for new or upgraded devices._


Actual fields will vary, depending on the device's sensor configuration. Note that electrochemical sensors have auxiliary electrodes, whereas PIDs (used to sample VOCs) do not.

Depending on device configuration, the sensor used as the source of temperature and humidity data may or may not be the same as that for climate.

#### JSON example
> {"rec": "2021-10-12T15:58:38Z", "tag": "scs-bgx-537", "val": {"NO2": {"weV": 0.29513, "aeV": 0.28663, "weC": 0.00103, "cnc": 73.2}, "Ox": {"weV": 0.41782, "aeV": 0.41001, "weC": 0.03584, "cnc": -160.4}, "NO": {"weV": 0.26563, "aeV": 0.28844, "weC": 0.07678, "cnc": -523.1}, "CO": {"weV": 0.30569, "aeV": 0.27894, "weC": 0.01881, "cnc": 114.0}, "sht": {"hmd": 68.8, "tmp": 17.3}}, "exg": {"vB20": {"NO2": {"cnc": 9.3}}}}


#### CSV example
> rec, tag, val.NO2.weV, val.NO2.aeV, val.NO2.weC, val.NO2.cnc, val.Ox.weV, val.Ox.aeV, val.Ox.weC, val.Ox.cnc, val.NO.weV, val.NO.aeV, val.NO.weC, val.NO.cnc, val.CO.weV, val.CO.aeV, val.CO.weC, val.CO.cnc, val.sht.hmd, val.sht.tmp, exg.vB20.NO2.cnc

> 2021-10-12T15:59:48Z, scs-bgx-537, 0.295, 0.28669, 0.0008, 72.0, 0.41857, 0.41001, 0.03695, -157.6, 0.26544, 0.28832, 0.07576, -525.6, 0.305, 0.27825, 0.01763, 108.2, 68.7, 17.3, 9.5


#### Major fields
| Path | Meaning |
|:--------|---|
| tag | the unique ID of the sensing equipment |
| rec | an ISO 8601 localised datetime of the sensing operation |
| val | data, as reported by the sensors |
| exg | interpreted gas concentrations |



#### val fields
XXX is the name of a gas. It can be one of CO, CO2, H2S, NO, NO2 Ox, SO2, or VOC. Note the use of Ox to represent ozone.

| Path | Meaning | Unit |
|:--------|---|---|
| val.XXX.aeV | auxiliary electrode voltage | Volts |
| val.XXX.weV | working electrode voltage | Volts |
| val.XXX.weC | temperature-compensated working electrode voltage | Volts |
| val.XXX.cnc | gas concentration, based on Alphasense Application Note 803 | parts per billion |
| val.sht.hmd | relative humidity | % |
| val.sht.tmp | temperature | Centigrade |

#### exg fields
Supplied by the the interpretation algorithm NNN. Any number of alternate algorithm outputs may be included.

| Path | Meaning | Unit |
|:--------|---|---|
| exg.NNN.XXX.cnc | interpreted concentration for gas XXX | parts per billion |

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
