to the appropriate option: -bg for background color, -bd for window border color, and -fg for foreground color.

⇒ To start an xclock with a light blue window background, type:

```
$ xclock -bg lightblue RET
```

You can specify any combination of these attributes.

⇒ To start an xclock with a sea green window background and a turquoise window foreground, type:

```
$ xclock -bg seagreen -fg turquoise RET
```

NOTES: The -bordercolor, -background, and -foreground options are synonymous with -bd, -bg, and -fg.

# 4.2.3 Specifying X Window Font

To specify a font for use in a window, use the -fn option followed by the X font name to use. (To get an X font name, use xfontsel; see Recipe 16.1 [Using X Fonts], page 395).

⇒ To start an xclock with a digital display, and specify that it use a 17-point Helvetica font for text, type:

```
$ xclock -digital -fn -*-helvetica-*-r-*-*-17-*-*-*-*-*-*-* RET
```

This command starts an xclock that looks like Figure 4-4.

![](bbox=[0.32, 0.94, 0.68, 0.00102])

Figure 4-4. A digital xclock with Helvetica type.

NOTES: If you specify the font for a shell window, you can resize it after it's running, as described in Recipe 16.14 [Resizing the Xterm Font], page 398.

The -font option is synonymous with -fn.

# 4.2.4 Specifying X Window Border Width

To specify the width of the border of an X client, use -bw followed by the desired width, in pixels.

⇒ To start an xclock with a border width of 30 pixels, type:

```
$ xclock -bw 30 RET
```

NOTES: The -borderwidth option is synonymous with -bw.