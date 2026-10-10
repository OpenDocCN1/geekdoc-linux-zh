# Scalable Fonts

Scalable fonts are a fairly recent addition to X. They are named by using 0 for the pixel size, point size, x and y resolution, and average width. Note that only Type 1 and Speedo fonts are scalable; scaling bitmap fonts produces poor results.

# Background Material

The technical term for using “magical” values in the XLFD is kludge. It overloads the meaning of fields in the XLFD in a questionable and nonintuitive manner.

When you use xlsfonts, you might see some proportional fonts such as:

```
-bitstream-courier-medium-r-normal--0-0-0-m-0-iso8859-1
```

You can view the font in a specific size by specifying a particular size. This gives an xterm with 48-pixel-high letters:

```
$ xterm -fn \\
-bitstream-courier-medium-r-*-*-48.*.*.*.*.*.*
```

# Starting X

If you successfully installed KDE as part of your installation, X Windows probably starts automatically when you boot the computer. The program which that manages the login session is called kdm. It is covered in the Chapter 5.

If X does not start automatically (because you couldn’t configure it or you prefer booting into text mode), you can start X from the shell prompt with the startx command. The simplest way to invoke startx is:

```
$ startx
```

This starts an X server and executes the shell script $HOME/.xinitrc. Usually, you place commands to start various X clients and a window manager in $HOME/.xinitrc. If this file does not exist, the file /etc/X11/xinit/xinitrc is run instead. This starts a clock and a few xterm terminal windows, which is probably not what you want.