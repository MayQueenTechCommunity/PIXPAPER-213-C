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


## Driver Installation instructions

## User-Space Utility instructions
