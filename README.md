# Raspberry Pi IoT Water Quality Controller
A Raspberry Pi based controller that can be used for water treatment systems, hydroponics, aeroponics, aquaponics, reef tanks and similar applications.

The inspiration came from [reef-pi](https://github.com/reef-pi/reef-pi). There's a great write up on that project over at [Adafruit](https://learn.adafruit.com/search?q=reef-pi). 

This is simply a variation on the same theme better suited to what I'm doing that's coded in Python. 

* Interface with MQTT, MODBUS TCP and other protocols
* Interface with I2C sensors (RTD, PH, EC, DO, light)
* Control 12 VDC PWM devices (dosing pumps)
* Control 12 VDC devices (chillers, submersible pumps)
* Control 120 VAC devices (lights, air pumps)

### I2C Device Map
I/O is I2C for isolation and sanity purposes. Aside from 3.3V, GND, SDA and SCL all other Pi GPIO pins are available for other uses.

* 0x20 8 channel GPIO expander for 120V AC, 10A relays
* 0x21 4 channel GPIO expander for 12V DC, 20A MOSFETs
* 0x60 4 channel HAT 12V PWM, 1.2A
* 0x66 RTD
* 0x63 PH
* 0x64 EC/TDS
* 0x97 DO

The I2C bus connectors are 4 wires.
* 3.3V
* GND
* SDA
* SCL

### Full Disclosure
This is one of my infamous cocktail napkin designs and should be considered a prototype work in progress for now.

## Hardware
### Water Quality Sensing
Atlas Scientific offers a stackable HAT for Raspberry Pi called Tentacle T3 for their EZO boards and sensors. It provides two isolated, one non-isolated and two spare channels. 

I'm using the non-isolated for RTD temperature and the other two for PH and electrical conductivity (total dissolved solids). Normally the spare channels would be used for dosing pumps but I've repurposed one for dissolved oxygen by adding an additional isolated carrier board. Something similar can be done with channel 5.

* [Whitebox Labs Tentacle T3](https://www.atlas-scientific.com/product_pages/components/tentacle-t3.html)
* [Electrically Isolated EZO™ Carrier Board](https://www.atlas-scientific.com/product_pages/components/single_carrier_iso.html)
  * [EZO RTD](https://www.atlas-scientific.com/product_pages/circuits/ezo_rtd.html)
  * [EZO PH](https://www.atlas-scientific.com/product_pages/circuits/ezo_ph.html)
  * [EZO EC](https://www.atlas-scientific.com/product_pages/circuits/ezo_ec.html)
  * [EZO DO](https://www.atlas-scientific.com/product_pages/circuits/ezo_do.html)
  * [Adafruit AS7262 6-Channel Visible Light / Color Sensor Breakout](https://www.adafruit.com/product/3779)

![Sensor](/images/hydro_sensor_bb.png)

### Dosing
Adafruit offers a 12V DC motor controller HAT with four channels. I'm using those for PH up, PH down and two nutrient solutions.

* [Adafruit DC & Stepper Motor HAT for Raspberry Pi](https://www.adafruit.com/product/2348)
  * [Peristaltic Liquid Pump](https://www.adafruit.com/product/1150 )

![Dosing](/images/hydro_12V_PWM_bb.png)

### Chillers and Pumps
The Adafruit HAT is great for 12VDC PWM but isn't designed to switch lager loads. For that I'm using a MOSFET board.

* [Diymore 4 Channels 4 Route MOSFET](https://www.amazon.com/Diymore-Channels-MOSFET-Button-Arduino/dp/B01MRQFYJN/ref=asc_df_B01MRQFYJN/?tag=hyprod-20&linkCode=df0&hvadid=198109700569&hvpos=1o3&hvnetw=g&hvrand=1418185042287151470&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9007347&hvtargid=pla-385355383830&psc=1)
  * [IceProbe Thermoelectric Aquarium Chiller](https://smile.amazon.com/IceProbe-Thermoelectric-Aquarium-Chiller/dp/B001JSVLBO/ref=cm_cr_arp_d_product_top?ie=UTF8)
  * [12v Submersible Water Pump 206 GPH](https://www.amazon.com/dp/B01816E1YU/ref=psdc_402303011_t2_B01267CT80?th=1)

![Chillers and Pumps](/images/hydro_12V_DC_bb.png)

### Lights and Air Pumps
For switching line voltage devices such as lights and air pumps I'm using a relay board.

* [CAMDEC Inc Raspberry PI Expansion Board, Relays Board](https://www.amazon.com/CAMDEC-Inc-Raspberry-Expansion-Automation/dp/B071ND1FMR/ref=sr_1_1?s=electronics&ie=UTF8&qid=1547461584&sr=1-1&keywords=CAMDEC+Inc)

![Lights and Air Pumps](/images/hydro_120VAC_bb.png)

### Power
A quick review of the power budget says I'm going to need more than just a wall adapter. Main power comes from a 12 VDC supply then we step down to 5 VDC with a buck converter for the Raspberry Pi.

* [SUPERNIGHT 12V 30A Switching Power Supply, 110-240 Volt AC to DC 360W Universal Regulated Switching Transformer](https://smile.amazon.com/SUPERNIGHT-Switching-Universal-Regulated-Transformer/dp/B01LATMSGS/ref=sr_1_20?ie=UTF8&qid=1547384587&sr=8-20&keywords=12vdc+power+supply)
* [ZYAMY 12A High Power DC-DC Buck Converter Adjustable Step Down Power Supply Module 4.5-30V to 1.2-30V ](https://smile.amazon.com/dp/B07GGRCCRL/ref=sspa_dk_detail_0?psc=1)
