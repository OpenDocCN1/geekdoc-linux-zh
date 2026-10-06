# Offset from Buffer Origin

| 0 | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|--|
| 41H | 07H | 42H | 07H | 43H | 01H |
| Char. | Attr. | Char. | Attr. | Char. | Attr. |

Note the 01H attribute, for underlined characters

![](bbox=[0.228, 0.2485, 0.9035, 0.5235])

In a color display, this address would be 0B800:0 instead.

There is neither electrical nor logical (addressing) division of the buffer into lines; line structure exists only in the display.

Figure 6.11 The PC's video refresh buffer.

The byte at 0B000:0005 is also an attribute byte, but its value is 01H. On a monochrome screen, 01H makes the corresponding character underlined. On a color display, 01H makes the character blue on a black background.

There is nothing about the video refresh buffer to divide it into the lines you see on the display. The first 160 characters (80 ASCII codes plus their 80 attribute bytes) are shown as the first line, and the subsequent 160 characters are shown on the next line down the screen.

You might rightfully ask ASCII code is in the video refresh buffer for locations on the screen that show no character at all. The answer, of course, is that there is character there in every empty space: the space character, whose ASCII code is 20H.