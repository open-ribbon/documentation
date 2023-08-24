# ANC - Camera Animation

The ANC format store keyframes for a single camera animation. These files are used to control the camera during gameplay, menus and cutscenes. Longer animation sequences may be split into multiple .ANC files.

## File Layout

* .ANC
    * 1 `Header`
    * 0-n `CameraKeyrame`

### Header

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | int16 | unk | Always 0x8000 |
| 0x02 | int16 | unk | Unused? Possible values: 1, 15, 20, 30, or 60 |
| 0x04 | uint16 | keyframeCount | |

### CameraKeyframe

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | int16 | vpx | Viewport X |
| 0x02 | int16 | vpy | Viewport Y |
| 0x04 | int16 | vpz | Viewport Z |
| 0x06 | int16 | vrx | Reference point X |
| 0x08 | int16 | vry | Reference point Y |
| 0x0A | int16 | vrz | Reference point Z |
| 0x0C | int16 | rz | Viewport twist. 0x1000 = 1º |
| 0x0E | int16 | fov | Field of view |

Each frame, the game orients the viewport camera by calling `GsSetRefView2()` with a static `GsRVIEW2` object using parameters supplied by the current keyframe. This function call places the camera at coordinates `(vpx, vpy, vpz)` facing towards `(vrx, vry, vrz)`.
