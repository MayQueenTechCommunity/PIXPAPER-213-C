[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

## Overview

|Platform|Tested|
|---|---|
| Pico 2 | &#10004;|
| Pico |&#10004;|


## Hardware Preparison

Because [Raspberry Pi Pico 2](https://www.raspberrypi.com/products/raspberry-pi-pico-2/) has a generic pin header with one SPI interface can be used.

Firstly, connecting the PIXPAPER-213-C's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

![image](https://github.com/user-attachments/assets/af657fcd-c5c5-4a54-b7a7-40c95f902b9c)
![image](https://github.com/user-attachments/assets/6ae059a1-9711-4d93-b800-46bffb24d128)

Then, connect to the Raspberry Pi Pico 2 specific PINs of PIN header as follows:

<img src="https://github.com/user-attachments/assets/d5272a2f-a0cf-4cf8-a5ca-c44d774f407b" width="400"> <br>
|PIXPAPER-213-C Pinout|Pico Pin assignment|
|---|---|
| 3V3 | 3V3(OUT)|
| GND | GND|
| MOSI | GPIO19|
| SCK | GPIO18|
| CS | GPIO17|
| DC | GPIO16|
| RST | GPIO20|
| BUSY | GPIO21|

## Firmware Update

Step 1. Install necessary packages (Windows, Ubuntu host both work)

        1. VScode Studio
        2. open VScode and install pi pico extension


Step 2. Prepare the example code and import to VScode

        Download link
        $ git clone https://github.com/meteorTriangle/EPDA0213E5_4C

Step 3. Pressing compile and deploy button to flash the firmware to Pico, then it works

        Note that if your wired connection is different with chapter 1 "Hardware Preparison", especially DC# PIN, RST# PIN, and BUSY PIN.
        Please modify the specific macros definition of extern/EPDA0213E5_4C_RPIMCU_driver/epd_lib.h:

        // Pin definitions
        #define EPD_SPI_TX 19
        #define EPD_SPI_SCK 18
        #define EPD_SPI_CS 17
        #define EPD_DC 16
        #define EPD_RST 20
        #define EPD_BUSY 21


Expection results: <br>



https://github.com/user-attachments/assets/ef027c6a-ef98-40ca-92b4-272fc4898f1f




## Contributors

Thanks goes to these wonderful people from open source community:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
<td align="center" valign="top" width="14.28%"><a href="https://github.com/meteorTriangle"><img src="https://avatars.githubusercontent.com/u/87787306?v=4" width="100px;" alt="Triangle Alien"/><br /><sub><b>Triangle Alien</b></sub></a><br />💻</td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

---
