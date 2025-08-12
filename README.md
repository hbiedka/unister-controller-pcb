## Dude, I need professional-looking PCB with <n> dry-contact relays, <m> 230V on/off relays, <x> inputs and <y> opto-isolated inputs

After ~10 similar projects I used to make using perfboards and PCBs etched at home I have created this PCB project to utillize it in as many automation projects as possible.

# What does it have

* 2.54 mm perfboard-like field for whatever you want
* 4 relays
  * NO/NC dry contact
  * fused AC output with N and PE split into 2 circuits protected by separated fuses 
* 8x terminal outputs for general purpose (6 of them can be easily connected to GND
* 2x optoinolated input
  * dry contact
  * low-voltage wet contact
  * AC wet contact
* AC to low voltage converted (12V, 5V or similar) using HiLink HLK series
* optional LDO or DC/DC converter (the net is called 5V but it can be any voltage by using proper LDO or converter)
* power LED diode

# Configuration and customisation options

## Relays

| Footprint | Dry contact output | Wet contact output (AC voltage out) |
|---|---|---|
| Kn_DRY (closer to relay) | Populate | Do not populate |
| Kn_230VAC (closer to edge) | Do not populate | Populate |
| KN_WET jumper | Do not populate | Populate using ~1mm^2 wire |

If you are using wet contact output(s), remember to populate F2 or F3 by fuse holder and provide a proper fuse. **Remember to select proper amperage based on fuse rate and wiring**

### Negative voltage controlled coils with common VCC voltage (recommended)
If you would like to use eg. NPN or MOSFET-N transistor to drive relay coils and supply it from Hi-Link supply voltage output:
* Short COM_RELAY with VCC - the best way is to use solder nieghbor points near D4
* Solder suppression diodes according to PCB symbol (bar is cathode)

### Negative voltage controlled coils with common LDO/converter output voltage
Like above, but short COM_RELAY to 5V net

### Positive voltage controlled coils with common ground
If you would like to use PNP or MOSFET-P transistors to drive relay coils:
* Short COM_RELAY with GND
* Solder suppression diodes **opposite to PCB symbol** (bar is anode)



## Optoisolated inputs

| Footprint | Dry contact (positive) | Dry contact (negative) | Wet contact (low voltage) | Wet contact (AC voltage) |
|---|---|---|---|---|
| J10/J11 | Solder 2-pole terminal to pins 1-2 (left), short pins 3-4 | Solder 2-pole terminal to pins 3-4 (right), short pins 1-2 | Solder 2-pole terminal to pins 2-3 (middle) | Solder 2-pole terminal to pins 2-3 (middle) |
| D6/D8 | Short | Short | Short | Populate |
| R3/R4 | Short | Short | Short | Populate |
| C4/C6 | Do not populate | Do not populate | Do not populate | Populate |
| D7/D9 | Do not populate | Do not populate | Do not populate | Populate |

For all cases:
* Populate R2/R5 - use proper resistance to provide suitable diode current with nominal voltage
* Use PC817 or similar transoptor

## Single DC voltage (no DC/DC or LDO)

Short pins 1 and 3 of U1
