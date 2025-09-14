---
description: Documentation of the component library.
icon: microchip
---

# Component

* The `component` library allows for interacting with OpenComputers components of all sorts. This is a native library, but the version in Halyde is improved with several new features.
* This library also allows for virtual components to be added or for components to be virtually removed (so they won't show up in `component.list()`). This is useful for drivers and adaptation layers to create new virtual components that could smoothly interface with higher-level libraries like [`filesystem`](filesystem.md).
* `component.list([filter: string]): table`\
  Returns a table with all the components or virtual components available, or any of type `filter` if specified. Has a \_\_call metatable iterator, so you can do things like...

{% code fullWidth="false" %}
```lua
for address, componentType in component.list() do
  ...
end
```
{% endcode %}

* `component.invoke(address: string, method: string, [...]): ...`\
  Invokes a function on a component.\
  `address`: Address of the component.\
  `method`: Function name to invoke.\
  `...`: Arguments to the function (or nil).
* `component.proxy(address: string): table`\
  Returns the proxy to a certain component. The proxy is a table of all the component's functions and properties.
* `component.get(shortenedAddress: string): string or nil, string`\
  Finds the full component address of `shortenedAddress`. Returns `nil` and an error message otherwise. `shortenedAddress` must be at least 3 characters long.
* `component.virtual.add(address: string, type: string, proxy: table)`\
  Adds a virtual component with `address` and `type`. When this component is proxied, returns `proxy`. When this component is invoked, the function is called from `proxy`.
* `component.virtual.remove(address: string)`\
  Virtually removes a component. If this was a real component, it won't show up in `component.list()`, but it will still be able to be proxied and invoked. If this was a virtual component, it will be removed completely.
* `component.virtual.check(address: string): boolean, table or nil` \
  Returns `true`, with information of the process that created the component (in the same format as `tched.getCurrentTask`), if the component from the specified address is virtual. Otherwise `false`.
* `component.doc(address:string, method:string): string`\
  Returns the documentation string for the method with the specified name of the component with the specified address, if any. Note that you can also get this string by using `tostring` on a method in a proxy, for example.
* `component.methods(address:string):table`\
  Returns a table with the names of all methods provided by the component with the specified address. The names are the keys in the table, the values indicate whether the method is called directly or not.
* `component.type(address:string):string`\
  Get the component type of the component with the specified address.
* `component.fields(address:string):string`\
  I'm going to be honest, I have no clue what this does. It's undocumented in the official OpenComputers wiki. Just know that it exists, I guess.
* `component.slot(address:string):string`\
  Return slot number which the component is installed into. Returns -1 if it doesn't otherwise make sense.
