![image](https://github.com/user-attachments/assets/c2cb952e-7385-4665-9877-0b3269abaa0c)


[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

## Overview

## Hardware Preparison

Because [Kakip AI-Single Board Computer](https://www.kakip.ai/) has a 40-PIN pin header and compatible with Raspberry PI, so it has one SPI interface can be used.

Firstly, connecting the PIXPAPER-213-C's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

![image](https://github.com/user-attachments/assets/af657fcd-c5c5-4a54-b7a7-40c95f902b9c)
![image](https://github.com/user-attachments/assets/6ae059a1-9711-4d93-b800-46bffb24d128)

Then, connect to the Kakip specific PINs of 40-PIN header as follows:

<img src="https://github.com/user-attachments/assets/6362c17b-1d5d-4137-93dd-5e0041440099" width="400"> <br>
<img src="https://github.com/user-attachments/assets/98380f8c-72f4-44fb-a657-1628215f39a5" width="400">




## Driver Installation instructions

|Kernel|Tested|
|---|---|
| 6.1 | &#x23F3;|
| 5.10 |&#10004;|

Note that if your target OS is Ubuntu image revision V8 and above, it has device tree overlay function inside the image, no need modify any source code, please follows from Step 1-1.<br>
And if your target OS is Ubuntu image is lower revision, please it has to tweaked device tree file, follows from Step 2-1.

Step 1-1. **Device tree overlay method will be updated soon**

Step 2-1. Merge the patch as follows modification, a quick way is download these code as a patch, then use git apply into the kernel source.

```diff
diff --git a/arch/arm64/boot/dts/renesas/kakip-es1.dts b/arch/arm64/boot/dts/renesas/kakip-es1.dts
index 91555f3c3..09ea2bd0a 100644
--- a/arch/arm64/boot/dts/renesas/kakip-es1.dts
+++ b/arch/arm64/boot/dts/renesas/kakip-es1.dts
@@ -292,13 +292,12 @@ usb21_pins: usb21 {

        spi0_pins: spi0 {
                pinmux = <RZG2L_PORT_PINMUX(9, 1, 1)>, /* MISO */
-                        <RZG2L_PORT_PINMUX(9, 0, 1)>, /* MOSI */
-                        <RZG2L_PORT_PINMUX(9, 3, 1)>, /* SSL0 */
-                        <RZG2L_PORT_PINMUX(9, 4, 1)>, /* SSL0 */
-                        <RZG2L_PORT_PINMUX(9, 2, 1)>; /* RSPCK */
+                       <RZG2L_PORT_PINMUX(9, 0, 1)>, /* MOSI */
+                       <RZG2L_PORT_PINMUX(9, 2, 1)>, /* SSL0 */
+                       <RZG2L_PORT_PINMUX(9, 3, 1)>, /* SSL0 */
+                       <RZG2L_PORT_PINMUX(9, 4, 1)>; /* RSPCK */
        };
 };
-
 &extal_clk {
        clock-frequency = <24000000>;
 };
@@ -1349,6 +1348,14 @@ &spi0 {
        pinctrl-names = "default";

        status = "okay";
+
+    spi_dev0: spi@0 {
+        compatible = "rohm,dh2228fv";
+        pl022,com-mode = <1>;
+        spi-max-frequency = <10000000>;
+        reg = <0>;
+        status = "okay";
+    };
 };
```

Step 2-2. Recompile the kernel and copy the new dtb file to the /boot folder of  rootfs partition instead of the old one. <br>
Step 2-3. Boot up the system and checking the device node is exist or not <br>

    ls /dev/spidev0.0
 

## User-Space Utility instructions (Linux OS)

Step 1. Install necessary packages

        Ubuntu/Debian:
        $ sudo apt install gpiod libgpiod-dev

        Yocto:
        Need add the line in machine conf file as following:
        IMAGE_INSTALL_append = " libgpiod"



Step 2. Please download the utility source code in the rootfs of PANZER-PLUS, then compile it and execute the compiled executable file.

        PIXPAPER-213-C:
        # wget https://raw.githubusercontent.com/wigcheng/open-epd/refs/heads/master/2.13/color/spi/pixpaper-213-c-test-kakip.c
        # gcc -o epd_test pixpaper-213-c-test-kakip.c -lgpiod
        # ./epd_test

        Note that if your wired connection is different with chapter 1 "Hardware Preparison", especially DC# PIN, RST# PIN, and BUSY PIN, also can issue command 'gpioinfo' to check the gpip pin detail. 
        Please modify the specific macros definition of pixpaper-213-c-test-kakip.c:

        #define EPD_GPIO_CHIP "gpiochip0"
        #define EPD_DC_PIN 60
        #define EPD_RST_PIN 87
        #define EPD_BUSY_PIN 91


Expection results: <br>




https://github.com/user-attachments/assets/33c27ed3-f82c-435f-919b-019f91ef661a



        
Step 3. If I need change a new image for PIXPAPER-213-C, how to update the image raw data.

        Download the PNG to RAW converter base on python3, remember to install opencv package first
        $ sudo apt install python3-opencv
        $ wget https://raw.githubusercontent.com/wigcheng/open-epd/refs/heads/master/2.13/color/spi/png2epd.py

        Then, rename your PNG file as test.png, and excute the python script
        $ python3 png2epd.py

        It will generate a output file: test_HEX.txt, the copy the content and paste to img_hex array of jd79661-epd-image-kakip.c instead of old array data.

## Contributors

Thanks goes to these wonderful people from open source community:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/lc-wang"><img src="https://avatars.githubusercontent.com/u/125327848?v=4" width="100px;" alt="LC Wang"/><br /><sub><b>LC Wang</b></sub></a><br /><a href="https://github.com/wigcheng/open-epd/commits?author=lc-wang" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

---
