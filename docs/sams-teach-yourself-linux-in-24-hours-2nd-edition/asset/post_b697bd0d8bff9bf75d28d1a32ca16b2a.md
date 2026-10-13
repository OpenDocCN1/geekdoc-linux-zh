
## Customizing the X11 Root Window and Using Screen savers

If you have a color monitor, you might want to change the default color or pattern of the root, or desktop, window. You can do this quickly and easily with several X11 clients. I'll also show you how to put pictures into your background and how to set up and use screen savers in X11.

### Setting the Background Color

You can change the background color of your display with the xsetroot, or root window utility, which is found under the /usr/X11R6/bin directory. Your choice of color, as I mentioned previously, depends on the number of color depth of your X11 server. If you're using the SVGA server, you have a choice of 256 colors. For example, you can change the color with the following:

```
# xsetroot -solid red
```

### Setting the Background Pattern

If a solid color is too hard on your eyes or too plain for your tastes, you can also use one of nearly 90 different bitmap graphics files from the /usr/include/X11/bitmaps directory to set a desktop pattern. For example, to get a red basket-weave pattern for your desktop, use the following:

```
# xsetroot -bitmap /usr/include/X11/bitmaps/wide_weave -bg red
```

This command line tells the xsetroot client to load the bitmap graphic file wide_weave from the X11 bitmap graphics directory and display the pattern with a background color. If you have a monochrome display, you're out of luck with colors. But you can change the pattern and apparent shade of your background display with different bitmap files. Try the dimple1, dimple3, or flipped_gray bitmap files.

### Displaying Pictures on the Root Display

Many users like to display a favorite picture in the root window. If you have a favorite photograph you've scanned or a graphic you like, you can display your image on the desktop with the xsetroot client, but the image must be in the X11 bitmap format.

You can use a client that's already been discussed—xloadimage. See what graphics file formats the xloadimage client recognizes with the -supported command-line option, for example:

```
# xloadimage -supported
Type Name Can Dump Description
```

| Format | Supported | Description |
|---|---|---|
| niff | Yes | Native Image File Format (NIFF) |
| sunraster | No | Sun Rasterfile |
| gif | No | GIF Image |
| jpeg | Yes | JFIF-style JPEG Image |
| fbm | No | FBM Image |
| cmuraster | No | CMU WM Raster |
| pbm | Yes | Portable Bit Map (PBM, PGM, PPM) |
| faces | No | Faces Project |
| rle | No | Utah RLE Image |
| xwd | No | X Window Dump |
| vff | No | Sun Visualization File Format |
| mcidas | No | McIDAS areafile |
| vicar | No | VICAR image |
| pcx | No | PC Paintbrush Image |
| gem | No | GEM Bit Image |
| macpaint | No | MacPaint Image |
| xpm | No | X Pixmap |
| xbm | No | X Bitmap |

The file formats xloadimage can use are listed in the left column. If you have a graphic you want to display, you can use the following:

```
# xloadimage -onroot cathy.gif
```

This loads the graphic file, cathy.gif, and displays it (depending on its size) in a tiled, or multiple-view, format. If you only want one large version of your graphic in the root display, use the -fullscreen command-line option, for example:

```
# xloadimage -onroot -fullscreen cathy.gif
```

This causes the xsetroot command to load the graphic and zoom to fit the display. You have to experiment with different sized graphics to get the best effect for your graphics.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_190_0.png)

> The xv client can also be used to put images in your root display. If you use KDE, save your favorite image in JPEG format in the /opt/kde/share/wallpapers directory. You can then select the image as a default wallpaper for one of your desktops with the KDE Control Center's Desktop Background dialog box.

### Screen Saver Settings and Programs

Although displaying a colored pattern or picture on your desktop can be fun, X11 screen savers also offer password control. Even though screen savers aren't needed to protect modern computer monitors from the "burn-in" effect of a continuous display, they are fun, and you can find an interesting variety installed along with X11.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_191_0.png)

> KDE users can use the KDE Control Center's Desktop Screen savers dialog box to control screen saving.

