# Homebase

A home control panel with built-in thermostat features and Z-Wave base
functions.

## BOM

Below is a list of all the materials needed to build this project. I have
included links to the products that I bought but substitutes may be chosen for
certain parts. Parts that can be substituted will have `(*)` prepended to the
part name.

| Part                                                                                                 | Qty | Price |
| ---------------------------------------------------------------------------------------------------- | --- | ----- |
| [WaveShare 13.3" Display](https://www.waveshare.com/13.3inch-dsi-lcd.htm)                            | 1   | $157  |
| ([\*](#raspberry-pi)) [Raspberry Pi 3B+](https://www.pishop.us/product/raspberry-pi-3-model-b-plus/) | 1   | $35   |
| ([\*](#6-channel-relay-board)) [6 Channel Relay Board](https://a.co/d/0NnzUo6)                       | 1   | $10   |
| [Zooz 800 Z-Wave GPIO Module](https://a.co/d/3nAOChq)                                                | 1   | $23   |
| (\*) [BMP180 Board](https://a.co/d/gI1moHX)                                                          | 1   | $10   |
| (\*) [24V to 5V Buck Converter](https://a.co/d/9Pe8hRs)                                              | 1   | $15   |
| (\*) [60mm x 10mm x 3mm Magnets](https://a.co/d/hqvYCyN)                                             | 16  | $15   |
| (\*) [22awg Wire](https://a.co/d/0vo3LXO)                                                            | ?   | $15   |
| (\*) M3 Screws                                                                                       | ?   | ?     |
| (\*) M3 Screw Inserts                                                                                | ?   | ?     |

## Substitutions

### Raspberry Pi

I used a Raspberry Pi 3B+ because it's what I had lying around but from looking
at the dimensions of versions 4 and 5 they should also work. The screw pattern
just has to match as the software shouldn't care what version it runs on.

### 6 Channel Relay Board

My thermostat only had 6 wires that needed to be controlled. When you look at
your thermostat wiring if you have a C wire as is needed for most smart
thermostats that is not a wire that needs controlling so does not need to be
included in this count.

## Build Instructions

1. Print the provided drywall cutout template.

> [!WARNING]
> Still need to go through and finish/validate these steps.

### Circuit Diagram

![circuit](./diagrams/circuit.drawio.svg)
