
# For installation purists only

You can run the Fedora Core installation system from either a graphical or text-based interface. If the installation process successfully detects your graphics hardware, the graphical method is selected automatically, and that’s the system we discuss in this chapter. In addition to the ease of using a mouse to point and click, the graphical method groups similar configuration choices. For example, the keyboard and mouse selections are presented within one window; not two, as in the text-based installation.

- Your mother told you never to point and click.

- In an unlikely (but possible) turn of events, the Fedora Core installation system found it couldn’t use your graphics adapter. Occasionally the installation system cannot start the graphics interface; in that case, it defaults to text mode. Using the text-mode interface, you use the keyboard to enter information and the cursor (arrow) keys to move you from step to step.

You may have to use the text-based installation for these reasons:

You can select the text-based installation method by typing **linux text** at the **boot:** prompt.

The Fedora Core installation process has a point of no return. That time comes toward the end of the configuration process, after which your disk is partitioned and the software is installed (see the section “Installation Stage 5: The Point of No Return,” later in this chapter). If you stop at or before that point, you keep intact the old operating system and data on your computer.

# Choosing an Installation Type

Fedora Core provides several installation types to choose from. Although we think that you can probably get away with having less space on your system, we decided to give you the minimum disk space requirements that Fedora Core suggests for each installation option:

- **Workstation:** This option adds software-development tools, such as the gcc (GNU C Compiler) compiler, to the Personal Desktop installation process described next in this list. You need at least 3GB of disk space to use this option. We use the Workstation installation option in this book not because we’re programmers but, rather, because the tools often come in handy when you’re installing certain applications. We encourage you to use the Workstation installation type for your Fedora Core installations.

- **Personal Desktop:** This option installs the software necessary to use your computer as a personal workstation. Applications such as Mozilla, OpenOffice, and Evolution plus the GNOME graphical environment give you all the tools you need to enjoy the Internet and get your work done. This installation type requires at least 2.3GB of free space.

- **Server:** Using this option creates an operating-system environment for computers that provide services, such as hosting Web pages. This installation requires at least 1.1GB of free space if you want the minimum number of bells and whistles, at least 1.4GB of free space if you want to install all the bells and whistles but not the graphical X-Window System; and at least 2.1GB to install all the bells and all the whistles, and to throw in the Acme Bell and Whistle Factory.

- **Custom:** This installation type provides two options: minimal and everything. The minimal option installs the bare essentials and nothing more; this option requires only 620MB of space. The everything option installs, as you may have already guessed, every piece of software plus the kitchen sink; you need at least 6.9GB for this option.

- **Upgrade:** Updates the Fedora Core software that is already installed on a computer and leaves all existing settings, users, and data alone. You can optionally choose to install additional packages. Your disk space use should stay roughly the same as your existing installation. Additional packages require additional space, of course.

Both the Workstation and Personal Desktop installation options create a computer you can use for your daily work. In either case, the installation includes the GNOME graphical user interface (GUI) and all the tools that an average computer user (that’s you) needs to survive. If you want software that the installation doesn’t provide, you can always add packages later.

# Installation Stage 1: Beginning the Journey

Before you install Fedora Core, you need to insert the companion DVD into the DVD/CD-ROM drive and boot or reboot your computer. The instructions in this section describe how to start installing Fedora Core on your computer.

This section gets you started with the Fedora Core installation process. Use these initial steps to start the installation and perform some basic configuration:

1. Insert the companion DVD and boot (start) your computer. (If your computer can’t boot from a DVD, use the coupon on the back of this book to obtain Fedora Core CD-ROMs.)
   After contemplating the meaning of life, your computer displays the first installation screen, which includes the boot: prompt.
2. Press Enter.
   A series of messages scroll by, indicating the hardware that the Linux kernel detects on your computer. Most of the time, particularly with newer systems, Fedora Core detects all the basic hardware. Then the Fedora Core installation process starts and the Welcome to Fedora Core window opens.

