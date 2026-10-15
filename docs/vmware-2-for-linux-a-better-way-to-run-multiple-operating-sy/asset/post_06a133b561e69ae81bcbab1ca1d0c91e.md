
See Figure 17.17 for an example of a Basilisk II session installing MacOS. When installing MacOS, keep the following in mind:

- Rather than try to match the system files to the exact Mac model you are installing, use the Install for Any Macintosh setting.
- If the installer asks you to upgrade your disk controller driver, ignore it.
- Not all QuickDraw functions work properly in emulation, but you should be safe installing the drivers. Some software that relies on advanced graphics features might not work up to spec, however.

![](img/b2b6702758c230ce537468351fc8af15_363_0.png)

After MacOS is installed and you reboot the emulation, the Macintosh software world is your oyster. You can navigate the Finder, copy programs from your PC through the My Computer or UNIX icon, and adjust the Mac's control panels to tweak the experience to your liking. A sample Macintosh emulation desktop appears in Figure 17.18.

To install new programs, simply insert the floppy (remember, high-density only) or CD-ROM containing the Macintosh software, and follow the standard installation instructions. Unlike Executor, you can run multiple programs at once, just as you can on a real Mac. See Figure 17.19 for a demonstration.

Basilisk II's wide range of software compatibility allows you to run the vast majority of the entertainment, education, and productivity applications designed for the Macintosh since MacOS 7 became the standard. Even with the speed impact of

![](img/b2b6702758c230ce537468351fc8af15_364_0.png)

Figure 17.18 Basilisk II is up and running, ready for action.

![](img/b2b6702758c230ce537468351fc8af15_364_1.png)

Figure 17.19 Shosun running is an atlas program (upper left), a text adventure game (lower left), and a personal journal program (lower right).

emulation, a modern VMware-capable PC has much more storage and memory (and sometimes even speed) to offer Mac applications than the most impressively equipped 68K Macintoshes of old.

> Whenever possible, use the Special, Shut Down command to quit Basilisk II, just like you would a normal Macintosh. If that is impossible, you can use Alt+F4 in Windows, or send a Ctrl+C in the command window you launched Basilisk II in, to break out of the emulator. Note that you will probably be pestered by the same warning (see Figure 17.20) you would see on a real Macintosh the next time you launch the emulator.

![](img/b2b6702758c230ce537468351fc8af15_365_0.png)

Figure 17.20 Just like the real thing, an emulated Mac complains if you do not use the proper shutdown command to end your session.

## Conclusion

The decision to run Linux or Windows is largely one of software. Until emulators came along, PC users were barred both by software and by hardware from running Macintosh applications. Through ARDI Executor or Basilisk II, you can sidestep the hardware barriers and add an entirely new range of software to your library without adding a new Macintosh to your desk.

The next chapter explores other, non-x86 computers you might want to emulate in Linux or through a Windows virtual machine.

## Chapter 18: Exploring More Emulators

- Using UAE Amiga Emulator for Linux
- Using MAME Arcade Game Emulator for Linux
- Using VICE Commodore 64 Emulator for Linux
- Running other emulators

Emulation doesn’t begin and end with Windows and Linux, or even with the Macintosh. It would only be a slight exaggeration to say that nearly every computer ever widely manufactured and sold has a corresponding emulator; there are even emulators of classic handheld electronic games!

There are too many emulators for Linux and Windows to treat individually in this book. In this chapter, I highlight a few of my favorites, which are relatively easy to install and run, either in Linux or in a VMware Windows virtual machine.

> Most of the emulators in this chapter require you to compile the source code yourself. Although this process is relatively automated, things can occasionally go wrong. Be sure to read the installation documentation included with each emulator before you attempt to install the program; the specific instructions are more detailed than this book can be and contain valuable troubleshooting information.

### Using UAE Amiga Emulator for Linux

The Commodore Amiga was the world’s first true multimedia computer. Launched in 1985, the Amiga brought color, sound, and robust multitasking to market arguably before the world was ready, and after selling only about five million computers, Commodore went out of business in 1994 and the Amiga fell out of mass production. See Figure 18.1 for a classic Amiga image.

For years, the Amiga’s high-power graphics and sound hardware made emulation seem infeasible, but the combination of rapid advances in PC processor speeds and hard work on the part of an international open-source effort resulted in the UAE Amiga emulator.

### Installing UAE

The good news is that you might already have UAE installed on your system, or available from your Linux distribution CDs, because it ships with a number of different packages, including SuSE, Debian, and TurboLinux.
