# ANM - Model Animation

The ANM format stores keyframes for a TMD model animation. Longer animation sequences may be split into multiple .ANM files.

## File Layout

* .ANM
    * 1 `Header`
      * 0-n `Frame`
        * 0-n `Keyframe` (per object)

### Header

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | int16 | unk | Always 0x8000 |
| 0x02 | int16 | unk | Unused? Possible values: 1, 15, 20, 30, or 60 |
| 0x04 | uint16 | frameCount |
| 0x06 | uint16[] | frameOffsetTable |

The `frameOffsetTable` array contains `(frameCount + 1)` elements. Multiply each value by 2 to get the file offset for each set of keyframes. The last entry marks the end offset of the file.

### Frame

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | Keyframe[] | | | |

Contains keyframes for all keyed objects in the TMD for a particular frame of the animation.

If an object index does not have a keyframe, it is not drawn for the current frame.

There is no explicit count for the number of elements in the `Keyframe` array. To determine this count for frame `n`, keep processing the next `Keyframe` until reaching the end offset given by `frameOffsetTable[n + 1] * 2`.

### Keyframe

| Offset | Type | Name | Notes |
|-|-|-|-|
| 0x00 | uint8 | objectIndex | |
| 0x01 | uint8 | flags | |
| 0x02 | int16 | rotationX | Present if `(flags & 0b001) > 0`. Radians = value * 2π / 4096 |
| 0x04 | int16 | rotationY | Present if `(flags & 0b001) > 0`. Radians = value * 2π / 4096 |
| 0x06 | int16 | rotationZ | Present if `(flags & 0b001) > 0`. Radians = value * 2π / 4096 |
| 0x02 / 0x08 | int16 | scaleX | Present if `(flags & 0b010) > 0`. Scale = value / 4096 |
| 0x04 / 0x0A | int16 | scaleY | Present if `(flags & 0b010) > 0`. Scale = value / 4096 |
| 0x06 / 0x0C | int16 | scaleZ | Present if `(flags & 0b010) > 0`. Scale = value / 4096 |
| 0x02 / 0x08 / 0x0E | int16 | positionX | Present if `(flags & 0b100) > 0`. |
| 0x04 / 0x0A / 0x10 | int16 | positionY | Present if `(flags & 0b100) > 0`. |
| 0x06 / 0x0C / 0x12 | int16 | positionZ | Present if `(flags & 0b100) > 0`. |

Each keyframe animates an individual object in the TMD given by `objectIndex`. Rotation, scale and position are optional depending on the bits set in `flags`, and will always appear in that order.
