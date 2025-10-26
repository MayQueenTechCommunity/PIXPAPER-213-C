<img src="https://www.mayqueentech.com/img/logo.png" width="100" align="right">
<br>

 ### MayQueen introduces PIXPAPER-213-C
A 2.13 inch prototype 4-color Electronic Paper Display (EPD) module, in collaboration with Triangle Alien Studio for the first time, showcasing craftsmanship and excellent hardware quality.<br>
It is based on an SPI interface and is fully compatible with our NXP edge fanless AIoT computing solutions.<br>
We will gradually port it to more embedded platforms, so this page will be updated periodically!

----------------------


#### Overview
|                         Model                         | SKU.                                                  |                       Driver support                       |
| :----------------------------------------------------------: | :----------------------------------------------------------- | :---------------------------------------------------------| 
| <img src="https://github.com/user-attachments/assets/eee65e6d-8fb5-4698-9081-32c951031dab" width="200"> | **PIXPAPER-213-C (Color)** <br />  | ARM MPU platform <br> ARM MCU platform <br> RISC-V MCU platform |


|                         Specifications                         |                                                   |
| :----------------------------------------------------------: | :----------------------------------------------------------- |
| Screen size | 2.13 inch |
| Resolution | 250x122 |
| Color | black, white, yellow, red |
| PPI | 130.6 |
| Active area | 23.7046×48.55(mm) |
| Interface | SPI |
| Partial update | NO |
| PINOUT | 3.3V, GND, MOSI, SCK, CS#, DC#, RST#, BUSY (DC#, RST#, BUSY are GPIOs)|
| Enclosure | Plastic using 3D printer |
|Operating temperature| 0-40 ℃ |

----------------------

#### MPU Supported Platforms (ARM64)

| **Platform** | <a href="https://www.renesas.com/" target="_blank"><br> <img src="https://www.macnica.com/apac/galaxy/zh_tw/products-support/products/renesas.coreimg.jpeg/structure/_jcr_content/root/container/container/bannerimage/1653236359047.jpeg" width="" height="100" /></a> | Status |<a href="https://www.nxp.com/" target="_blank"><br> <img src="https://github.com/TechNexion-Vision/.github/assets/28101204/67cc61c0-6bb7-44d5-889a-1ba5d4c0b9b5" width="" height="80" /></a> | Status | <a href="https://www.telechips.com/" target="_blank"><img width="" height="90" alt="image" src="https://github.com/user-attachments/assets/4f260b12-4d99-42e3-b9bd-6b90b2bbec16" /> | Status |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| **Porting Guide** | [KAKIP SBC(RZ/V2H)](https://github.com/MayQueenTechCommunity/PIXPAPER-213/blob/main/KAKIP_PIXPAPAER-213-C.md) | &#10004;  |  [PANZER-PLUS(IMX8MP)](https://github.com/MayQueenTechCommunity/PIXPAPER-213/blob/main/PIXPAPER-213-C_PIXPAPAER-213-C.md) <br> [FRDM-IMX93(IMX93)](https://github.com/MayQueenTechCommunity/PIXPAPER-213/blob/main/FRDM-IMX93_PIXPAPAER-213-C.md) | &#10004; <br> &#10004;| [TOPST D3-G(Dolphin 3M)](https://github.com/MayQueenTechCommunity/PIXPAPER-213/blob/main/D3G_PIXPAPAER-213-C.md) | &#10004; |

| **Platform** | <a href="https://www.rockchip.com/" target="_blank"><br> <img src="https://github.com/user-attachments/assets/6c51be9a-8cc4-4077-b67d-f1f72890f623" width="200" height="100" /></a> | Status |
| ---- | ---- | ---- |
| **Porting Guide** | [CUBE-RK3588(RK3588)](https://github.com/MayQueenTechCommunity/PIXPAPER-213/blob/main/CUBE-RK3588_PIXPAPAER-213-C.md) | &#10004;  |

#### MPU Supported Platforms (ARM32)

| **Platform** | <a href="https://www.raspberrypi.com/" target="_blank"><br> <img src="https://camo.githubusercontent.com/fc8b5f8e2e02a0e81be9f9ae53bdf674c2a730f55345c6df533ed0e319804095/68747470733a2f2f7777772e72617370626572727970692e636f6d2f6170702f75706c6f6164732f323032322f30322f434f4c4f55522d5261737062657272792d50692d53796d626f6c2d526567697374657265642e706e67" width="" height="120" /></a> | Status |
| ---- | ---- | ---- |
| **Porting Guide** | [Raspberry PI 2 Model B](https://github.com/MayQueenTechCommunity/PIXPAPER-213-C/blob/main/RPI2_PIXPAPAER-213-C.md)| &#10004;  |

#### MCU Supported Platforms (ARM32)

| **Platform** | <a href="https://www.raspberrypi.com/" target="_blank"><br> <img src="https://camo.githubusercontent.com/fc8b5f8e2e02a0e81be9f9ae53bdf674c2a730f55345c6df533ed0e319804095/68747470733a2f2f7777772e72617370626572727970692e636f6d2f6170702f75706c6f6164732f323032322f30322f434f4c4f55522d5261737062657272792d50692d53796d626f6c2d526567697374657265642e706e67" width="" height="120" /></a> | Status | <a href="https://www.nxp.com/" target="_blank"><br> <img src="https://github.com/TechNexion-Vision/.github/assets/28101204/67cc61c0-6bb7-44d5-889a-1ba5d4c0b9b5" width="" height="80" /></a> | Status |
| ---- | ---- | ---- | ---- | ---- |
| **Porting Guide** | [Raspberry PI Pico](https://github.com/MayQueenTechCommunity/PIXPAPER-213/blob/main/RPI-PICO_PIXPAPAER-213-C.md) | &#10004; | [FRDM-IMX93(M33)](https://github.com/MayQueenTechCommunity/PIXPAPER-213/blob/main/FRDM-IMX93-M33_PIXPAPAER-213-C.md) | &#10004; |

----------------------
#### INTRO. video
[![PIXPAPER-213-C](https://res.cloudinary.com/marcomontalbano/image/upload/v1741367072/video_to_markdown/images/youtube--Of7b3zhF5BQ-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/Of7b3zhF5BQ?si=HYnkLzXCjnIHI1I5 "PIXPAPER-213-C")

----------------------
#### Price and Availability
PIXPAPER-213-C is now available through direct sales (www.mayqueentech.com).
PIXPAPER-213-C is offered in a variety of configurations starting from $29 for 1pc order.
Detailed ordering and pricing information is available on sales contact window.
<br>

#### About MayQueen Technologies
MayQueen Technologies is a leading designer and manufacturer of ARM based embedded computing products since 2015.
MayQueen Technologies products are used in digital signage, telecommunication, industrial PC, gaming, medical devices, aerospace and marine systems and countless other applications.
MayQueen Technologies offices are located in Sheffield, U.K. and Taoyuan, Taiwan.
<br>

#### For additional details please contact:

International Sales: Grace To
<br> 
sales@mayqueentech.com 