![](img/41feae212f5c6612ff709354891f7b39_49_0.png)

If the installation process crashes at this point, reboot your computer and add the `nofb` option after the boot: prompt (for example: boot: nofb). If that fails, reboot and use the text installation mode: boot: linux text. Also, Sony Vaio notebook users may need to enter the option `pci=off` `ide1=0x180,0x386` at the boot: prompt to make their CD-ROM drive work correctly.

3. If prompted with the CD Found screen, you can select to verify that your DVD or CD-ROMs are error-free. (Refer to the sidebar “Checking your discs.”) Otherwise, press Tab to select the Skip option and then press Enter.

4. Click the **Next** button.
   The Language Selection window opens.

![](img/41feae212f5c6612ff709354891f7b39_49_1.png)

You can view information about Fedora Core by clicking the **Release Notes** button, in the lower-left corner of the screen. Additional information about where to find more information is displayed on the informational sidebar on the left side of the information window.

5. Select a language (if you don’t want the default of English) and click **Next**.
   Choose the language you speak — or, if you’re feeling adventurous, one you don’t (not recommended).
   The Keyboard Configuration window appears.
6. Select your **keyboard configuration** and then click **Next**.
   Usually Fedora Core detects and configures your mouse, but if it doesn’t, the Mouse Configuration window opens.
7. If prompted (unlikely), select your mouse (squeak!) and click **Next**.
   - If you have a PS/2 mouse, all you have to do is select the manufacturer and the number of buttons.
   - If you have the older style of mouse that connects via a serial port, you have to select the manufacturer, number of buttons, and serial port to which it’s connected: you can only four serial ports to select from (in many cases, only two: either `ttyS0` or `ttyS1`).
   - If you have a two-button mouse (either serial or PS/2), you can choose to have it emulate three buttons by selecting the **Emulate 3 Buttons** option. You emulate the third (middle) button by pressing both mouse buttons at one time.
8. In the **Installation Type** window, select the **Workstation** option and click the **Next** button.

# Checking your discs

Fedora Core provides a validation mechanism for checking its DVD or CD-ROMs. If your distribution disc is a DVD, Fedora Core uses numeric keys to help verify that it isn't corrupted: You can enter **linux mediacheck** at the **boot:** prompt, at the beginning of the installation process, to verify the disc's integrity. Follow these steps to verify that your DVD is in working order:

1. Select the **OK** option by pressing the **Enter** key if you want to verify that your DVD (or CD-ROM) is okay.
2. Press the **Tab** key to select the **Test** option and press the **Enter** key to start the integrity check.
   The media-check system displays a progress meter and then shows the result in the Media Check Result window when it’s finished. The possible results are **PASS** and **FAIL**.
3. Select the **OK** button (the only option) in the Media Check Result window.
4. Assuming your **DVD** passed, re-insert the DVD and select **Continue**.
5. If you’re testing **CD-ROMS**, insert the second or third **CD-ROM** and repeat Steps 2–4 for each **CD-ROM**. You’re finished after testing the third **CD-ROM**.

Obviously, if the DVD (or any of the CD-ROMs) fails the test, you shouldn’t use it. You should buy another copy of this book. (No, no – just kidding.) Contact the Wiley Photo Technical Support department, at www.wiley.com/techsupport, to find out how to get a replacement DVD (or CD-ROM).

# Installation Stage 2: Slicing and Dicing the Pie

You must decide where on your hard drive to install Fedora Core. This process, called *disk partitioning*, divides the disk into multiple sections. Fedora Core is then installed on its own partitions.

Fedora Core provides both automatic and manual methods for creating disk partitions. We use the Fedora Core automatic method because it’s easy. The automatic method erases any existing Fedora Core partitions, but doesn’t touch any existing Windows partitions. If you don’t have any existing Fedora Core partitions or unused space on your disk, you have to make some free space. Refer to Chapter 2 for instructions on how to shrink Windows partitions to make space for Linux.
