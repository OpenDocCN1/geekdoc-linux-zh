FTP site.) The xv command can display a variety of image types: GIF, JPEG, TIFF, PBM, PGM, PPM, X11 bitmap, PCX, XPM, and a variety of others. (If you have an image in a different format, you may be able to use the convert command to change it to a format you can display.) Here is an example of the syntax of the xv command for displaying an image as your desktop background:

```
`$ cd /usr/share/pixmaps/backgrounds/space/`
`$ xv -quit -root -max apollol17_earth.jpg`
```

As noted earlier, any of these attributes that you want set each time you start your desktop can be added to your `.xinitrc` or `.xsession` files.

> **TIP:** You can find some nice background images in the Propaganda directories (`/usr/share/pixmaps/backgrounds/Propaganda/*`). There are also many places to find nice background images on the Web, including Digital Blasphemy (`www.digitalblasphemy.com`) and Background Pics for Linux (`http://heimat.de/ruebe/linux/bgs.html`).

# ## Screen saver

There is an option that you can add when you run the X server to have a screen saver come on after a set number of minutes of idle time. Using the `xset` command, you can change that timeout value. (As with the background examples previously shown, your desktop environment will probably take over control of the screen saver function.)

There are different ways to set screen saver timeout when you start X from a shell prompt.

```
`$ x -s 15`
`$ xinit -- -s 15 serverargs="-s 15"`
```

In the first example, you simply run the `x` command with the `-s 15` option to have the screen saver come on after 15 minutes of inactivity. If you run `xinit`, two dashes on the command line indicate that the next arguments are to be passed to the X server (in this case, `-s 15` is passed). The last example isn't a command at all. It is a line in the `startx` command. As the root user, edit the `startx` command and add `-s 15` to the `serverargs` line between the quotes. This causes the `-s 15` argument to be passed to the server.

To change the screen saver timeout after X has started, use the `xset` command as follows:

```
`$ xset s 15`
```

You can also add the `xset` command line to an initialization file (such as `.xinitrc`), to have it set the timeout value each time the desktop starts up. If you simply want the screen saver off, type `xset s off`. To turn it on, type `xset s on`. To have the screen be blanked when it times out, type `xset s blank`.