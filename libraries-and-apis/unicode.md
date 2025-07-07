---
description: Documentation of the Unicode library.
icon: text-size
---

# Unicode

The Unicode library contains methods that exist in vanilla OpenComputers, but adds some other methods that are exclusive to Halyde.

* `unicode.readCodePoint(readByte: function): number or nil` \
  Reads the code point of the first Unicode character from an iterator function that returns a byte when called.
* `unicode.readChar(readByte: function): string` \
  Reads the first Unicode character from an iterator function that returns a byte when called.
* `unicode.codepoint(chr: string): number` \
  Acts as the reverse function for `unicode.char` . It returns the codepoint of the character in the string.
* `unicode.iterate(readByte: function): function` \
  Takes an [iterator function](https://www.lua.org/pil/7.1.html) that returns a byte when called, and returns an iterator function that returns a string when called. The string the output iterator function returns is an Unicode character that is getting read.

For the other, vanilla methods, these have been left untouched:

* `unicode.char(value: number, ...): string`\
  UTF-8 aware version of `string.char`. The values may be in the full UTF-8 range, not just ASCII.
* `unicode.charWidth(value: string, ...): number`\
  Returns the width of the first character given. For example, for `シ` it'll return `2`, where `a` would return `1`.
* `unicode.isWide(value: string, ...): boolean`\
  Returns if the width of the first character given is greater than 1. For example, for `シ` it'll return `true`, where `a` would return `false`.
* `unicode.len(value: string): number`\
  UTF-8 aware version of `string.len`. For example, for `Ümläüt` it'll return `6`, where `string.len` would return `9`.
* `unicode.lower(value: string): string`\
  UTF-8 aware version of `string.lower`.
* `unicode.reverse(value: string): string`\
  UTF-8 aware version of `string.reverse`. For example, for `Ümläüt` it'll return `tüälmÜ`, where `string.reverse` would return `tälm`.
* `unicode.sub(value: string, i:number[, j:number]): string`\
  UTF-8 aware version of `string.sub`.
* `unicode.upper(value: string): string`\
  UTF-8 aware version of `string.upper`.
* `unicode.wlen(value: string): number`\
  Returns the width of the entire string.
* `unicode.wtrunc(value: string, count: number): string`\
  Truncates the given string up to but not including `count` width. If there are not enough characters to match the wanted width, the function errors.
