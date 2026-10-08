
Command-line interfaces are generally run from a *shell*, which acts as a text-based interface between the Red Hat Linux operating system and you. The *bash* shell, which Red Hat Linux uses by default, displays a prompt like `[lidia@ Cancun lidia]$`. You enter commands at the shell prompt. That's where the term command-line interface (or CLI) comes from.

You can start a shell from within the GNOME interface by starting a GNOME Terminal (also known generically as a terminal emulator). Click the GNOME Menu and then choose System Tools: Terminal (you can also right-click anywhere on the GNOME Desktop and choose New Terminal) to start a terminal session, as shown in Figure 4-2. (You can find out more about the GNOME interface in Chapter 9.)

![](img/8c094d1b36276212c03d10d898508a6e_75_0.png)

You can run individual programs without starting an interactive shell by using the GNOME Run Program menu. Click the GNOME Menu button — the red hat in the lower-left corner of the screen — and choose Run Program. The Run Program window opens; type the name of any program in the text box. The program then runs — if it's graphically oriented. You don't see the output if the program is designed to interact with the terminal screen (the technical term is *standard output*). Entering **xclock**, for example, displays a graphical clock on your screen.

The GNOME Menu button looks like a red hat and is on the toolbar in the lower-left corner of your desktop. The button works in a manner similar to the Windows Start button.

![](img/8c094d1b36276212c03d10d898508a6e_75_1.png)

![](img/8c094d1b36276212c03d10d898508a6e_76_0.png)

The GNOME Terminal is similar to the MS-DOS window in Windows. Opening an MS-DOS window provides a CLI in which to enter DOS commands. The underlying technology of a Windows CLI is different from that of a Linux CLI. However, its capabilities are more or less the same.

## Configuring Your Graphical Display

The Red Hat installation process is good at automatically configuring itself to use your video hardware and display — Linux uses the X Window System (X, for short) to display graphics. However, occasionally the X configuration process fails, or you may want to reconfigure it. Red Hat gives you access to the same configuration tool it uses during the installation process.

The Red Hat X configuration utility is the redhat-config-xfree86 program. We refer to it as simply the Display Configurator. Generally, the Display Configurator automatically detects your display (monitor) and graphics card. After they have been detected, you can set your display's resolution and color depth.

## Configuring with the Display Configurator

You can start the Display Configurator even if you're not running X Window (if you're running in nongraphical mode; nongraphical mode is run level 3):

1. **Log in as root.**

   You're automatically placed in a CLI.
2. **Enter this command at the Bash prompt:**

   `redhat-config-xfree86`

   The Display Configurator window opens. The utility runs within a graphical interface.

You can, of course, start the Display Configurator if your computer is running X. You may want to reconfigure your system, for example. Follow these instructions to start the utility:

1. **Click the GNOME Menu.**
2. **Choose System Settings** → **Display**.
3. **Enter the root password, if you're prompted.**

The Display Configurator opens. Use the following set of steps to configure your graphical (X Window) interface.

![](img/8c094d1b36276212c03d10d898508a6e_77_0.png)

The X Window System (X, for short) was invented at the Massachusetts Institute of Technology (MIT). MIT designed X to display graphical applications across a wide range of machines. It was originally built to run on Unix platforms, but has been adapted to Linux, Windows, and other platforms.

![](img/8c094d1b36276212c03d10d898508a6e_77_1.png)

Old monitors that aren’t multicanning can be damaged if you try to use them at a higher resolution than VGA, which is 640 x 480 and 60Hz (a multicanning monitor can switch to the same signal frequency that a video card is generating). Most newer monitors have built-in protection mechanisms to keep them from burning up in what is known as overdriving, but older monitors don’t have this type of protection. Older monitors can literally catch on fire. If you hear weird noises from your monitor or smell burning components, turn off your computer immediately!

## Configuring manually

You can manually change your display settings if the Display Configurator doesn’t automatically detect them. These steps describe how to access and use the advanced Display Configurator features:

1. **Start the Display Configurator** and **click the Advanced tab.**

   Figure 4-3 shows that you can configure the monitor, the video card, and multiple-head computers (to use more than one monitor at a time). A description of multiple-head systems is beyond the scope of this book.

![](img/8c094d1b36276212c03d10d898508a6e_77_2.png)

Figure 4-3: The monitor Advanced Settings dialog box.

The Advanced Settings window shows the monitors available to you by default.

2. Try to locate and select your particular monitor.

   You have dozens and dozens of monitors to choose from, so you have at least as good a chance of finding yours as winning the PowerBall. If not, your best bet is to rummage around in the Generic section.

   Generic monitors include several laptop configurations and old-fashioned heavy ones. If you don’t know what type fits your monitor, take a guess and try one. Keep trying different generic monitors if your first choice doesn’t work.

   Click the OK button and return to the advanced settings window.
3. Click the Video Card Configure button. Control is sent to the Video Card Settings window, as shown in Figure 4-4. Select your video card from the long list of choices.

![](img/8c094d1b36276212c03d10d898508a6e_78_0.png)

You can tell the Display Configurator to probe and locate your video card for you by clicking the Probe Videocard button. Your card is most likely detected and highlighted for you.

The lowest (8-bit) option allows only 256 colors on the window at one time. The 16-bit option allows for 65,535 colors, and 24-bit allows for more than 16 million colors (also known as *true color*).

4. Click the OK button to return to the Advanced Display Settings window.

![](img/8c094d1b36276212c03d10d898508a6e_78_1.png)

![](img/8c094d1b36276212c03d10d898508a6e_79_0.png)

## Delving deep into color depth

Color depth, the number of colors your system can have active on the window at any one time, is loosely a function of both the amount of video memory contained by your system and the window resolution.

If your system has a small amount of memory (such as 1MB), your screen can have a resolution of 1024 x 768 pixels (dots) with 256 colors (8 bits) on the screen at one time. If your system has 2MB, you can have 64K colors (16 bits) on the screen at the same time at the same resolution. If you have an older video board with a small amount of video memory but some additional video memory sockets, you may be able to upgrade the amount of video memory on the video card.

If you have only 1MB and want to see 64K colors on the screen at one time, you can reduce your resolution from 1,024 x 768 to 800 x 600 pixels. If you want true color (24 bits), you can set your resolution to 640 x 480 pixels. The picture you're viewing takes up more of the screen, but color depth versus resolution is a trade-off you can make by choosing the right options.

When you want to display an image and the color depth isn't correct, nothing drastic happens. The picture may look lackluster or not quite normal. X has an interesting capability to have virtual color maps, which allow the active window to utilize all the colors of the bits of color depth, even if other windows are using different colors. When this option is turned on (as it is with the Red Hat distribution on this book's companion DVD-ROM), the various windows turn odd colors as your mouse moves from window to window, but the window that your mouse activates is shown in the best color available. With newer video cards and larger video memories, which allow for true color at high resolutions in every window, this option is less useful.

5. Click the OK button and the Display Settings window closes.

   An Information window opens, informing you that you need to log out and log back in to make the changes take effect.

   Log out and log back in to make the changes take effect.

![](img/8c094d1b36276212c03d10d898508a6e_79_1.png)

You can also restart X in emergencies (for example, if it freaks out) by pressing Ctrl+Alt+Backspace. Your current X session is stopped and eventually restarted. You can then log back in.

## Creating User Accounts with the Red Hat User Manager

If you have cause to add new users (if you have a home network, for example) or you forgot to create a nonroot user during installation, this section
