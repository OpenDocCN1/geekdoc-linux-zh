
At the Password for root prompt, guess what you’ll be asked? Here’s where you’ll set the root password. Now, you might be asking, what in the world is root? Root is a special administrative account that should only be used for system configuration. This password is essential. Whatever you set it to, make sure that you don’t forget it. Otherwise, you might have to reinstall the system. Note that your characters will not show as you type the password in. This is so that someone can’t look over your shoulder and steal your password. After entering it once, you’ll be asked to enter it again so that the computer is sure you typed it correctly.

Accounts are covered in more detail in the first few chapters in the book. For now, just remember this password.

## Creating the First Account

If you should only use the root account for system configuration, what account do you use on a day-to-day basis? The step following the root password setup is where you create your own home account. This is the account that you normally use when working with Linux. Select a username (eight characters, no spaces). Typically, your account will be your first name or a combination of your first and last names, although it could be your nickname. Enter the first letter of your name followed by your last name, or anything else you like.

Leave the UID displayed as it is (100).

Select users standard group.

Press Enter to set the user’s home directory. It should read /home/username where username is the username you selected for your account.

On the shell selection, leave GNU bash as the default option.

Enter your full name and provide a password for your account. Again, your characters will not display as you type them, and you’ll be asked to enter the password twice.

Don’t forget your username and password; you’ll need them to log in. Note that passwords and logins are case sensitive.

## Configuring LILO

The next few steps configure the LILO boot manager. LILO is the software responsible for starting your computer when you use Linux. If Linux is sharing your computer with another OS, LILO can provide you with a choice of OSs when you start your computer. To do this, LILO must be installed on the first hard disk’s MBR (master boot record).

Some OSs, like Windows NT, don’t like LILO very much. For a multiboot system with NT, you’ll need to install LILO on the Linux root partition instead of on the MBR and configure the NT loader to give you a choice when you start your box (computer). Other OSs like MS-DOS, Windows 95, and Windows 98 work fine with LILO on the MBR.

When installing LILO, you will be asked to choose a Linux kernel for your system. Select the default (/boot/vmlinuz) and press Enter. If you are asked to provide an initial ramdisk file image, select the default file by pressing Enter. If you are asked to name the boot image, the default name linux should be used. At the boot parameter box, press Enter to accept whichever values appear by default, unless you do need to add some special parameters for your hardware. When the LILO installation menu displays again, select No further entries to add to LILO and press Enter to display the configuration file LISA has built for you. Press Enter to continue, and when the Install LILO as configured dialog box is displayed, press Enter once more to install LILO.

## Configuring Daemon Services

Say OK to the options listed for the daemon/server autostart. These options should be left alone unless you know what you are doing. If you need to alter these settings at some point in the future, you can do them using LISA without having to reinstall Linux.

## Configuring X Windows

To configure X Windows, select the X11 server appropriate for your card and press Enter.

Select Yes to call XF86Setup right now. For LISA, “right now” really means “postpone this until the installation is finished,” so you won’t see XF86Setup until later.

If you have another floppy disk handy, save your configuration to a diskette in case you need to restore it later. This will save you from having to manually reconfigure the install.

Congratulations! You have installed most of Linux on your system. Your computer will now boot into Linux, and afterward, you’ll be able to setup the X server. During the boot process, you’ll notice some scrolling status information while Linux starts. This process will take anywhere from several seconds to several minutes, depending on the speed of your computer.

## XF86Setup

After your computer finishes booting into Linux, you should see a graphics screen with an X-shaped mouse pointer. After a few seconds, the XF86Setup program will be displayed.

If your mouse is working, you can use the mouse to click on boxes and select various options. Otherwise, you might have to use your arrow and Tab keys to move among the various options. Use the Enter key to activate the option.

## Mouse Settings for X Windows

The mouse configuration screen allows you to set the details about your mouse (see the next figure). Linux likes mouse devices that have three buttons. If your mouse only has two, you might want to consider purchasing an inexpensive three-button mouse. Your other alternative is to select the Emulate3Buttons option. This will require that you press both mouse buttons at the same time to simulate the middle one.

Note that configuring a nonworking mouse can be tricky. For example, some newer Logitech mouse devices use the Microsoft protocol, whereas some older Microsoft mouse devices use the Logitech protocol. If yours is an older mouse, try to match the name of the mouse to the name of the protocol. If yours is a newer serial mouse, it is most likely a Microsoft mouse, regardless of its manufacturer. If your mouse is connected to a PS/2 mouse port, select the PS/2 protocol. If your mouse is already working, just let it be!

![](img/edf072a03d4de1f8f4a13465ac79e7fb_311_0.png)

The mouse configuration option allows you to fine-tune and configure your mouse settings. If your mouse is working, you should leave most of the settings as they are by default.

## Keyboard Configuration

To begin keyboard configuration, select the Keyboard button at the top of the display (see the following figure). More than likely your keyboard is already working properly. One setting that many people like is assigning the Caps Lock key (to the right of the A key) as the Ctrl key. This is only one of the possible options. The keyboard selection also has settings for specific keyboards from Dell and other vendors, including laptop models. Check this option to see if you have one of those listed. Click the Apply button when you have completed your configuration.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_311_1.png)

The keyboard option allows you to select a keyboard and to control various options such as the location of the Ctrl key.

## Video Card Configuration

To begin video card configuration, select the Card button at the top of the display. The following figure shows you your video card configuration. Provided you selected the appropriate X11 server to match your card, you should be able to specify a minimum number of settings to have your card recognized. You will want to specify the amount of Video RAM you have and the chipset. If you know the exact card and chip settings (an S3 86C375/86C385 type of thing), you can click on the Card List button, pick the correct card, and then press Detailed Setup.

If you don’t know a specific value, use the Probed options. XF86Setup will try to query the card for the unknown information. If your card is unknown, you might want to try the SVGA settings. The system won’t be able to make use of advanced features available for your card, but you’ll be able to work while you find more information about your system.

## Configuring Your Monitor

To begin monitor configuration, select the Monitor button at the top of the display, as shown in the next figure. You’ll need to know the specs for your monitor and supply the appropriate range for horizontal and vertical refresh rates. If you don’t know them, you’ll need to pick one of the options listed. Note that it’s very important that you supply the correct options for your monitor. Using incorrect refresh rates will overdrive your monitor, possibly wrecking it. This is more of an issue with non-multisync-type monitors. If you have your monitor manual, you should enter the settings yourself by hand.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_312_0.png)

This is the configuration screen for your video card. Note that you can assign multiple settings by clicking the Card List button and picking your card.

Laptop monitors can be especially tricky. Newer laptops might work without problems using standard 640×480, 800×600, or 1024×768 modes. (Select the resolution that matches your laptop’s display.) Some laptops, on the other hand, might exhibit display problems. On my laptop I have been unable to find the proper setting, so when I boot into X-Windows, my screen dances. My fix for a number of years has been to switch between monitor output options (internal and external), and that somehow fixes the problem for the session.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_312_1.png)

Monitor resolution selects the refresh rates your monitor is capable of supporting. Overclocking a refresh rate will kill a monitor.

## Selecting Resolutions

To begin resolution configuration, select the Modeselection button at the top of the display. You’ll see the screen shown in the next figure. Depending on the amount of video RAM your video card has, it might be possible to specify various resolutions and color settings. By default, X-Windows will use the biggest resolution the card can handle. In some environments, this means enabling a virtual screen in which the screen drops off the right and bottom edges. Moving the cursor to the right or bottom edges scrolls what you see. To me, this sort of setting is disturbing, so I specify settings that match what my monitor can do.
