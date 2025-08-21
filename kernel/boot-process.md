---
description: Documentation of Halyde's boot process.
icon: file-binary
---

# Boot process

The first thing that gets loaded by the BIOS is the \`/init.lua\` file. It begins starting the OS. It is made to be minimal to easily be modified into an advanced bootloader in the future and to possibly fit into a boot sector.

\`/init.lua\` loads \`/halyde/kernel/boot.lua\`. This file initializes the system, loads its version

/`init.lua` is usually used as the file that gets loaded by the BIOS and begins starting the OS. In Halyde, it loads `/halyde/kernel/boot.lua` and catches/displays low-level errors.

The init file may be modified to serve as an advanced bootloader.
