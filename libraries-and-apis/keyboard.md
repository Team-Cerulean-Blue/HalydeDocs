---
description: Documentation of the keyboard API.
icon: keyboard
---

# Keyboard

The keyboard API is located in the public runtime as `keyboard`  and doesn't need to be `require`d.

* `keyboard.keys: table` \
  A table that contains all the keys based on their number, and vice-versa. Works like OpenOS.
* `keyboard.getCtrlDown(): boolean` \
  Returns `true`  if the Ctrl key is being held right now, otherwise `false`.
* `keyboard.getAltDown(): boolean` \
  Returns `true`  if the Alt key is being held right now, otherwise `false`.
* `keyboard.getShiftDown(): boolean` \
  Returns `true`  if the Shift key is being held right now, otherwise `false`.
