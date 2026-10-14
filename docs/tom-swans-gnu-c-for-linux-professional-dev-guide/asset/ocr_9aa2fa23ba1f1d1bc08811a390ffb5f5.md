It’s okay to select Custom even if you are unsure about the exact sync frequencies for your monitor. In that event, however, you should select a relatively safe entry such as Standard VGA, 640x480 @ 60 Hz or Super VGA, 800x600 @ 56Hz and go on to the next step. At least, this will let you start using Linux until you can figure out the proper settings, which you can specify later.

Select the Probe command to begin an auto-detection phase of the installation that attempts to identify your video hardware. This is done in addition to configuring your monitor—auto-detection probes your video card or circuitry to determine how much memory is available and what display modes are supported. Most modern video systems are correctly identified, and if the displayed test screen looks right, you can proceed. However, if auto-detection fails, you must enter the amount of memory in your video system, the number of bit planes, and select one or more resolutions. If you are unsure about these settings, try the highest values that seem to work. (For best results, X needs a resolution of at least 800-by-600. It works only marginally with a 640-by-480 display.)

Finally, you are asked whether to start Linux in graphics or console mode. I prefer console mode because it shortens boot time, but this requires me to log in and then enter *startx* to run X. If you want to run X at startup, that’s fine.

> **Tip**  After installation, a complete log of the steps taken is stored in the file `/tmp/install.log`.

# BOOTING LINUX

You have now installed Linux and are ready to begin using your new operating system. Remove all floppy disks and CD-ROMs, and reboot. If you set up your computer as a stand-alone system, Lilo boots directly into Linux after a 5-second pause. If you have a dual-boot system, Lilo waits briefly for you to select an operating system. Enter *dos* to boot into Microsoft Windows, or just press Enter to boot to Linux. If Lilo times out, it automatically boots the Linux kernel (but see the tip at the end of this section to change the pause time).

The first step after booting is to log in as root. You must do this even if you are running Linux on a standalone workstation. During installation, you were given the opportunity to create a login name and password. Enter these now at the login prompt.

Some users see a graphics display for logging in; others log in at a character-based terminal. Either way, after logging in, you should see a prompt of some kind in a terminal window, probably with a blinking dollar sign ($). If not, look for a button, a command, or an icon of some sort that opens a terminal window. This might be called a console or a terminal. You’ll use this console mode to compile and run the sample programs in this book, as explained in the coming chapters.

If you see a character prompt after logging in, and you want to run the X windowing system, enter *startx* at the prompt. Because of the many routines and window managers available, I can’t predict what you’ll see at this point. Probably, you see a graphics screen