+   • To start a large xclock, 480 pixels wide and 500 pixels high, type:

```
$ xclock -geometry 480x500 RET
```

+   • To start an xclock with a width of 48 pixels and the default height, type:

```
$ xclock -geometry 48 RET
```

+   • To start an xclock with a height of 48 pixels and the default width, type:

```
$ xclock -geometry x48 RET
```

You can give positive or negative numbers for the XOFF and YOFF fields. Positive XOFF values specify a position from the left of the screen; negative values specify a position from the right. If YOFF is positive, it specifies a position from the top of the screen; if negative, it specifies a position from the bottom of the screen. When giving these offsets, you must specify values for both XOFF and YOFF.

To place the window in one of the four corners of the desktop, use zeroes for the appropriate XOFF and YOFF values, as follows:

| XOFF AND YOFF VALUES | WINDOW POSITION |
| +0+0 | Upper left corner. |
| +0-0 | Lower left corner. |
| -0+0 | Upper right corner. |
| -0-0 | Lower right corner. |

+   • To start a default size xclock in the lower left-hand corner, type:

```
$ xclock -geometry +0-0 RET
```

Or, to put it all together, you can specify the size and location of a window with one geometry line that includes all four values.

+   • To start an xclock with a width of 120 pixels, a height of 100 pixels, an x offset of 250 pixels from the right side of the screen, and a y offset of 25 pixels from the top of the screen, type:

```
$ xclock -geometry 120x100-250+25 RET
```