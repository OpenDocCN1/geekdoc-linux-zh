
## Fine-Tuning the X Window System

If you cannot get the X Window System to work on your computer, or if you are not satisfied with the results, you can fine-tune the X Window System by making changes to the configuration file that controls how the X server acts to service your particular combination of video hardware and peripherals. The configuration file that controls the X server for the XFree86 version of the X Window System for Linux is the /etc/X11/XF86Config file.

The X Window System consists of a collection of servers that can be tailored to fit any unique combination of graphics card and monitor hardware that you might have. After the configuration of the X server is done, the server configuration is stored in the /etc/X11/XF86Config file. When the X server is started, it reads the /etc/X11/XF86Config file and then sets up the multimedia and video display on your computer. To make changes to the X Window System installation on your computer, you edit the XF86Config file. This can be done by editing the file in a text editor or by using a configuration utility.

![](img/782ecfdc0b083a767896cc983e10427f_288_0.png)

> Because it is possible to damage your equipment by making the wrong choices in the /etc/X11/XF86Config file, and because the configuration of video devices is a complex and technical process that's outside the experience of most users, you should not try editing the /etc/X11/XF86Config file by hand.

The /etc/X11/XF86Config file tells the X server where to find the databases for color palettes, where the font libraries are stored, what peripheral devices to operate, what the video card and monitor parameters are, what the keyboard layout is, which special features to run for your mouse, and much more. You can find out a lot more about the information contained in the /etc/X11/XF86Config file by looking at the sample file that was loaded along with the default X installation when you installed Linux. The sample file is called /usr/X11R6/lib/X11/XF86Config.eg and is shown in Figure 18.1.

### FIGURE 18.1
The mouse section of the /etc/X11/ XF86Config file.

![](img/782ecfdc0b083a767896cc983e10427f_289_0.png)

## Task: Reading the XFree86 Documentation

If you had problems with the video setup during the installation, you might want to read some of the specific documentation for your video card and monitor. Because every system is different, it is difficult to tell you exactly how to set up your system. Your best bet is to be prepared before you begin. Here’s where you’ll find more information to help you through the X Window System configuration process:

- 1. Learn more about the XFree86 Project; get on the Internet and navigate to www.xfree86.org.
- 2. Find helpful information in the Linux filesystem. Change to the /usr/X11R6/lib/X11 directory (shown in Figure 18.2).
- 3. See whether your monitor is supported. Read the /usr/X11R6/lib/X11/MonitorsDB file.
- 4. Make sure your video card is supported. Read the /usr/X11R6/lib/X11/CardsNames file.
- 5. Read the Quick Start guide to give you a little more background information (and confidence) before you begin. This file is located at /usr/X11R6/lib/X11/doc/QuickStart.doc. You might also want to read the README.Linux file.

### FIGURE 18.2
Look in the filesystem to find information to help you configure the video settings.

![](img/782ecfdc0b083a767896cc983e10427f_290_0.png)

- 6. Read the documentation for your particular video card. You'll find this information in the /usr/X11R6/lib/X11/doc directory. There are several README files for each of the supported video cards. For example, if you have an NVidia card, read the README.NVIDIA file.
- 7. Read about mouse support and support for other input devices, such as joysticks and graphics tablets. These files are named README.mouse and xinput.
- 8. Back up the /etc/X11/XF86Config file before you begin. To back up the /etc/X11/XF86Config file, you must be logged in as root. At the command line, type the following:

```
cp /etc/X11/XF86Config /etc/X11/XF86Config.old
```

This command copies the original /etc/X11/XF86Config file to a file with a different name that won't be overwritten. That way, in the instance that your tinkering around renders something inoperable, you can always copy the file back.

## Using Configuration Tools to Tune X

Wizards are available to make the editing of /etc/X11/XF86Config file manageable. These programs guide you through the configuration by helping you select from lists of options to edit the file. When the editing is finished, the wizard saves the new configuration in the same place where the old one is saved. In fact, it will overwrite any /etc/X11/XF86Config that you have in the /etc/X11 directory. This is the reason that you made a copy of this file in the previous task.

