---
description: Documentation of the Halyde kernel's module system.
icon: rectangles-mixed
---

# Modules

Halyde's kernel is modular, meaning that it works by relying on modules that can communicate with the kernel and load at any time whenever possible.

Modules are Lua files located in `/halyde/kernel/modules`  and return a table containing:

* `[dependencies: table]`: List of required modules, or required module types. If specified, will start loading these dependencies before using this module.
* `[type: string]`: The type of the module.
* `check: function`: A function that returns whether the module is capable of loading in these circumstances.
* `init: function`: The main code of the module.
* `exit: function`: Must stop any tasks created by the module, and delete any entries related to it in the public space.

The `dependencies` and `type` entries aren't important, but keep their values if you are transitioning from a driver (feature removed since v3.0.0).

The user space is exclusively located in `_PUBLIC`, because all modules run in the kernel space. Anything running in user space (shell, libraries, apps...) will have `_PUBLIC` set at its environment.

All modules don't run as tasks, but are directly executed from the kernel. If the code needs to run in the background while the system is running, use the [Task Scheduler](task-scheduler.md) (`_PUBLIC.tsched`).

Here is an example of how a module could look:

```lua
local module = {}

function module.check()
    return true
end
function module.init()
    _G._PUBLIC.helloworld="Hello, World!"
    -- running "helloworld" in the lua shell will now return "Hello, World!"
end
function module.exit()
    _G._PUBLIC.helloworld=nil
end

return module
```
