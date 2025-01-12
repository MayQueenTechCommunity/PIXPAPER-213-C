<img src="https://www.mayqueentech.com/img/logo.png" width="100" align="right">
<br>

 ### MayQueen introduces PIXPAPER-213
A 2.13 inch prototype Electronic Paper Display (EPD) module, Coop Triangle Alien Studio.
It is based on an SPI interface and is fully compatible with our NXP edge fanless AIoT computing solutions.
We will gradually port it to more embedded platforms, so this page will be updated periodically!



#### Overview
|                         Model                         | SKU.                                                  |                       Driver support                       |
| :----------------------------------------------------------: | :----------------------------------------------------------- | :---------------------------------------------------------| 
| <img src="https://github.com/user-attachments/assets/eee65e6d-8fb5-4698-9081-32c951031dab" width="200"> | **PIXPAPER-213-C (Color)** <br />   **PIXPAPER-213-M (Mono)**  | ARM MPU platform <br> ARM MCU platform <br> X86 PC (**coming soon**) |


|                         Specifications                         |                                                   |
| :----------------------------------------------------------: | :----------------------------------------------------------- |
| Screen size | 2.13 inch |
| Resolution | 250x122 |
| DPI | 130 |
| Active area | 23.7046×48.55(mm) |
| Interface | SPI |
| Partial update | PIXPAPER-213-C: NO <br> PIXPAPER-213-M: YES |
| PINOUT | 3.3V, GND, MOSI, SCK, CS#, DC#, RST#, BUSY (DC#, RST#, BUSY are GPIOs)|
|Operating temperature| 0-40 ℃ |

#### MPU Supported Platforms

| **Platform** | <a href="https://www.renesas.com/" target="_blank"><br> <img src="https://www.macnica.com/apac/galaxy/zh_tw/products-support/products/renesas.coreimg.jpeg/structure/_jcr_content/root/container/container/bannerimage/1653236359047.jpeg" width="" height="100" /></a> | Status |<a href="https://www.nxp.com/" target="_blank"><br> <img src="https://github.com/TechNexion-Vision/.github/assets/28101204/67cc61c0-6bb7-44d5-889a-1ba5d4c0b9b5" width="" height="80" /></a> | Status |
| ---- | ---- | ---- | ---- | ---- |
| **Porting Guide** | Coming soon | &#x23F3;  |  [PANZER-PLUS(IMX8MP)](https://github.com/MayQueenTechCommunity/PANZER-PLUS-EPD) <br> Mecha Compat (Coming soon) | &#10004; <br> &#x23F3;|


#### MCU Supported Platforms

| **Platform** | <a href="https://www.renesas.com/" target="_blank"><br> <img src="https://camo.githubusercontent.com/fc8b5f8e2e02a0e81be9f9ae53bdf674c2a730f55345c6df533ed0e319804095/68747470733a2f2f7777772e72617370626572727970692e636f6d2f6170702f75706c6f6164732f323032322f30322f434f4c4f55522d5261737062657272792d50692d53796d626f6c2d526567697374657265642e706e67" width="" height="120" /></a> | Status |
| ---- | ---- | ---- |
| **Porting Guide** | Raspberry PI Pico | &#10004; |
