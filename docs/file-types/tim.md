# TIM - PlayStation Image
The TIM format is a little endian-based image file format for the PlayStation. While their use varies from textures, UI elements and loading screens, Vib-Ribbon only uses them for the company logos when the game starts up. It's file structure mimics how textures are managed in the PlayStation's VRAM. There are a limited amount of colors a TIM can use, but each file can use it's own 16 or 256 color palette, known as a color lookup table, or CLUT for short (16 and 24 bit color options are also avilable, but aren't used in Vib-Ribbon's textures.)

## Header

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | int8 | ID | Always 0x10 |
| 0x01 | int8 | Version | Always 0x00 |
| 0x04 | int8 | Flag | Possible Values: 0, 1, 2, 3, 4, 8, 9 |

`Flag` determines the color depth of the image and if it has its own CLUT. 0-3 represents either 4, 8, 16 and 24-bit color modes. A value of 4 is used if the TIM contains multiple types of sprite and texture data that need to be intermingled. 8 represents a 4-bit color depth that has its own CLUT, and 9 means the same but for 8-bit color depth.

## CLUT Header

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | int32 | bnum | Said to be the data length of the CLUT, but doesn't seem to do anything |
| 0x04 | int16 | DX | X Coordinate for VRAM placement |
| 0x06 | int16 | DY | Y Coordinate for VRAM placement |
| 0x08 | int16 | H | Horizontal resolution for placing CLUT in VRAM |
| 0x08 | int16 | V | Virtical resolution for placing CLUT in VRAM |

`H` and `V` have to equal 16 for 4-bit color depth and 256 for 8-bit color depth when multiplied. Supposedly you can change the resolution of CLUT to where it's more of a rectangle than a 256 pixel long line, possibly saving some space, but doing so will make the other colors go unused so it's not recommended. Keep `H` set to 256/16 and `V` to 1.

## CLUT Data

Each color is recorded as a int16 value, but is read under binary. Each color is split into 5 bits, and the final bit is for transparency control, known as STP for short. Bits 0-4 are for Red, bits 5-9 are for Green, and bits 10-14 are for Blue. As for the STP, what it does depends on its value and the values of the previous bits.

| STP value | Value of other Bits | Result |
|-|-|-|
| 0 | All 0's | Fully Transparent |
| 0 | Any value | Non-Transparent color |
| 1 | All 0's | Black, Non-Transparent |
| 1 | Any value | Semi-Transparent color |

## Image Header

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | int32 | bnum | Said to be the data length of pixel data, but doesn't seem to do anything |
| 0x04 | int16 | DX | X Coordinate for VRAM placement |
| 0x06 | int16 | DY | Y Coordinate for VRAM placement |
| 0x08 | int16 | H | Horizontal resolution of image in VRAM |
| 0x08 | int16 | V | Vertical resolution of image in VRAM |

The PlayStation's VRAM stores all images as 16-bit color depth. For 8 and 4-bit images, their `H` value need to be devided to load into the VRAM correctly, and will be corrected when displayed. For 8-bit images, `H` should be half of it's original horizontal resolution. For 4-bit, `H` is the original horizontal resolution devided by 4.

## Image Data

How each pixel is recorded depends on the color depth of the image. For 4-bit color, 4 bits are used to specify what color from the CLUT will be used for that pixel. For 8-bit color, 8 bits are used to specify what color. For 16-bit color, every pixel uses the CLUT data format.

24-bit color is the most complex, using 3 int16 values. The first int16 value is used to store the red and green values, each taking up 8 bits. The second int16 value stores the blue value in the next set of 8 bits, but the following 8 bits is for the red color value of the next pixel. The last int16 value stores the green and blue values of the next pixel.

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
