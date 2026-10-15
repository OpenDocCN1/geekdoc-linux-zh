
Purchase a Mac ROM card from Emulators Inc. and obtain the ROMs from either Emulators Inc. or a Macintosh parts/repair vendor. You can then use a program from Emulators Inc. to read the ROM code. Unfortunately, that program only runs in a native Windows environment, so you either need a second computer or a dual-boot machine with a Windows partition to read the code.

In any of these cases, you are required not to use the physical ROMs while you run your emulator. That means if you have a real Macintosh, it should remain off while your emulator is on. If you own a set of the ROMs by themselves or on an Emulators Inc. ROM card, you cannot use those ROMs or the ROM images derived from them on any other computer or emulator.

If this sounds like a lot of work, that's because it can be. Aging Mac II and Mac LC machines are extremely cheap these days, however, and it is probably easiest and least expensive to simply pick up an old Mac, run the CopyROM program, and be done with it. However, you might want to evaluate Executor (ARDI provides a 30-day free trial version) before you invest time and money acquiring the Mac ROMs for Basilisk II.

> Newer PowerMacs, such as the iMac, actually store their "ROM" code in software that is included on the MacOS CD and gets loaded into a special area of memory every time you turn on the computer. Hence, when Power Macintosh emulation finally becomes available, it will actually be easier to legitimately run MacOS on another computer!

## Using ARDI Executor

ARDI has a 30-day free trial version of Executor on its Web site that disables only minor, trivial functions, such as the ability to use certain keyboard shortcuts. The trial version of Executor is also included on the CD that came with this book. It's well worth your time to give it a look.

## Installing ARDI Executor

If your computer is adequately equipped for VMware, installing and running Executor should be a breeze:

> Installing Executor requires that your system support either RPM or DEB packages, and RPM is strongly recommended.

- 1. Head to http://www.ardi.com/download.html. Alternately, you can look in the /Executor directory of the included CD-ROM.
- 2. Select the Linux version of Executor most appropriate to your system. Chances are this will be Linux glibc RPM. Select a download site as well.
- 3. The download should result in a file named something like executor-xxxx-glibc-demo-i386.rpm.tar.gz with the version number replacing the xxxx. Place this in a convenient directory.
- 4. Extract the archive you just downloaded with the command tar -zxvf executor-xxxx-glibc-demo-i386.rpm.tar.gz, replacing the xxxx with the actual version number in the filename. You should see four or five new RPM files.
- 5. There are three versions of Executor: standard, SDL (Simple DirectMedia Layer), and SVGA. Do not use the obsolete SVGA version. If possible, you should install the SDL version.

> The upcoming installation steps might require that you use the su command for root-level access.

- 6. Install the SDL system by typing rpm --install SDL-1.0.6-1.i386.rpm. (The version number might be slightly different.)
- 7. Install the Executor support files with rpm --install executor-aux-2.1pr11-1.noarch.rpm. (Again, the version number might be different.)
- 8. Install Executor itself with the command rpm --install executor-glibc-demo-ds1-2.1pr11-1.i386.rpm. (Substitute the proper version number if necessary.)
- 9. Executor is installed and can be invoked with the command executor-demo-sdl at any command prompt. (If you find it necessary to install the plain version of Executor, the command is executor-demo.)

## Running Macintosh Programs in Executor

When you run Executor, you should briefly see a graphical splash screen, followed by an About box containing information about the demo version and ordering information, as shown in Figure 17.4.

Executor can see your Linux file system without any network trickery or user intervention. Indeed, as part of the installation process, ARDI creates a new directory at /home/executor and fills it with sample Mac programs that work well in the emulator. See Figure 17.5 for an example.

You can use the Browser to install or copy new Macintosh programs to your Linux hard drive (in the special /home/executor directory, if you want to keep things organized).
