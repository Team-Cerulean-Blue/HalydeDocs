---
description: Documentation of the dataTools library.
icon: database
---

# DataTools

The `dataTools` library adds extra utilities for working with different data types like strings and tables. It is always loaded as a global and adds to the native `string` and `table` globals.

* `table.find(haystack: table, needle: any): any or nil`\
  Finds `needle` in `haystack` and returns its key or `nil` .
* `table.copy(original: table): table`\
  Recursively copies a table and returns the identical copy.
* `convert(amount: number, fromUnit: string, toUnit: string): number or nil, string`\
  Converts from a unit to another unit. Returns nil and an error message if it fails. Supported units are:
  * B - GB
  * B - GiB
