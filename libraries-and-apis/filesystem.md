---
description: Documentation of the filesystem library.
icon: files
---

# Filesystem

The `filesystem` library allows for interacting with `filesystem` components more easily and properly processing paths.

`filesystem.absolutePath(path: string): string, string`\
Returns the address of the filesystem component that `path` leads to and the absolute path in said filesystem component.

`filesystem.canonical(path: string): string`\
Returns the canonical path of `path` (one containing no special segments like . or ..). For example, the canonical path of `/home/../halyde/./apps` is `/halyde/apps`.

`filesystem.concat(path1: string, path2: string): string`\
Returns the result of concatenating the `path1` and `path2` together.

`filesystem.copy(fromPath: string, toPath: string): boolean or nil, string`\
Copies the file at `fromPath` to `toPath`. `toPath` must contain the file's name. Returns `nil` and an error message if an error occurred.

`filesystem.exists(path: string): boolean`\
Returns whether there is an object at `path` or not.

`filesystem.isDirectory(path: string): boolean`\
Returns whether the object at `path` is a directory or not.

`filesystem.list(path: string): table or nil, string`\
Returns a table of all objects at `path`, if it is a directory. Directories are suffixed with `/`. Returns `nil` and an error message if an error occurred.

`filesystem.makeDirectory(path: string): boolean or nil, string`\
Creates a directory at `path`. Returns `nil` and an error message if an error occurred.

`filesystem.open(path: string, [mode: string]): table or nil, string`\
Opens a file at `path` for reading/writing. `mode` defaults to `r`. Possible modes are `r`, `rb`, `w`, `wb`, `a` and `ab`. Returns a file stream - a table with 3 functions. Returns `nil` and an error message if an error occurred.

* `stream:read(amount: number): string or nil, string`\
  Tries to read the specified number of bytes from the file stream. Returns `nil` and an error message if an error occurred.
* `stream:write(data: string): boolean or nil, string`\
  Writes `data` to the file stream. Returns `nil` and an error message if an error occurred.
* `stream:close()`\
  Closes the file stream.

`filesystem.remove(path: string): boolean or nil, string`\
Removes the object at `path`. Returns `nil` and an error message if an error occurred.

`filesystem.rename(path: string): boolean or nil, string`\
Renames the object at the specified path. Returns `nil` and an error message if an error occurred.

`filesystem.size(path: string): number`\
Returns the size of the file at `path`. Returns 0 if the file does not exist or if it is a directory.
