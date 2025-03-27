[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

## Overview

## Hardware Preparison

Because [FRDM-IMX93 - Single Board Computer](https://youtu.be/ZpD9j6_nsNI?si=w4PjBL8ydYqj8hmg) has a 40-PIN pin header and compatible with Raspberry PI, so it has one SPI interface can be used.

Different with previously, we will running the e-paper demo on Cortex-M33 core.

Firstly, connecting the PIXPAPER-213-C's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

![image](https://github.com/user-attachments/assets/af657fcd-c5c5-4a54-b7a7-40c95f902b9c)
![image](https://github.com/user-attachments/assets/6ae059a1-9711-4d93-b800-46bffb24d128)



Then, connect to the FRDM-IMX93 specific PINs of 40-PIN header as follows:

<img src="https://github.com/user-attachments/assets/af0d0f76-5212-4ceb-ab12-6904166d30d0" width="600"> <br>
<img src="https://github.com/user-attachments/assets/deae640f-062d-47e9-8889-c7c233c8f22b" width="400">




## Firmware Installation instructions

|FreeRTOS|Tested|
|---|---|
| SDK_24_12_00 |&#10004;|

Please download our sample code and compile as elf file

Ubuntu Host PC (20.04 or above):

    Step 1. Package pre-installation
    $ sudo apt install cmake git

    Step 2. Download the source code
    $ git clone https://github.com/open-EPD/frdm-imx93_m33.git

    Step 3. Download the toolchain
    filename: arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi.tar.xz

    Step 4. Compiling the source
    $ export ARMGCC_DIR=/opt/m33/toolchain
    $ cd <source directory>/boards/mcimx93evk/driver_examples/lpspi/pixpaper-213/master/armgcc
    $ ./build_release.sh

    Step 5. Output firmware file
    $ ./release/lpspi_polling_b2b_transfer_master.elf

    Step 6. Rename your firmware file name (optional)
    $ mv lpspi_polling_b2b_transfer_master.elf pixpaper-c-213-demo.elf

Ubuntu 24.04 on Cortex-A55 (NEW):

![image](https://github.com/user-attachments/assets/6c15672a-58ef-4915-bffd-0efb9e5599c5)


    Step 1. Package pre-installation
    $ sudo apt install cmake

    Step 2. Download the source code
    $ git clone https://github.com/open-EPD/frdm-imx93_m33.git

    Step 3. Download the toolchain
    filename: arm-gnu-toolchain-12.2.mpacbti-rel1-aarch64-arm-none-eabi.tar.xz
    decompress and move to under /opt/m33/ and rename toolchain folder

    Step 4. Compiling the source
    $ export ARMGCC_DIR=/opt/m33/toolchain
    $ cd <source directory>/boards/mcimx93evk/driver_examples/lpspi/pixpaper-213/master/armgcc
    $ ./build_release.sh

    Step 5. Output firmware file
    $ ./release/lpspi_polling_b2b_transfer_master.elf

    Step 6. Rename your firmware file name (optional)
    $ mv lpspi_polling_b2b_transfer_master.elf pixpaper-c-213-demo.elf

## Firmware Running instructions on Linux OS

Step 1. Move compiled firmware to FRDM-IMX93's Linux OS via network, USB storage, etc.

Step 2. Setting the environment for remoteproc function

        $ echo -n /home/ubuntu/ > /sys/module/firmware_class/parameters/path (Yocto no need this commnad)
        $ echo -n pixpaper-c-213-demo.elf > /sys/class/remoteproc/remoteproc0/firmware

Step 3. Starting the remoteproce, load assigned firmware on M33 core

        $ echo -n start > /sys/class/remoteproc/remoteproc0/state

        If you want to stop the running firmware on M33 core, issue the stop command
        $ echo -n stop > /sys/class/remoteproc/remoteproc0/state


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
