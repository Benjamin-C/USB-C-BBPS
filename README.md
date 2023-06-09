# USB-C-BBPS
A USBC-PD powered breadboard power supply with selectable voltage outputs. This lets you power your project with 3.3V and/or a voltage of your choice provided by a USBC Power Delivery capable power supply.

![Front render](https://github.com/Benjamin-C/USB-C-BBPS/blob/main/graphics/v1.0-render-front.png?raw=true)
![Front render](https://github.com/Benjamin-C/USB-C-BBPS/blob/main/graphics/v1.0-render-back.png?raw=true)

## Ratings
* VBUS has a 1.5A polyfuse, so no more than 1.5A may be drawn between the VBUS output and 3.3V regulator.
* Do not feed power back into either 3.3V or VBUS. Doing so may kill the board or possibly the USB power supply
* Each side of the board has a maximum of 1A. This is not regulated on the board, so don't draw more than that.

## Configuration
### VBUS selection:
|      | SW3 | SW2 | SW1 |
|------|-----|-----|-----|
| 5V   |  A  |  A  |  A  |
| 9V   |  A  |  A  |  B  |
| 12V* |  A  |  B  |  A  |
| 15V  |  A  |  B  |  B  |
| 20V  |  B  |  x  |  x  |

\* 12V is an optional part of the USBC-PD spec, so many laptop chargers including most Apple ones do not support 12V.

### Output Voltage Selection
* Use the 3-pin jumpers on each side of the board to select the voltage output to that side of the breadboard.
* Each side can be independently selected to be 3.3V or VBUS.
* Only 1 VBUS value may be used at a time.
* For any voltage over 5V, one or more of the output voltage monitoring LEDs will be lit. The current output voltage is the highest value with a lit LED.

### Errors
* If the board is not able to negotiate at least the desired voltage from the upstream power supply, the outputs will be turned off and the fault LED will be turned on.
* If the polyfuse is tripped, all lights on the board will turn off. To reset the polyfuse, turn disconnect power from the board, remove the cause of the over current event, and return power to the board.
* If there is a larger over current event, the protection in the USBC power supply may be triggered before the polyfuse reacts. To fix this, disconnect power from the board, remove the source of the nonrecurrent event, then reconnect power to the board.
* If the 3.3V light and voltage monitoring lights are blinking but the VBUS light is on, this is an indication that the 3.3V regulator may be damaged and require replacement.

## Assembly
* Mount the switch so that the switches are "on" when the switch is towards the bottom of the board and "off" when the switch is towards the top of the board. A "A" state is when the switch is down towards the bottom of the board (connected), and a "B" state is when the switch is towards the top of the board (disconnected)
* Be sure to securely solder the mounting tabs on the USBC connector to prevent damage to the board if the cable is pulled.

## More features!
* The 3 pin connector near the USBC connector exposes the I2C lines from the [CYPD3177-24LQXQT](https://www.infineon.com/cms/en/product/universal-serial-bus/usb-c-charging-port-controllers/ez-pd-barrel-connector-replacement-bcr/cypd3177-24lqxqt/) USBC PD Interface IC, and can be connected to a microcontroller for additional features.

## Design notes
This board was designed entirely by me based on the reference schematics for the utilized ICs.

