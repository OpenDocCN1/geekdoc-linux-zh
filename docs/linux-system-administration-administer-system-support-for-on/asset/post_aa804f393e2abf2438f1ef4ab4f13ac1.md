
## Using the X Window System

The popularity of Windows 95 and NT has led many people to think that operating systems without graphical user interfaces don't have a future. Slackware Linux, as well as other UNIX operating systems, have a graphical user interface: the X Window System.

![](img/8ad518fddafc7f5e73715a2604b61d50_165_0.png)

> The X Window System, as a UNIX-specific feature, should not be confused with any version of the Microsoft Windows operating system.

![](img/8ad518fddafc7f5e73715a2604b61d50_165_1.png)

> Slackware Linux comes with XFree86, a free implementation of X provided by the X consortium. Most of the X applications look very similar to any Motif implementation of X such as `xterm`, `xload`, `xclock`, and `xeyes`.

To set up X, first make sure you've included the VGA 16-color X server, and then run the following as root:

```bash
# XF86Setup
```

Before you set up X, check your video card and your monitor's frequency settings to ensure compatibility and support. It also helps to know what type of mouse you have and what Slackware Linux thinks it is.

### Setting Up an X Server

X is a graphical user interface created for UNIX at MIT. X is network transparent, and clients (known as *Xterminals*, basically dumb graphical terminals) which are designed to accept only X traffic from the X server. With Linux, usually the X server and the X client are located directly on the same computer. However, you may need to set up X clients such as Xterminals or X-emulation software for PCs to access your X server from another computer.

There you will setup your mouse, video card, monitor, mode, and keyboard. Your mouse should be the same one you picked at setup. It should work in the XF86Setup mode; otherwise, you'll have to use the tab key to move between fields to get your mouse working properly. You can also have a two-button mouse emulate three buttons, and you can tweak the response times and baud rate of your mouse.

When you’ve done that, you should be able to set up your video card. To set up your video card, choose the appropriate – supported – video card on the list. That’s all you should have to do. Even a high-powered card with tons of video does you no good if it’s not compatible with Xfree86. For a list of currently compatible video cards, consult the Xfree86-HOWTO included in the appendix. (Accelerated video cards such as the S3 chipset are great for X.) The type of bus your computer uses for the video card shouldn’t matter; either PCI or ISA buses should work.

You should also set up the appropriate frequency for your monitor. Multisync monitors are common today, and as long as you have the hardware manual or know the video modes for yours, it should be a piece of cake to configure.

The video mode determines the size of the screen. The smaller the number for the resolution, the larger your X display will be. Where the higher the resolution, the smaller the display. The available preset modes are 640x480, 800x600, 1024x768, 1280x1024, and 1600x1200 (for those will really big monitors or really good eyes). To toggle between modes, use Ctrl+Alt+-(minus) to go down in resolution or Ctrl+Alt++(plus) to increase the resolution.

Your keyboard configuration should not change; so, the next step would be to save the configuration by pressing the Done button at the bottom.

After you complete the XF86Setup, a symbolic link (X) is created to link to XF86_[servertype], depending on your video card and choices. Some Xfree86 X servers are:

```
/usr/X11R6/bin/XF86_Mono
/usr/X11R6/bin/XF86_SVGA
/usr/X11R6/bin/XF86_VGA16
/usr/X11R6/bin/XF86_S3
```

Notice that there a couple of generic X servers, including monochrome, VGA, and Super VGA, as well as X servers for specific graphics cards, including S3 and Mach32 chipsets.

When the link is created, the X server is restarted and xvdtune runs. This enables you to tweak your X configuration file. You’ll see a warning message that tells you that you can damage your monitor this way; but that only refers to the ancestors of Multisync monitors. It’s good for tweaking how far to the right or left, or any little thing. However, if the screen starts behaving weirdly – flashing or drawing lines across the screen – kill the X server by pressing Ctrl+Alt+Backspace.

After you have completed the setup, the .X defaults are created in the users' directories after they run X.

To run X, type startx at the prompt.

```
$ startx
```

Now you have a common desktop. The defaults for applications are in the $HOME/.xinitrc file. A .xinitrc file could look like this:

```
# loads the .Xresources, which defines the look and feel
xrdb -load $HOME/.Xresources
# Sets the root display, can choose colors, patterns, or bitmaps
xsetroot -solid blue &
# start X with applications already running, xclock, xload, and xeyes &
xclock -g 50x50-0+0 -bw 0 &
xload -g 50x50-50+0 -bw 0 &
# xeyes is an X application that follows the cursor by always
# "looking" at it
xeyes 50x50-100+0 -bw 0 &
# start a couple of xterms
xterm -g 80x24+0+0 &
xterm -g 80x24+0-0 &
# start the window manager
fvwm
```

Common window managers include these:

- LessTif (mwm) - a clone of the commercially popular Motif
- Tab Window Manager (twm) - one of the original window managers (not as pretty as LessTif and doesn't manage memory as well)
- Virtual Window Manager (fvwm2) - which gives you virtual root displays and provides more 3D effects than LessTif

Figures 5-3 and 5-4 show the LessTif and Tab Window Manager respectively.

![](img/8ad518fddafc7f5e73715a2604b61d50_167_0.png)

Though not included with Slackware, WindowMaker provides a NeXT-like interface that's handy to configure. Figures 5-5 and 5-6 show the WindowMaker interface in action. You can download WindowMaker from http://www.windowmaker.org.

![](img/8ad518fddafc7f5e73715a2604b61d50_168_0.png)

Figure 5-3: Viewing a LessTif display.

![](img/8ad518fddafc7f5e73715a2604b61d50_168_1.png)

Figure 5-4: Viewing a Tab Window Manager display

![](img/8ad518fddafc7f5e73715a2604b61d50_169_0.png)

Figure 5-5: Viewing the Virtual Window Manager display in WindowMaker (see Tip)

![](img/8ad518fddafc7f5e73715a2604b61d50_169_1.png)

Figure 5-6: Viewing the WindowMaker display (see Tip)

If you are looking to run X from bootup, you can run Linux at run level 4. This will start xdm, the X display manager, which saves users having to run startx every time they log in. However, if your X server starts giving you fits, you might have some problems trying to fix them. In addition, you'll have to change your run level or reboot into single-user mode.

![](img/8ad518fddafc7f5e73715a2604b61d50_170_0.png)

Chapter 6 provides more information on run levels.

## Security and X

A major advantage of X is its network transparency — which can also create a security problem. X is transferred over a cleartext session, which means anyone with a sniffer can access the data. Using X also means you'll have another port open on your network, which in turn means that your host is more vulnerable to attack from the network.

Provided you can control the potential security issue raised by X, it's also possible to let other computers run X applications on your terminal. To control which computers can do so, use the `xhost` command:

```
# xhost +
```

## Fun with X

I taught a UNIX fundamentals class last year and showed the students the joys of X (so to speak). One such delight was `xeyes` — a cute-but-useful application for finding your cursor — as well as how to use `xhost`, and how to send `xeyes` to a neighbor's X display. The command looked like this:

```
$ xeyes -display neighbor:0.0
```

Some of the students had figured out that the up arrow in some shells enables you to go back and reuse a command — and promptly sent 20 xeyes displays to their neighbors' X displays. This made for an amusing class — as long as it stayed in class.

If you can do this operation with a harmless application, consider the possible damage if an intruder tries the same hijinks with a hostile X application. The lesson for administrators is straightforward: Don't allow just anyone to use anyone else's X display.