![](img/782ecfdc0b083a767896cc983e10427f_291_0.png)

> Many Linux distribution vendors have created their own configuration utilities for the /etc/X11/XF86Config file: Red Hat has XConfiguror, SUSE has SAX, Mandrake has XFDrake, and TurboLinux has turbocfg, to name a few. All these vendor-supplied programs should work to varying degrees to get you through the configuration of your X server. However, since the arrival of X11R6 release 4.0, many of these distribution specific utilities don't function as well anymore and need updating. But, as luck would have it, the X.org people already have an updated utility, xf86config, that is present in all Linux distributions so that's the one we will concentrate on in this hour.

## Task: Configuring X11 with the xf86config Command

To begin configuring the X Window System to fine-tune your video display, you will need to be logged in to the root account. As you step through each process, you might want to keep your Linux diary next to you and write down the steps you performed during the configuration. To begin working with xf86config, perform these steps at the command line:

- 1. Start the configuration process. Type xf86config and press Enter. The opening screen appears. Read the information and press Enter to move to the next screen.
- 2. Select your mouse. Several mouse types (as shown in Figure 18.3) are listed. Type the number that applies to the mouse that is attached to your computer and press Enter. If you use a two-button mouse, you will be asked whether you want the mouse to act like a three-button mouse. Type y and press Enter.
- 3. Select a mouse device. Press Enter to select the default device of /dev/mouse.
- 4. Select to use Xkeyboard extension. Type y and press Enter.
- 5. Select a keymap (the type of keyboard that is attached to the computer). Press Enter to display the list of keyboards. Type the number that corresponds to your keyboard and press Enter.
- 6. Set monitor specifications. Press Enter to display the list of available monitor types (shown in Figure 18.4). Type the number that most closely matches the specifications for your monitor and press Enter.

### FIGURE 18.3
Select a mouse from the list.

![](img/782ecfdc0b083a767896cc983e10427f_292_0.png)

Choose a mouse

Type corresponding mouse number

### FIGURE 18.4
Select a monitor type from the list.

![](img/782ecfdc0b083a767896cc983e10427f_292_1.png)

Choose a monitor type

Type corresponding monitor number

- 7. Select a vertical sync range. Type the number that corresponds to the vertical sync range for your monitor and press Enter. You will next be asked a few questions about the monitor, such as the vendor's name and the model number. You can type answers, or just press Enter to accept the defaults.
- 8. Select a video card. Type y and press Enter to look at the card database. Scroll through the list (by pressing Enter to move from page to page) until you find the video card installed in the computer. When you find the card, type the corresponding number (it appears to the left) and press Enter. The information that appears is important. It might look something like this:

Your selected card definition:
Identifier: SIS 620
Chipset: SiS620
Server: XF86_SVGA
Do NOT probe clock or use any Clock line.

You will need to remember the information in the last line for use later in the configuration process. Press Enter to keep going.
- 9. Select a server. Type 5 and press Enter to use the server for the card that you selected in step 8. You will be asked whether you want to create a symbolic link. Type y and press Enter.
- 10. Select the amount of video RAM installed on the video card. Type the corresponding number and press Enter. You will then be asked to provide information about the video card. You can just press Enter to move through these fields.
- 11. Provide a Clockchip setting. Select a number from the list and press Enter. Or, if the card definition said to NOT probe clocks or use any Clock line, just press Enter.
- 12. Probe the clock. Type y and press Enter if you want to use X -probeonly unless the card definition said not to. In that case, type n and press Enter.
- 13. Change the color depths. The list shows the order in which you can cycle through color depths. If you want to change the order, select the number that corresponds to the color depth you want to change. Read the directions to help you through each color depth that you change.

![](img/782ecfdc0b083a767896cc983e10427f_293_0.png)

> When you change color depths, you will be asked whether you want a virtual screen that is larger than the physical screen. Type n and press Enter if you don't want a display that is larger than the monitor screen. This option is useful only if you are working on a laptop.

- 14. You're now at the end. Write the configuration to the /etc/X11/XF86Config file. Type y and press Enter.