Use the xset client, introduced earlier, to manage screen saving under X11. If you want to see the current settings, use the q command-line option (note that there is no hyphen used), for example:

```
# xset q
```

```
Screen Saver:
prefer blanking: yes  allow exposures: yes
timeout: 0    cycle: 600
```

You can turn on screen saving with the xset client by using the s command-line option, followed by the word on. To set the time in seconds, use the s option, followed by the number of seconds you want your X11 server to wait to blank the screen, for example:

```
# xset s 10
```

This sets the time out interval to 10 seconds before the X11 screen saver is activated (just to test screen saving). To enable the screen saver, which is built in to your X11 server, use the s option with the word on, for example:

```
# xset s on
```

After 10 seconds, X displays a blank screen. If you want to see graphics and a background pattern, you can use the noblank option for the xset s command-line option, for example:

```
# xset s noblank
```

As you can see, a large X is displayed on the screen. To turn off screen saving, use the s off command-line option (don't forget to change the screen saving interval to something more reasonable, such as 600 for 10 minutes, if you use xset). If this isn't your idea of a screen saver, you can try the xscreensaver clients.

The xscreensaver and xscreensaver-command clients, by Jamie Zawinski, are found under the /usr/X11R6/bin directory. The xscreensaver client has 16 command-line options. Although this hour doesn't cover all the options, the basic way to use this screen saver is to first run the xscreensaver client in the background, as follows:

```
# xscreensaver -timeout 5 &
```

This command sets the screen saver to run after five minutes of no keyboard or mouse activity. You can control this client with the xscreensaver command client to turn the xscreensaver on or off or to activate it immediately. Although the xscreensaver client has a -lock option to password-protect your display, you have to recompile the program to enable this feature.

The xscreensaver client comes with nearly two dozen different screen savers, which can also be run as standalone programs. For example, you can run the fractal drawing program, hopalong, in a window, as follows:

```
# hopalong
```

After you press Enter, a fractal image appears in a window (as shown in Figure 7.9), so you can see what it looks like.

### FIGURE 7.9

The hopalong client is part of a screen saver for X11.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_192_0.png)

For a list of the screen savers that work with the xscreensaver client, read the file XScreenSaver in the /usr/X11R6/lib/X11/app-defaults directory. You can find other settings in the file, which is the X11 resources file for this client.

You might also be interested in the xlock client. Although it is not a screen saver, xlock is a sophisticated terminal-locking program with nearly 50 command-line options and more than 50 different displays built in. The xlock client is helpful if you want to password-protect your display to prevent others from using your computer while you're away.

By default, after you start the xlock program, you must enter your password before you can use your display again. You can use it as a simple screen saver without password protection to display a variety of animations, for example:

```
# xlock -duration 10 -nolock -mode random
```

This command line tells the xlock program to display a random selection of its animations, each of which runs for 10 seconds.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_193_0.png)

> The xlock client can also make your desktop an animated display if you use the -inroot command-line option. This doesn't protect your system, but you might find the visuals stimulating!

## Exploring X11 Programs

There’s not enough room in this hour to discuss all the X11 clients on your CD-ROM. You can find discussions about different clients throughout the rest of this book, but this section shows you some helpful programs that give you more information about your system and some tips and tricks on how to use them.

### Listing X11 Fonts with xlsfonts

If you want a list of all the fonts recognized by X11 on your system, you can use the xlsfonts client. Use a pager like less or more (discussed in Hour 4, “Reading and Navigation Commands”) if you call the client without any options. You can also use wildcards or patterns to match font names. This can be handy to find a particular font on your system, for example:

```
# xlsfonts -fn "*italic*"
lucidasans-bolditalic-10
lucidasans-bolditalic-10
lucidasans-bolditalic-12
lucidasans-bolditalic-12
lucidasans-bolditalic-14
lucidasans-bolditalic-14
lucidasans-bolditalic-18
lucidasans-bolditalic-18
lucidasans-bolditalic-24
lucidasans-bolditalic-24
lucidasans-bolditalic-8
lucidasans-bolditalic-8
lucidasans-italic-10
lucidasans-italic-12
```
