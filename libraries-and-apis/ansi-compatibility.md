---
description: List of ANSI commands that are currently available in Halyde.
icon: typewriter
---

# ANSI Compatibility

All the commands listed here are only what is capable with the OpenComputers GPU. Most commands outside color are unlisted due to these constraints.

A command must always be on the same string for it to work properly. If a command is cut off, or separated into two strings, this can lead to undefined behavior.

### [Select Graphic Rendition](https://en.wikipedia.org/wiki/ANSI_escape_code#Select_Graphic_Rendition_parameters)

Command: `\x1b[*m` where \* are the arguments.

#### [Colors](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors)

* [x] [3-bit and 4-bit color](https://en.wikipedia.org/wiki/ANSI_escape_code#3-bit_and_4-bit) (Arg ID 30-37, 40-47, 90-97, 100-107)
* [ ] [8-bit color](https://en.wikipedia.org/wiki/ANSI_escape_code#8-bit) (Args `38;5;n`)
* [ ] [24-bit color](https://en.wikipedia.org/wiki/ANSI_escape_code#24-bit) (Args `38;2;r;g;b`)
* [ ] [Reverse video](https://en.wikipedia.org/wiki/Reverse_video) or invert (Arg ID 7)

#### Resetting

* [x] Reset all attributes (Arg ID 0)
* [x] Reset 3-bit color (Arg ID 39, 49)

***

### Cursor movement

* [ ] Cursor Up (`\x1b[*A`)
* [ ] Cursor Down (`\x1b[*B`)
* [ ] Cursor Forward (`\x1b[*C`)
* [ ] Cursor Back (`\x1b[*D`)
* [ ] Cursor Next Line (`\x1b[*E`)
* [ ] Cursor Previous Line (`\x1b[*F`)
* [ ] Cursor Horizontal Absolute (`\x1b[*G`)
* [ ] Cursor Position (`\x1b[*H`)
* [ ] Horizontal Vertical Position (`\x1b[*f`)

It is recommended to change the `termlib.cursorPosX` and `termlib.cursorPosY` values instead of using ANSI escape codes (see [Terminal](terminal.md)).

***

### Other [CSI commands](https://en.wikipedia.org/wiki/ANSI_escape_code#Control_Sequence_Introducer_commands)

* [ ] Erase in Display (`\x1b[*J`)
* [ ] Erase in Line (`\x1b[*K`)
* [ ] Scroll Up (`\x1b[*S`)
* [ ] Scroll Down (`\x1b[*T`)

***

### [C0 ](https://en.wikipedia.org/wiki/ANSI_escape_code#C0_control_codes)[Control Codes](https://en.wikipedia.org/wiki/ANSI_escape_code#C0_control_codes)

* [x] Bell (`\x07` or `\a` )
* [ ] Backspace (`\x08`)
* [ ] Tab (`\x09`)
* [x] Line Feed (`\x0A` or `\n`)
* [ ] Carriage Return (`\x0D` or `\r`)
