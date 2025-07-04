---
description: Documentation of Halyde's driver system.
icon: gear-code
---

# Drivers

Like any good operating system, Halyde has a driver system. Drivers are small scripts that run on system startup (or in other cases, but that functionality is coming soon) and can depend on other drivers. They are usually to add virtual components to allow the system to interface with some miscellaneous code better.\
For example, there could be a driver that works with the filesystem on an unmanaged drive and creates a `filesystem` virtual component for each of such drives upon startup.\
Drivers can also have types based on the type of virtual component they create, for example the aforementioned driver would have the type `filesystem`.

To add a driver, simply create a lua file in `/halyde/drivers`. It should return a table with:

* `onStartup: function`: This is where the main code goes that runs on system startup.
* `type: string`: The type of the driver, that being the type of virtual component it creates. (Optional)
* `dependencies: table`: The drivers this depends on. This can contain driver names (filenames without the .lua) and driver types. (Optional)

Here is an example snippet of how a driver file could look:

```lua
local driver = {}
driver.type = "filesystem"
driver.dependencies = {"tapeDriver", "drive"}
driver.onStartup = function()
  -- This is where the main code goes
end

return driver
```
