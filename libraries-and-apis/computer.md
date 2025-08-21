---
description: Documentation of the computer library.
icon: computer
---

# Computer

This is just the low-level library, but mildly tweaked to work well with multitasking. It is functionally identical to the low-level one. The rest of this page is taken from the OpenComputers documentation.

* `computer.address(): string`\
  The [component address](https://ocdoc.cil.li/component:component_access) of this computer.
* `computer.tmpAddress(): string`\
  The component address of the computer's temporary file system (if any), used for mounting it on startup.
* `computer.freeMemory(): number`\
  The amount of memory currently unused, in bytes. If this gets close to zero your computer will probably soon crash with an out of memory error.
* `computer.totalMemory(): number`\
  The total amount of memory installed in this computer, in bytes.
* `computer.energy(): number`\
  The amount of energy currently available in the network the computer is in. For a robot this is the robot's own energy / fuel level.
* `computer.maxEnergy(): number`\
  The maximum amount of energy that can be stored in the network the computer is in. For a robot this is the size of the robot's internal buffer (what you see in the robot's GUI).
* `computer.uptime(): number`\
  The time in real world seconds this computer has been running, measured based on the world time that passed since it was started - meaning this will not increase while the game is paused, for example.
* `computer.shutdown([reboot: boolean])`\
  Shuts down the computer. Optionally reboots the computer, if `reboot` is true, i.e. shuts down, then starts it again automatically. This function never returns. This example will reboot the computer if it has been running for at least 300 seconds(5 minutes)
* `computer.getBootAddress():string`\
  Get the address of the filesystem component from which to try to boot first.
* `computer.setBootAddress([address:string])`\
  Set the address of the filesystem component from which to try to boot first. Call with nil / no arguments to clear.
* `computer.users(): string, ...`\
  A list of all users registered on this computer, as a tuple. To iterate the result as a list, use `table.pack` on it first. Please see [the user rights documentation](https://ocdoc.cil.li/computer_users).
* `computer.addUser(name: string): boolean or nil, string`\
  Registers a new user with this computer. Returns `true` if the user was successfully added. Returns `nil` and an error message otherwise.\
  The user must be currently in the game. The user will gain full access rights on the computer.
* `computer.removeUser(name: string): boolean`\
  Unregisters a user from this computer. Returns `true` if the user was removed, `false` if they weren't registered in the first place.\
  The user will lose all access to this computer. When the last user is removed from the user list, the computer becomes accessible to all players.
* `computer.pushSignal(name: string[, ...])`\
  Pushes a new signal into the queue. Signals are processed in a FIFO order. The signal has to at least have a name. Arguments to pass along with it are optional. Note that the types supported as signal parameters are limited to the basic types nil, boolean, number, string, and tables. Yes tables are supported (keep reading). Threads and functions are not supported.\
  Note that only tables of the supported types are supported. That is, tables must compose types supported, such as other strings and numbers, or even sub tables. But not of functions or threads.
* `computer.pullSignal([timeout: number]): name, ...`\
  Tries to pull a signal from the queue, waiting up to the specified amount of time before failing and returning `nil`. If no timeout is specified waits forever.\
  The first returned result is the signal name, following results correspond to what was pushed in `pushSignal`, for example. These vary based on the event type. Generally it is more convenient to use `event.pull` from the [event](https://ocdoc.cil.li/api:event) library. The return value is the very same, but the `event` library provides some more options.
* `computer.beep([frequency:string or number[, duration: number])`\
  if `frequency` is a number, its value must be between 20 and 2000.\
  Causes the computer to produce a beep sound at `frequency` Hz for `duration` seconds. This method is overloaded taking a single string parameter as a pattern of dots `.` and dashes `-` for short and long beeps respectively.
* `computer.getDeviceInfo(): table`\
  Returns a table of information about installed devices in the computer.
* `computer.getArchitecture(): string`\
  Returns the current architecture the computer is running on (for example, Lua 5.3.)
* `computer.getArchitectures(): string`\
  Returns all possible architectures the computer can run on.
* `computer.setArchitecture(architecture: string)`\
  Set the architecture of the machine.
* `computer.getProgramLocations(): table`\
  ???
* `computer.isRobot(): boolean`\
  Returns `true` if the machine is a robot, `false` otherwise.
