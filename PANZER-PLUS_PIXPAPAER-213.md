## Overview

## Hardware Preparison

Based on the PANZER-PLUS hardware design, SPI interface support was not originally included. However, you have three options to use the SPI interface on PANZER-PLUS: <br>

- Manually rework the J6 connector on the PCBA by connecting the wires on both ends of the IC and pulling a 3.3V wire to PIN 1, modifying J6 as shown in the diagram below. <br>
**Step 1. Remove component U131.** <br>
**Step 2. Connect pin 26 of the removed component's footprint to pin 40, pin 34 to pin 20, pin 33 to pin 21, and pin 25 to pin 5.** <br>
**Step 3. Connect a 3.3V power source to pin 1 of JP2.** <br>
<img src="https://github.com/user-attachments/assets/d078649b-6386-4ebc-ab80-e8636ebd399e" width="250">
<img src="https://github.com/user-attachments/assets/a295b2cd-11bd-4b92-9a99-4f7116dfa3cf" width="480">

- Purchase reworked hardware directly from us.
- Use an external USB-to-SPI dongle.

Next, connect the PIXPAPER-213's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

![image](https://github.com/user-attachments/assets/af657fcd-c5c5-4a54-b7a7-40c95f902b9c)
![image](https://github.com/user-attachments/assets/6ae059a1-9711-4d93-b800-46bffb24d128)

The PANZER-PLUS PCBA can be connected as follows JP2 & JP3 mapping:

JP2

![image](https://github.com/user-attachments/assets/c8c17f15-2931-46ce-b59c-35a7c2ab32fb)


JP3 (EXT_GPIO8=DC#, EXT_GPIO6=RST#, EXT_GPIO4=BUSY)

![image](https://github.com/user-attachments/assets/85ae632d-a87e-4bb6-906d-dba9d6b1c32b)


## Driver Installation instructions

## User-Space Utility instructions
