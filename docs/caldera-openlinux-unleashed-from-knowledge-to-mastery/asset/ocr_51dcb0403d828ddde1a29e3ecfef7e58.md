After finding two blank 1.44MB floppy disks and inserting one in the drive, type the following as root:

```
> dd if=install.144 of=/dev/fd0
```

After the drive has finished writing, remove the disk and label it “LISA”. Then, stick the next disk in the drive and type this:

```
> dd if=modules.144 of=/dev/fd0
```

Remove it from the drive and label this one “Modules”. The Modules disk contains kernel modules that will allow you to install and configure your hardware correctly. The standard install disk only contains drivers for a typical PC; the modules disk contains additional support for nearly every hardware device that is supported under Linux.

Creating LISA and Modules disks is also possible from DOS. To do this, change directories to your CD-ROM drive, which in this example is D:

```
> CD D:\
> CD COL\\LAUNCH\\LISA\\FLOPPY
```

You will now need to create a LISA install disk, along with a Modules disk by using the following commands:

```
> INSTALL_.BAT
> MODULES.BAT
```

Have two blank 1.44MB disks ready.

Creating LISA and Modules disks under Windows 95 is similarly straightforward. After installing OpenLinux Tools (from the CD) under Windows, put a blank disk in your floppy drive, and select Start, Programs, OpenLinux, Create LISA Install Diskette. After the disk is created, put another blank disk in the drive and select Start, Programs, OpenLinux, Create LISA Module Diskette. You’ll now have the disks you need to start up the LISA text-based configuration program.

# Using LISA

To use LISA, simply insert the LISA disk in the drive and reboot your machine. You’ll want to place the Caldera OpenLinux 2.2 CD-ROM in the drive as soon as your system begins booting. A prompt will be displayed that looks like this:

```
boot:
```

Simply press Enter, and the installation process will begin. You should be presented with a series of blue text-based menus that allow you to configure your new installation to your liking. The first ones you will encounter are fairly straightforward, allowing you to select your language and keyboard map. You’ll then be asked whether you want to use a