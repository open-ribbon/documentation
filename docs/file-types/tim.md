# TIM - PlayStation Image
The TIM format is a little endian-based image file format for the PlayStation. While their use varies from textures, UI elements and loading screens, Vib-Ribbon only uses them for the company logos when the game starts up. It's file structure mimics how textures are managed in the PlayStation's frame buffer. There are a limited amount of colors a TIM can use, but each file can use it's own 16 or 256 color palette, known as a color lookup table, or CLUT for short (16 and 24 bit color options are also avilable, but aren't used in Vib-Ribbon's textures.)

### Header

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | int16 | unk | Always 0x8000 |
| 0x02 | int16 | unk | Unused? Possible values: 1, 15, 20, 30, or 60 |
| 0x04 | uint16 | keyframeCount | |

## Logos
The only TIMs that are used in the game are at the beginning of MAIN\_T execution. They are located in `TITLE\FILES\MENU\LOGOS\`. Every TIM is a section of an image, and all of them get loaded and lined up to complete the image.

`SONY_X.TIM` Make up the "Sony Computer Entertainment Inc. Presents" screen. Uses a 16 color (4 BPP) palette. Only used in the Japan version. Is present in the PAL version, but goes unused (renamed to `01_SONY_X.TIM`)

**SONY_1 + 2.TIM**
<center><img src="../../img/TIMs/01_SONY_FULL.png"></img></center> 


`FE_SONY_X.TIM` Make up the "Sony Computer Entertainment Europe Presents" screen, along with a URL to the European PlayStation Website. Uses a 16 color (4 BPP) palette. Only present in the PAL version.

**FE_SONY_1 + 2.TIM**
<center><img src="../../img/TIMs/FE_SONY_FULL.png"></img></center> 


`7ON_X.TIM` Make up the NanaOn-Sha logo. Uses a 256 color (8 BPP) palette, but not all colors are used. The amount of colors in the palette are also different between all 4 TIM files. 

**7ON_1 + 2,3,4.TIM**
<center><img src="../../img/TIMs/7ON_FULL.png"></img></center> 
