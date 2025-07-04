---
description: Documentation of the raster library.
icon: alien-8bit
---

# Raster

The `raster` library is a library for creating pixel-based graphics in Halyde. Since OpenComputers graphics are text mode only, `raster` uses braille characters to represent pixels. The limitation of this is that there can only be 2 colors per character (or 2x4 pixel chunk): the foreground color and the background color.

`raster.init(width: number, height: number, bgcolor: number)`\
Initializes the `raster` library and a render buffer for it.\
`width`: The width of the render buffer.\
`height`: The height of the render buffer.\
`bgcolor`: The background color of the render buffer.

`raster.clear()`\
Clears the `raster` render buffer.

`raster.units.charToBraille(x: number, y: number): number, number`\
Converts `x` and `y` in text characters to `x` and `y` in pixels and returns them.

`raster.units.brailleToChar(x: number, y: number): number, number`\
Converts `x` and `y` in pixels to `x` and `y` in text characters and returns them.

`raster.set(x: number, y: number, color: number): boolean`\
Sets a pixel at `x` and `y` to be of `color`. `color` must be in hex. Returns false if `x` and `y` are out of bounds.

`raster.get(x: number, y: number): number`\
Returns the color at `x` and `y` in pixel coordinates.

`raster.drawLine(x1: number, y1: number, x2: number, y2: number, color: number)`\
Draws a straight line of color between `x1``, y1` and `x2``, y2` with a color of `color`.

`raster.drawRect(x1: number, y1: number, x2: number, y2: number, color: number)`\
Draws an unfilled rectangle between `x1, y1` and `x2, y2` with a color of `color`.

`raster.fillRect(x1: number, y1: number, x2: number, y2: number, color: number)`\
Draws a filled rectangle between `x1, y1` and `x2, y2` with a color of `color`.

`raster.drawCircle(x: number, y: number, radius: number, color: number)`\
Draws an unfilled circle with the center being at `x, y` with a radius of `radius` and a color of `color`.

`raster.fillCircle(x: number, y: number, radius: number, color: number)`\
Draws a filled circle with the center being at `x, y` with a radius of `radius` and a color of `color`.

`raster.drawEllipse(x1: number, y1: number, x2: number, y2: number, color: number)`\
Draws an unfilled ellipse with one corner being at `x1, y1` and the other being at `x2, y2` and a color of `color`.

`raster.fillEllipse(x1: number, y1: number, x2: number, y2: number, color: number)`\
Draws a filled ellipse with one corner being at `x1, y1` and the other being at `x2, y2` and a color of `color`.

`raster.update()`\
Renders everything from the `raster` render buffer.

`raster.free()`\
Uninitializes the `raster` library and frees the render buffer.
