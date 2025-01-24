[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

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

Next, connect the PIXPAPER-213-C's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

![image](https://github.com/user-attachments/assets/af657fcd-c5c5-4a54-b7a7-40c95f902b9c)
![image](https://github.com/user-attachments/assets/6ae059a1-9711-4d93-b800-46bffb24d128)

The PANZER-PLUS PCBA can be connected as follows JP2 & JP3 mapping:

JP2

![image](https://github.com/user-attachments/assets/c8c17f15-2931-46ce-b59c-35a7c2ab32fb)


JP3 (EXT_GPIO8=DC#, EXT_GPIO6=RST#, EXT_GPIO4=BUSY)

![image](https://github.com/user-attachments/assets/85ae632d-a87e-4bb6-906d-dba9d6b1c32b)


## Driver Installation instructions

|Kernel|Tested|
|---|---|
| 6.6 |&#10004;|
| 5.15 |&#10004;|

Step 1. Download the kernel source and modify the target device tree file: imx8mp-b643-ppc.dts <br>
Step 2. Merge the patch as follows modification, a quick way is download these code as a patch, then use git apply into the kernel source.<br>

```diff
diff --git a/arch/arm64/boot/dts/freescale/imx8mp-b643-ppc.dts b/arch/arm64/boot/dts/freescale/imx8mp-b643-ppc.dts
index 0079ffc2501b..dd6fb8cdb8ba 100755
--- a/arch/arm64/boot/dts/freescale/imx8mp-b643-ppc.dts
+++ b/arch/arm64/boot/dts/freescale/imx8mp-b643-ppc.dts
@@ -198,13 +198,13 @@ lte_reset {
        };
 };

-&ecspi2 {
+&ecspi1 {
        #address-cells = <1>;
        #size-cells = <0>;
-       fsl,spi-num-chipselects = <1>;
+       num-cs = <1>;
        pinctrl-names = "default";
-       pinctrl-0 = <&pinctrl_ecspi2 &pinctrl_ecspi2_cs>;
-       cs-gpios = <&gpio5 13 GPIO_ACTIVE_LOW>;
+       pinctrl-0 = <&pinctrl_ecspi1 &pinctrl_ecspi1_cs>;
+       cs-gpios = <&gpio5 9 GPIO_ACTIVE_LOW>;
        status = "okay";

        spidev1: spi@0 {
@@ -616,15 +616,6 @@ &uart2 {
        status = "okay";
 };

-&uart3 {
-       pinctrl-names = "default";
-       pinctrl-0 = <&pinctrl_uart3>;
-       assigned-clocks = <&clk IMX8MP_CLK_UART3>;
-       assigned-clock-parents = <&clk IMX8MP_SYS_PLL1_80M>;
-       fsl,uart-has-rtscts;
-       status = "okay";
-};
-
 &usb3_phy0 {
        status = "okay";
 };
@@ -950,12 +941,17 @@ MX8MP_IOMUXC_UART2_TXD__UART2_DCE_TX      0x49
                >;
        };

-       pinctrl_uart3: uart3grp {
+       pinctrl_ecspi1: ecspi1grp {
                fsl,pins = <
-                       MX8MP_IOMUXC_ECSPI1_SCLK__UART3_DCE_RX          0x140
-                       MX8MP_IOMUXC_ECSPI1_MOSI__UART3_DCE_TX          0x140
-                       MX8MP_IOMUXC_ECSPI1_SS0__UART3_DCE_RTS          0x140
-                       MX8MP_IOMUXC_ECSPI1_MISO__UART3_DCE_CTS         0x140
+                       MX8MP_IOMUXC_ECSPI1_SCLK__ECSPI1_SCLK           0x140
+                       MX8MP_IOMUXC_ECSPI1_MOSI__ECSPI1_MOSI           0x140
+                       MX8MP_IOMUXC_ECSPI1_MISO__ECSPI1_MISO           0x140
+               >;
+       };
+
+       pinctrl_ecspi1_cs: ecspi1cs {
+               fsl,pins = <
+                       MX8MP_IOMUXC_ECSPI1_SS0__GPIO5_IO09                     0x140
                >;
        };
```

Step 3. Recompile the kernel and copy the new dtb file to the boot partition instead of the old one. <br>
Step 4. Boot up the system and checking the device node is exist or not <br>

    ls /dev/spidev1.0
    

## User-Space Utility instructions (Linux OS)

Step 1. Install necessary packages

        Ubuntu/Debian:
        $ sudo apt install gpiod libgpiod-dev

        Yocto:
        Need add the line in machine conf file as following:
        IMAGE_INSTALL_append = " libgpiod"



Step 2. Please download the utility source code in the rootfs of PANZER-PLUS, then compile it and execute the compiled executable file.

        PIXPAPER-213-C:
        # wget https://raw.githubusercontent.com/wigcheng/open-epd/refs/heads/master/2.13/color/spi/pixpaper-213-c-test-imx8mp.c
        # gcc -o epd_test pixpaper-213-c-test-imx8mp.c -lgpiod
        # ./epd_test

        Note that if your wired connection is different with chapter 1 "Hardware Preparison", especially DC# PIN, RST# PIN, and BUSY PIN,
        please modify the specific macros definition of pixpaper-213-c-test-imx8mp.c:

        #define EPD_GPIO_CHIP "gpiochip5"
        #define EPD_DC_PIN 15
        #define EPD_RST_PIN 13
        #define EPD_BUSY_PIN 11


Expection results: <br>
final image is some procgress bar with black background <br>
![ezgif-4-6446ab9a4e](https://github.com/user-attachments/assets/224ee0a3-6eda-4a69-8ffe-28d9f717d7a8)


        
Step 3. If I need change a new image for PIXPAPER-213-C, how to update the image raw data.

        Download the PNG to RAW converter base on python3, remember to install opencv package first
        $ sudo apt install python3-opencv
        $ wget https://raw.githubusercontent.com/wigcheng/open-epd/refs/heads/master/2.13/color/spi/png2epd.py

        Then, rename your PNG file as test.png, and excute the python script
        $ python3 png2epd.py

        It will generate a output file: test012_HEX.txt, the copy the content and paste to img_hex array of jd79661-epd-image-imx8mp.c instead of old array data.



## Contributors

Thanks goes to these wonderful people from open source community:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/wigcheng"><img src="https://avatars.githubusercontent.com/u/7148592?v=4" width="100px;" alt="Wig Cheng"/><br /><sub><b>Wig Cheng</b></sub></a><br /><a href="https://github.com/wigcheng/open-epd/commits?author=wigcheng" title="Code">💻</a></td>
<td align="center" valign="top" width="14.28%"><a href="https://github.com/meteorTriangle"><img src="https://avatars.githubusercontent.com/u/87787306?v=4" width="100px;" alt="Triangle Alien"/><br /><sub><b>Triangle Alien</b></sub></a><br />💻</td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

---
