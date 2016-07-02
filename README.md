# BinPack
Pack rectangles inside a bin efficiently in JavaScript.

Uses the MAXRECTS-BSSF-BNF algorithm outlined in Jukka Jylanki's paper
[A Thousand Ways to Pack the Bin - A Practical Approach to Two-Dimensional 
Rectangle Bin Packing](http://clb.demon.fi/files/RectangleBinPack.pdf). Jukka's 
C++ implementation can be found in 
[this repo](https://github.com/juj/RectangleBinPack).

# API Reference
(The API is very unstable at the moment.)

*#* **BinPack**()

Create a new bin `packer`.

*#* **packer**

Bin packing definition object. Has various methods that set the packers
specification. Each method returns the `packer` object so parameters can
be set using method chaining.

*#* packer.**binWidth**([*width*])<br>
*#* packer.**binHeight**([*height*])

Set the width and height of the bin. If not specified, return the current
width and height of the bin. Both default to `800`;

*#* packer.**add**(*datum*)

Packs a rectangle in the bin using the width and height information stored
in the *datum* object, e.g., `{ width: 50, height: 25 }`. By default
it looks for a `width` and `height` property on `datum` but this
can be changed using the `rectWidth()` and `rectHeight()` 
methods.

*#* packer.**addAll**(*data*)

Packs multiple rectangles given an array of objects each defining a 
rectangle.

*#* packer.**rectWidth**([*width*])<br>
*#* packer.**rectHeight**([*height*])

Set the rectangle width and height accessor functions. When rectangles are
packed using the `add()` and `addAll()` methods these accessors are used
to determine the width and height associated with each `datum`.

*#* packer.**sort**([*comparator*])

Sort the `data` array passed to the `addAll()` method before packing. If
`false`, no sorting is done. No sorting is the default behavior.

*#* packer.**positioned**

Array of rectangles that have successfully been packed in the bin. This is
empty until `add()` or `addAll()` have been called. Each rectangle has five
properties:
- `x`: x-position of rectangle's left side
- `y`: y-position of rectangle's bottom side (or top side if zero starts at the top, like in browsers)
- `width`: width of the rectangle
- `height`: height of the rectangle
- `datum`: the data object associated with the rectangle that was passed to `add()` or `addAll()`

*#* packer.**unpositioned**

Array of rectangles that couldn't be packed into the bin because there
wasn't enough free space.