---
description: Documentation of the terminal library.
icon: rectangle-terminal
---

# Terminal

Interacting with the terminal doesn't require you to import anything. The entirety of the terminal library (`terminal`) is provided as a global in the runtime environment.

* `print(...)`\
  Prints every argument into the screen. Any arguments that aren't a string will turn into their `tostring()` counterpart. This is good for basic strings, numbers, booleans, and nil, but not function and tables. Strings with ANSI are supported (see [ANSI Compatibility](../ansi-compatibility.md)).
* `terminal: table`\
  This is a global table that contains readable and writable values for directly interacting with the library.

> - `terminal.cursorPosX: number`\
>   X position of the cursor, in range \[1, width]
> - `terminal.cursorPosY: number`\
>   Y position of the cursor, in range \[1, height]
> - `terminal.readHistory: table`\
>   Contains all the read history for every history type, like so:
>
> ```
> {
>   ["historyTypeA"]={"commandA","commandB"},
>   ["historyTypeB"]={"commandA","commandB"}
> }
> ```
>
> * `terminal.read([readHistoryType: string], [prefix: string], [defaultText: string], [maxChars: number]): string`\
>   Read keyboard input as text, until the user presses Enter.\
>   `readHistoryType`: Type of history for the command. If you wish to have command history (where the up and down keys can scroll through it), use an unique ID. Otherwise, this can be left as nil.\
>   `prefix` : Text to print before the user input. For example, the shell puts `/home/ >` as its prefix, and updates accordingly when the path changes.\
>   `defaultText` : Default text to insert before any user input.\
>   `maxChars` : The maximum amount of characters that can be inserted by the user. Please note that this uses an Unicode character count, and not the width of when it gets rendered.
> * `terminal.write([text: any], [textWrap: boolean])`\
>   Writes a string into the screen. Behaves like `print()` but without multiple arguments.\
>   `textWrap` : Whether to wrap the text or not. If this is false, the text cuts off when it reaches the end of the screen. Defaults to `true`.
> * `clear()`\
>   Clears the entire screen, and resets the cursor position.
