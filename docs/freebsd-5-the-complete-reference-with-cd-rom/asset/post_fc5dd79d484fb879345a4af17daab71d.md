
from sight, and a client as the computer at which a user sits. To better understand the client/server terminology in the case of X (or in any case, really), think of it from the application's point of view. To a program such as a word processor, the keyboard, mouse, and display constitute a set of input/output streams, much like a file server on which data files are stored. To the word processor, then, a network server for handling user input may be remote. The fact that a human happens to sit at that server computer is unimportant to the word processor.

X's network-enabled nature makes it possible to set up a powerful FreeBSD system to run applications for many users and employ much less powerful computers as X display terminals. In fact, an entire class of computer, known as X terminals, is designed for this purpose. X terminals provide little or no independent computational capacity, but provide a keyboard, mouse, and (typically very large) monitor. You can also use one FreeBSD system as an X server for another—in fact, this practice can be a good way to squeeze more life out of an otherwise outdated computer. Even Windows, OS/2, and other non-UNIX systems can function as X servers, if equipped with appropriate software, such as Hummingbird Exceed (http://www.hcl.com/products/nc/xexceed/), Netsarang's Xmanager (http://www.netsarang.com/products/xmanager.html), or a Windows port of XFree86 (http://sources.redhat.com/cygwin/xfree86/).

When used over a network, X is slower than when the X server and X client (the application) run on the same computer. Depending upon the type of network and application, though, this difference might be small enough that it is unimportant.

The basic X configuration for FreeBSD sets it up as a local X server only; you can't use a default FreeBSD system to access X applications run from another computer. Chapter 21 describes configuring X to accept remote connections.

## Reconfiguring X

When you installed FreeBSD, as described in Chapter 2, the system configured X. Sometimes, though, this configuration goes wrong, either badly (so that X doesn't run at all) or subtly (so X runs nonoptimally). In other cases you may need to reconfigure a previously working X, such as when you change a mouse or video card. For whatever reason, reconfiguring X is sometimes necessary, and this section describes how to do it, beginning with a look at the structure of the XF86Config control file. This section then moves on to some common configuration changes: to video cards, to resolution and color depth, to the mouse, and to fonts. This section concludes with a look at some tools you can use to help make these changes.

> **Note** *This section describes configuring XFree86 4.x. The older XFree86 3.x configuration file format was somewhat different from what's described here.*

## Tips for Making Changes

When editing XF86Config, it’s useful to first configure your system to *not* start X automatically at boot time. This configuration enables you to manually start X to test your changes, quickly exit from X, make more changes, and then restart X. A text-mode startup that permits this test cycle is FreeBSD’s default configuration, but if you’ve reconfigured the system to start X automatically, you should undo these changes. One method of starting X automatically, which is described in Chapters 6 and 21, involves running the X Display Manager (XDM) or a similar program from /etc/ttys. By default, this file contains a line like this:

```
ttyv8	/usr/X11R6/bin/xdm -nodaemon xterm off secure
```

The `off` in this line may read `on` if the system starts X automatically. Change it back to read `off`, and then type **kill -HUP 1**. This command will reconfigure init so that it doesn’t automatically launch XDM, but the current instance may continue to run. You may need to log out of any running X session and type **killall xdm** in a text-mode session to terminate XDM and the X login that it provides.

When you make a change to your X configuration, you can type **startx** to test the new setup. (Try doing this as a regular user, not as root, to be sure that all the necessary files are readable or executable by normal users.) When you select the log out or exit option in your window manager or desktop environment, X should close and you should be returned to your text-mode terminal. If this doesn’t happen, try pressing CTRL-ALT-BACKSPACE to kill the X session. In either case, you should see a series of lines with messages from the X server. If all goes well, these will be unimportant; but if something didn’t work correctly, one of these messages may contain a vital debugging clue. Unfortunately, the vital message may have scrolled off the top of the screen. To capture these messages, you can use redirection to save them to a file. For instance, instead of typing `startx`, type `startx &> startx.out` to save the X messages to `startx.out`. You can then examine this file at your leisure for clues to what went wrong.

## Basic Structure of XF86Config

The XF86Config file resides in the /etc/X11 directory. Like most other FreeBSD configuration files, XF86Config is a text file, so you can edit it using any text editor you like, as described in Chapter 5. As with other configuration files, it’s a good idea to back up the file before changing it; that way, if you make matters worse, you can restore the original and try again. Although editing the file directly gives you the greatest flexibility, you may prefer to use a GUI or automated X configuration tool for at least part of the job. The section, “Tools to Help Reconfigure X,” describes such tools.

The XF86Config file is divided into several sections, each of which begins with a `Section` keyword and ends with `EndSection`. For instance, the following is the opening section in a typical configuration:

```
Section "ServerLayout"
    Identifier    "XFree86 Configured"
    Screen        0        "MyScreen"  0  0
    InputDevice    "PS2Mouse"   "CorePointer"
    InputDevice    "StdKeyboard"    "CoreKeyboard"
EndSection
```

This **ServerLayout** section describes the rest of the configuration—it includes an *Identifier* for the configuration as a whole, a *Screen* line to identify the display, and two *InputDevice* lines, one for each input device (the mouse and the keyboard). The *Screen* and *InputDevice* lines point to subsequent sections, which provide more details about the devices in question. Such subsequent sections may optionally refer to still more sections (as the *Screen* section does). Thus, a typical *XF86Config* file describes a hierarchical structure, as illustrated in Figure 13-3. You can trace this structure by reading the identifiers (such as *MyScreen* and *PS2Mouse* in the preceding example) and locating them in *Identifier* lines of subsequent sections. You may want to examine your current *XF86Config* file and create a diagram like Figure 13-3 so you understand its structure. (The diagram you construct will probably closely resemble Figure 13-3.) Some sections in *XF86Config* don’t fit in this diagram, though—they apply to the X server as a whole. Sections you’ll likely find in *XF86Config* are:

-   **ServerLayout** As just described, this section is the top-level configuration; it ties together most of the other sections into a coherent whole.
-   **Files** This section doesn’t tie explicitly into the *ServerLayout*, but it’s very important. It defines the directories in which important XFree86 files can be found, such as font files (specified by *FontPath* lines) and drivers for specific hardware devices (specified by the *ModulePath* line).

![](img/f34d37e3abe9f4517128e54f80ab2616_373_0.png)

**Figure 13-3.** Most sections of *XF86Config* tie together to describe the devices associated with the X server.

-   **Module** XFree86.4.x uses a modular approach to drivers, and this section specifies some of the driver modules the server should load. Normally, you leave this section alone unless you want to enable or disable an advanced feature.
-   **InputDevice** As shown in Figure 13-3, there are usually two *InputDevice* sections, one for the keyboard and one for the mouse. The keyboard section seldom needs work, but you may need to adjust the mouse section if you specified the wrong mouse when you installed FreeBSD.
-   **Monitor** This section provides information about your monitor, such as the range of horizontal and vertical refresh rates it accepts. Properly configuring this section is vitally important—if its options are set incorrectly, your monitor may display no image or display an image at a suboptimal refresh rate or resolution.

> **Caution**
> Old monitors can be damaged if you specify a refresh rate that's too high. If your monitor predates the late 1990s, you should be very cautious about adjusting the *Monitor* section. Do so only with the monitor's manual at hand so that you can set the correct refresh rate values.

-   **Device** This section defines the video card, including the driver for the board and various other low-level details, including the resolution at which the display operates. It's not uncommon to find multiple *Device* sections in an XF86Config file. Typically, one defines an optimized display for your card, and another defines a generic Video Graphics Adapter (VGA) display, which works with most modern video cards, but only at very low resolutions. The VGA definition is likely to go unused once you've created a working optimized configuration.
-   **Screen** This section references the *Monitor* and *Device* sections, as shown in Figure 13-3, to create an integrated display. It includes a specification of the default color depth used by the display.

> **Note**
> These sections might not appear in your XF86Config file in the order in which they're described here. Order in the file is largely unimportant, but I've described them here in a logical order for understanding what these sections do.

## Setting the Screen

As shown in Figure 13-3, XFree86 defines a screen in terms of a video card and a monitor. This configuration is handled through a configuration section that most likely appears near the end of the XF86Config file:

```
Section "Screen"
Identifier "MyScreen"
Device "ATIMach64"
Monitor "EnvisionLCD"
```
