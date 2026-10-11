
## CAUTION

If you replace a video card, be sure to configure your system not to start X automatically when it reboots with the new card. This task can be accomplished by editing the /etc/inittab file. Specifically, a line in this file reads something like `id:5:initdefault:`. The number (5, in this case) is the runlevel—a code indicating what set of services the system runs. On most Linux systems, a runlevel of 5 corresponds to a full X startup, whereas a runlevel of 3 invokes a text-mode startup. Some Linux versions use different runlevels, though, and there are usually comments in /etc/inittab explaining the details. I recommend setting the runlevel to produce a text-mode boot when you change video cards. You can then test your new X configuration by running `startx` and, when you're satisfied with the results, change the runlevel back to a full GUI bootup. If you fail to make this change, it's likely that when you next start the computer, X will try to start, fail, then try to start again, fail, and so on. The result is that you won't be able to use the computer except from a network login.

There are several automated utilities available to help configure X. These utilities have names like `xf86config` or `XF86Setup`. Some of these utilities enable you to configure X by answering a series of questions in a text-mode screen, whereas others attempt to start X in a lowest-common-denominator VGA mode in order to let you use a GUI to configure X. Which utility works best for any given card is variable, so you might need to try two or more of these programs before you get a working configuration. You can check which ones are present on your system by using `ls` to search for appropriate filenames in the `/usr/X11R6/bin` directory, as in `ls /usr/X11R6/bin/*conf*`.

## TIP

Configuring XFree86 frequently necessitates that you enter detailed specifications for your monitor. You should therefore have your monitor's manual at hand before you begin this configuration. If necessary, check your monitor manufacturer's Web site or technical support number for the horizontal and vertical refresh rates your monitor can handle.

At its heart, XFree86 configuration is handled almost exclusively through entries in a single configuration file, `XF86Config`. This file is generally located in the `/etc` or `/etc/X11` directory. Like most Linux configuration files, it's plain text, and so can be edited in a text editor. The information it contains is tricky to define by hand, however, hence the configuration utilities.

### Example Configuration

As an example, you can run `xf86config` as root to configure X, following these steps:

1. Type `xf86config` to start the program. It displays a screenful of introductory information, to which you respond by pressing Enter.
2. The program displays several mouse protocols. Select the mouse type you’re using by typing the appropriate number. For instance, 4 represents PS/2 mice.
3. Many X programs assume that a mouse has three buttons, but this isn’t true of all mice. If yours has only two buttons, select `y` in response to the `Emulate3Buttons` prompt.
4. The program now prompts you for your mouse’s device file. On many systems, `/dev/mouse` is a link to the appropriate file, but on others you might need to enter another filename, such as `/dev/psaux` for a PS/2 mouse or `/dev/ttyS0` for the first serial port.
5. Select your keyboard from the list of types, much as you selected your mouse.
6. Enter the horizontal monitor synchronization range, which is the range of horizontal frequencies your monitor can display. This information is normally printed in your monitor’s manual, or you can use the associated resolution and refresh rates that `xf86config` provides. For instance, if you know your monitor can do $1280\times1024$ resolution at $85\mathrm{~Hz}$, you can select option `#10,31.5` – `95.0`.
7. Enter the vertical synchronization range. This is similar to the horizontal synchronization range, but it’s a different parameter. Enter this information from your monitor’s manual.
8. When the program asks for some identification information for your monitor, enter anything you like here, so long as you don’t include a quote character (`'`). This information is used only to help make the resulting `xf86config` file more understandable to humans.
9. You can, if you like, look at a database of video cards. I recommend that you examine this database, because there’s a good chance you’ll find your video card in it, which can simplify configuration. When you find your card in the database, enter its number. `xf86config` presents summary information to confirm that you’ve entered the correct information.
10. Select the X server to use. In most cases, this will be option `#5`, which loads the server specified in the card definition database. You might want to choose another option to override this choice, however.
11. `xf86config` will ask whether you want it to modify the `/etc/X11/Xserver` file to point to the appropriate server file. In most cases, you want to respond `y` to this request.
12. Enter the amount of RAM installed on your card.
13. As with the monitor, `xf86config` prompts you for several strings to identify the video card.
14. For some (mostly older) cards, enter the RAMDAC used in those cards. This is the component that converts video data stored in the video card’s RAM to a signal for the monitor. If you have a newer card, you can type `q` to skip this step; otherwise, you must locate and select the appropriate RAMDAC.
15. As with RAMDAC settings, the clock chip setting is something you don’t need to set explicitly for most recent boards; press Enter to skip setting this value. If you’ve got an older board, you must track down this information.
16. `xf86config` can probe the card for clock settings. On most cards, this step is neither necessary nor recommended, so instruct the program not to do so by typing `n`. On some older cards, you should select `y` instead.
17. Set the default and other supported resolutions. Near the top of your screen you’ll see a series of color depths and associated resolutions. You can set the default resolution for each color depth in turn by typing its number. When you type the number, you’ll see a series of numeric codes for supported resolutions, such as 4 for 1024×768 and 5 for 1280×1024. Type a string of numbers for each video mode. For instance, typing 54 means that 1280×1024 is the default mode, but the server also supports 1024×768. Repeat this procedure for each color depth.
18. As a final security check, `xf86config` asks for confirmation that you want to overwrite the existing `XF86Config` file. If you reply `y`, then the old file will be replaced with the new one.

When you’ve finished writing the new `XF86Config` file, you can test the results by typing `startx` if you’re running in text mode. (If you’ve reconfigured X while in X, you’ll need to exit from X first.) With luck, X will start up without problems. If there are problems, you’ll see an error message in the last few lines of text output. These error messages can be cryptic, but do point back to errors in the `XF86Config` file. One of the most common problems occurs when you specify incorrect horizontal or vertical refresh rate capabilities for your monitor. If X thinks your monitor can’t handle any of your desired resolutions, X refuses to run, in order to avoid damaging your monitor. Another problem relates to the mouse device file; if it doesn’t exist or points to nonexistant hardware, X will fail to run, or run with no mouse pointer available.

## TIP

If your initial configuration doesn’t work, I suggest you back up the `XF86Config` file and run a different X configuration utility. It’s not uncommon for one configuration utility to succeed where another one fails. Even if both fail, you might learn enough from differing error messages and `XF86Config` file details to put together a working `XF86Config` file.
