prompted a number of commercially successful products, e.g., the Apple Macintosh, Microsoft Windows, and the X Window System used in Linux and Unix workstations from DEC, HP, IBM, Sun, Silicon Graphics and others.

# A note about earlier display devices

In 1947, Dr. F.C. Williams developed a method of storing data using dots on a cathode ray tube [22]. Although data storage was the primary purpose of this device, it also proved a useful (and for a while the only) way of reading results on the Manchester University research computer. But with only 1024 bits of display, the idea never caught on and core memory quickly rendered this storage mechanism obsolete.

For some time thereafter, CRTs were relegated to one of two categories: vector display or character display.

A vector display draws each character as a series of strokes. Circuits direct the electron beam to the right place on the screen and other circuits turn the beam on or off as needed. Using this method, characters can be placed at arbitrary locations on the screen and can be rotated and sized with little additional effort.

The character display uses raster scanning of the entire screen with a series of horizontal lines. The beam is turned on and off according to entries in a look-up table, building images of characters out of fragments of a number of adjacent lines.

Both of these methods have a major shortcoming: they are unable to display arbitrary data. The bit-mapped display was the answer. Like the character display, it operates on a rasterized scan of the screen. The difference is that each pixel (picture element—a dot on the screen) is individually addressable—often with multiple bits of precision to offer grey scale or color control.

It's interesting to note that bit-mapped displays are practical only because memory prices have dropped low enough. In contrast to the system designed by Dr. Williams, memory now drives the display instead of the display being the memory.

It's also interesting to note that Linux easily supports all three kinds of CRT displays, as well as the hard-copy terminals which were so essential to the first Unix systems.