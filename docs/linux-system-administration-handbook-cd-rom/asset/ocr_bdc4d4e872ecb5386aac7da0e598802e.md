# 232 Chapter 16 • X Windowing System

override the DISPLAY variable if it's set. If the DISPLAY variable is set and the -display option is not used, the window will automatically be displayed on the host and display set in DISPLAY.

```
-bg <color>
```

Sets the color of the background of the window. Color can either be a name of color "gray" or "blue" or as collections of RGB (red, green, blue) values in hex. The syntax for this is rgb:h/h/h where h is a number relating to the amount of red (in the first slot), green (in the second slot), and blue (in the third slot) to make a particular color. The hex number can be one to four characters long, depending on the number of colors your X server supports. For example, rgb:0/0/0 is black, rgb:ffff/0/0 is red. A list of colors that have names is available in the /usr11/lib/x11/rgb.txt file. Each entry has the RGB values in decimal (0 to 255) and a name, which can be used instead of the rgb:h/h/h entry.

```
-fg <color>
```

sets the color of the foreground.

```
-fn <font>
```

specifies the default font to use in the window. You can get lists of the available fonts using the xfontsel or xlsfonts programs.

```
-geometry <WIDTH>x<HEIGHT>+<XOFF>+<YOFF>
```

Sets the size and position of the window. For an xterm, this is in terms of characters, so a geometry of

```
> -geometry 80x25
```

would create a window that is 80 characters wide and 25 lines long. The XOFF and YOFF set where the upper-left-hand corner of the window should be placed. In the case of positive XOFF or YOFF, the offset is from the right or top sides, respectively. Here's some example screen placements:

+   +0+0 Upper-left-hand corner
-0+0 Upper-right-hand corner
-0-0 Lower-right-hand corner
+0-0 Lower-left-hand corner