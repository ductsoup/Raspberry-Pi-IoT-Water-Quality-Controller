# Raspberry Pi IoT Water Quality Controller
A Raspberry Pi based controller that can be used for water treatment systems, hydroponics, aeroponics, aquaponics, reef tanks and similar applications.

## Overview
This is currently a work in progress repository inspired by [reef-pi](https://github.com/reef-pi/reef-pi). There's a great write up on that project over at [Adafruit](https://learn.adafruit.com/search?q=reef-pi). 

This is simply a variation on the same theme that's better suited to what I'm doing. Rather than a web interface, this is  Python based so it can exchange information via MQTT and other protocols.

## Hardware
### Water Quality Sensing
[Atlas Scientific](https://www.atlas-scientific.com) offers a stackable HAT for Raspberry Pi called Tentacle T3 for their EZO boards and sensors. It provides two isolated, one non-isolated and two spare channels. 

I'm using the non-isolated for RTD temperature and the other two for PH and electrical conductivity (total dissolved solids). I've also repurposed one of the spare channels for dissolved oxygen by adding an additional isolated carrier board. Something similar can be done with channel 5.

* [Whitebox Labs Tentacle T3](https://www.atlas-scientific.com/product_pages/components/tentacle-t3.html)
* [Electrically Isolated EZO™ Carrier Board](https://www.atlas-scientific.com/product_pages/components/single_carrier_iso.html)
** [EZO RTD](https://www.atlas-scientific.com/product_pages/circuits/ezo_rtd.html)
** [EZO PH](https://www.atlas-scientific.com/product_pages/circuits/ezo_ph.html)
** [EZO EC](https://www.atlas-scientific.com/product_pages/circuits/ezo_ec.html)
** [EZO DO](https://www.atlas-scientific.com/product_pages/circuits/ezo_do.html)

![Sensor](/images/hydro_sensor_bb.png)



