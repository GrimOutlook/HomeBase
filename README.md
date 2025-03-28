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

```mermaid
graph LR;
    subgraph Thermostat Wires
        thermo_wire_red[Red: 24V Power]
        thermo_wire_blue[Blue: Common/Ground]
        thermo_wire_white[White: Heat]
        thermo_wire_yellow[Yellow: Air Conditioning]
        thermo_wire_green[Green: Fan]
        thermo_wire_orange[Orange: Heat Pump Reverse Valve]
        thermo_wire_brown[Brown: Second Stage Heating]
    end
    lever_block[10-Way Connector Lever Block]
    subgraph 6 Relay Board
        dc_plus[DC+]
        dc_min[DC-]
        subgraph Relay 1
            r1_no[NO]
            r1_com[COM]
            r1_in[IN]
        end
        subgraph Relay 2
            r2_no[NO]
            r2_com[COM]
            r2_in[IN]
        end
        subgraph Relay 3
            r3_no[NO]
            r3_com[COM]
            r3_in[IN]
        end
        subgraph Relay 4
            r4_no[NO]
            r4_com[COM]
            r4_in[IN]
        end
        subgraph Relay 5
            r5_no[NO]
            r5_com[COM]
            r5_in[IN]
        end
    end
    subgraph Screen
        subgraph Power Connector
            screen_pow_1[Pin 1: 5V]
            screen_pow_2[Pin 2: 5V]
            screen_gnd[Pin 3: GND]
        end
        screen_dsi_port[DSI Out Port]
    end
    subgraph Raspberry Pi
        subgraph Raspberry Pi GPIO
            gpio_pin2[Pin 2: 5V]
            gpio_pin3[Pin 3: I2C Data]
            gpio_pin4[Pin 4: 5V]
            gpio_pin5[Pin 5: I2C Clk]
            gpio_pin6[Pin 6: GND]
            gpio_pin9[Pin 9: GND]
            gpio_pin11[Pin 11: GPIO 17]
            gpio_pin13[Pin 13: GPIO 27]
            gpio_pin15[Pin 15: GPIO 22]
            gpio_pin19[Pin 19: GPIO 10]
            gpio_pin21[Pin 21: GPIO 9]
        end
        rpi_dsi_port[DSI In Port]
    end

    %% CONNECTIONS

    %% Thermostat Wire Outgoing Connections
    thermo_wire_red --> lever_block
    thermo_wire_white --> r1_no
    thermo_wire_yellow --> r2_no
    thermo_wire_green --> r3_no
    thermo_wire_orange --> r4_no
    thermo_wire_brown --> r5_no

    %% Lever Block Outgoing Connections
    lever_block --> r1_com
    lever_block --> r2_com
    lever_block --> r3_com
    lever_block --> r4_com
    lever_block --> r5_com

    %% Screen Outgoing Connections
    screen_pow_1 --> gpio_pin2
    screen_pow_2 --> gpio_pin4
    screen_gnd --> gpio_pin6
    screen_dsi_port --> rpi_dsi_port

    %% Raspberry Pi GPI Outgoing Connections
    gpio_pin2 --> dc_plus
    gpio_pin9 --> dc_min
    gpio_pin11 --> r1_in
    gpio_pin13 --> r2_in
    gpio_pin15 --> r3_in
    gpio_pin19 --> r4_in
    gpio_pin21 --> r5_in