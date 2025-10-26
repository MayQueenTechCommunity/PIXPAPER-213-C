[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

## Overview

## Hardware Preparison

Based on the [CUBE-RK3588](https://github.com/MayQueenTechCommunity/CUBE-RK3588) hardware design, SPI interface support was not originally included. However, you have a option to use the SPI interface from UART interfaces on CUBE-RK3588: <br>



![image](https://github.com/user-attachments/assets/af657fcd-c5c5-4a54-b7a7-40c95f902b9c)
![image](https://github.com/user-attachments/assets/6ae059a1-9711-4d93-b800-46bffb24d128)

The CUBE-RK3588 SPI can be connected as follows COM1 & COM2 mapping:
<img width="536" height="401" alt="image" src="https://github.com/user-attachments/assets/b55fde25-bec6-4431-8a2b-a6f5b1d2e876" />



## Driver Installation instructions

|Kernel|Tested|
|---|---|
| 6.1 |&#10004;|

Step 1. Download the kernel source and modify the target device tree file: rk3588-b675.dts <br>
Step 2. Merge the patch as follows modification from UART to SPI, a quick way is download these code as a patch, then use git apply into the kernel source.<br>

```diff
diff --git a/arch/arm64/boot/dts/rockchip/rk3588-b675.dts b/arch/arm64/boot/dts/rockchip/rk3588-b675.dts
index caf79a6b1505..7a4bb47d0141 100644
--- a/arch/arm64/boot/dts/rockchip/rk3588-b675.dts
+++ b/arch/arm64/boot/dts/rockchip/rk3588-b675.dts
@@ -1250,13 +1250,11 @@ &u2phy3_host {
 };
 
 &uart5 {
-	status = "okay";
-	pinctrl-0 = <&uart5m0_xfer &uart5m0_ctsn &uart5m0_rtsn>;
+	status = "disabled";
 };
 
 &uart6 {
-	status = "okay";
-	pinctrl-0 = <&uart6m1_xfer &uart6m1_ctsn &uart6m1_rtsn>;
+	status = "disabled";
 };
 
 &uart9 {
@@ -1528,3 +1526,16 @@ &sdio {
 &dmc {
 	status = "disabled";
 };
+
+&spi4 {
+	status = "okay";
+	pinctrl-names = "default";
+	pinctrl-0 = <&spi4m2_pins>;
+	cs-gpios = <&gpio4 RK_PD4 GPIO_ACTIVE_LOW>;
+	num-cs = <1>;
+	spi_test@0 {
+		compatible = "rockchip,spidev";
+		reg = <0>;
+		spi-max-frequency = <5000000>;
+	};
+};
-- 
```

Step 3. Recompile the kernel and copy the new dtb file to the boot partition instead of the old one. <br>
Step 4. Boot up the system and checking the device node is exist or not <br>

    ls /dev/spidev4.0
    

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

        It will generate a output file: png_HEX.h, the copy the same folder witth pixpaper-213-c-test-imx8mp.c.
        Note that this step can running on host PC side or target board, but png_HEX.h must be put into the folder with c file together before 
        compiling.

        Download a sample header file:
        $ wget https://raw.githubusercontent.com/open-EPD/user-space-examples/refs/heads/master/2.13/color/spi/png_HEX.h


Step 3. Please download the utility source code in the rootfs of CUBE-RK3588, then compile it and execute the compiled executable file.

        PIXPAPER-213-C:
        # wget https://github.com/open-EPD/user-space-examples/raw/refs/heads/master/2.13/color/spi/pixpaper-213-c-test-rk3588.c
        # gcc -o epd_test pixpaper-213-c-test-rk3588.c -lgpiod
        # ./epd_test

        Note that if your wired connection is different with chapter 1 "Hardware Preparison", especially DC# PIN, RST# PIN, and BUSY PIN,
        please modify the specific macros definition of pixpaper-213-c-test-imx8mp.c:

        #define EPD_GPIO_CHIP "gpiochip4"
        #define EPD_DC_PIN 26
        #define EPD_RST_PIN 27
        #define EPD_BUSY_PIN 29


Expection results: <br>
final image is some procgress bar with black background <br>
![ezgif-4-6446ab9a4e](https://github.com/user-attachments/assets/224ee0a3-6eda-4a69-8ffe-28d9f717d7a8)


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
