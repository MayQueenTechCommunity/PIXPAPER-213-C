[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

## Overview

## Hardware Preparison

[D3-G](https://topst.ai/product/g/d3), an AI Single Board Computer, which has a 40-PIN pin header and compatible with Raspberry PI, so it has some SPI interfaces can be used.

Firstly, connecting the PIXPAPER-213-C's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

![image](https://github.com/user-attachments/assets/af657fcd-c5c5-4a54-b7a7-40c95f902b9c)
![image](https://github.com/user-attachments/assets/6ae059a1-9711-4d93-b800-46bffb24d128)



Then, connect to the D3-G specific PINs of 40-PIN header as follows:

<img src="https://github.com/user-attachments/assets/d401dc80-7faa-4536-b914-a8caaaaeff19" width="600"> <br>
<img src="https://github.com/user-attachments/assets/deae640f-062d-47e9-8889-c7c233c8f22b" width="400">




## Driver Installation instructions

|Kernel|Tested|
|---|---|
| 6.6 |&#10004;|

Because there has a SPI interface on Linux already, so no need any tweaking in kernel space, just need to checking the device node is exist or not <br>

    ls /dev/spidev0.0
 

## User-Space Utility instructions (Linux OS)

Step 1. Install necessary packages

        Ubuntu/Debian:
        $ sudo apt install gpiod libgpiod-dev

        Yocto:
        Need add the line in machine conf file as following:
        IMAGE_INSTALL_append = " libgpiod"


Step 2. Prepare a 250x122 size picture what you want to showing, then make a image raw data based header file

        Download the PNG to RAW converter base on python3, remember to install opencv package first
        $ sudo apt install python3-opencv
        $ wget https://raw.githubusercontent.com/open-EPD/user-space-examples/refs/heads/master/2.13/color/spi/png2epd.py

        Then, rename your PNG file as test.png, and excute the python script
        $ python3 png2epd.py

        It will generate a output file: png_HEX.h, the copy the same folder witth pixpaper-213-c-test-frdm-imx93.c.
        Note that this step can running on host PC side or target board, but png_HEX.h must be put into the folder with c file together before 
        compiling.

        Download a sample header file:
        wget https://raw.githubusercontent.com/open-EPD/user-space-examples/refs/heads/master/2.13/color/spi/png_HEX.h


Step 3. Please download the utility source code in the rootfs of FRDM-IMX93 SBC, then compile it and execute the compiled executable file.

        PIXPAPER-213-C:
        # wget https://raw.githubusercontent.com/open-EPD/user-space-examples/refs/heads/master/2.13/color/spi/pixpaper-213-c-test-frdm-imx93.c
        # gcc -o epd_test pixpaper-213-c-test-frdm-imx93.c -lgpiod
        # ./epd_test

        Note that if your wired connection is different with chapter 1 "Hardware Preparison", especially DC# PIN, RST# PIN, and BUSY PIN, also can issue command 'gpioinfo' to check the gpip pin detail. 
        Please modify the specific macros definition of pixpaper-213-c-test-frdm-imx93.c:

        #define EPD_GPIO_CHIP "gpiochip0"
        #define EPD_DC_PIN 0
        #define EPD_RST_PIN 5
        #define EPD_BUSY_PIN 26


Expection results: <br>



https://github.com/user-attachments/assets/69581ec8-6681-477a-bca2-5b8315e38604






## Contributors

Thanks goes to these wonderful people from open source community:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
        <td align="center" valign="top" width="14.28%"><a href="https://github.com/wigcheng"><img src="https://avatars.githubusercontent.com/u/7148592?v=4" width="100px;" alt="Wig Cheng"/><br /><sub><b>Wig Cheng</b></sub></a><br /><a href="https://github.com/wigcheng/open-epd/commits?author=wigcheng" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

---
