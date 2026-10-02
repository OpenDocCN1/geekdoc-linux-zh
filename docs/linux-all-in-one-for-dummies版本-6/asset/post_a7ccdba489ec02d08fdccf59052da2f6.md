
to hang with a gray screen. If this problem happens to you, here’s how you can troubleshoot it:

- **1. Press Ctrl+Alt+Delete to reboot the PC.**
The PC starts to boot. You get to a screen where GRUB (GRand Unified Bootloader) prompts you for the operating system to boot. (If the distribution uses LILO as the bootloader, you get a text prompt.)
- **2. For GRUB, press the A key to add an option that tells the Linux kernel to boot to a prompt; for LILO, skip this step.**
The GRUB bootloader displays a command line for the Linux kernel and prompts you to add what you want.
- **3. For GRUB, type a space followed by the word single and press Enter; for LILO, type linux single and press Enter.**
The Linux kernel boots in single-user mode and displays a prompt that ends in a pound sign like the following:

```
#
```

Now you’re ready to configure X.

X uses a configuration file (XF86Config-4 or xorg.conf, depending on the distribution) to figure out your display card, your monitor, and the kind of screen resolution you want. The Linux installer prepares the configuration file, but sometimes, the configuration isn’t correct.

To create a working configuration file quickly, follow these steps:

- **1. Type the following command:**
The X server runs and creates a configuration file. The screen goes blank; then the X server exits after displaying some messages. In Fedora, the last line of the message says the following:
- **2. Use a text editor such as vi to edit the /etc/xorg.conf.new file, and insert the following line after the line Section "Files":**
In Fedora, you must also change /dev/mouse to /dev/input/mice.

```
X -configure
```

```
To test the server, run 'X -config /etc/xorg.conf.new'
```

```
FontPath "unix/:7100"
```

- **3. Type xfs & to start the X font server.**

- **4. Try the new configuration file by typing the following line:**

```
X -config /etc/xorg.conf.new
```

If you see a blank screen with an X-shape cursor, the configuration file is working fine.

- **5. Press Ctrl+Alt+Backspace to kill the X server.**

- **6. Copy the new configuration file to the /etc/X11 directory with the following command:**

```
cp /etc/xorg.conf.new /etc/X11/xorg.conf
```

- **7. Reboot the PC by pressing Ctrl+Alt+Delete or typing reboot.**

If all goes well, you should get the graphical login screen.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_58_0.png)

The X configuration file created by using the -configure option of the X server doesn’t display at the best resolution. To fine-tune the configuration file, you have to run a utility to adjust the display settings after you reboot the system. Which utility you use depends on the Linux distribution, but most distributions include a utility that enables you to configure the video card, monitor, and display settings through a GUI.

## Resolving Other Installation Problems

I’m sure that I haven’t exhausted all the installation problems lurking out there. No one can. So many components in Intel x86 PCs exist that Murphy’s Law practically requires there to be some combination of hardware that the installation program can’t handle. In this section, I list a few known problems. For other problems, I advise you to go to Google Groups (https://groups.google.com) and type some of the symptoms of the trouble. Assuming that others are running into similar problems, you can get some indication of how to troubleshoot your way out of your particular predicament.

## Using Knoppix boot commands

The Knoppix Live CD can be a great troubleshooting tool because Knoppix is good at detecting hardware and can be run directly from the boot medium (CD/DVD/USB).

![](img/322157d1fa7d965f05bcd68ed0ffc36b_59_0.png)

If you have trouble starting Knoppix, try entering Knoppix boot commands at the `boot:` prompt. If Knoppix seems to hang when trying to detect a SCSI card, for example, you can disable SCSI probing by typing `knoppix noscsi` at the `boot:` prompt. Or, if you want the X server to load the *nv* module (for graphics cards based on the NVIDIA chipset), you can type `knoppix xmodule=nv` at the `boot:` prompt.

Table 3-2 lists some commonly used Knoppix boot commands.

### Table 3-2 Some Common Knoppix Boot Commands

| Boot Command | What It Does |
|---|---|
| expert | Starts in *expert mode*, which enables the user to interactively set up and configure Knoppix. |
| failsafe | Boots without attempting to detect hardware (except for the bare minimum needed to start Linux). |
| fb1280x1024 | Uses fixed framebuffer graphics at the specified resolution. (Specify the resolution you want, such as 1024 x 768 or 800 x 600.) |
| knoppix 1 | Starts Knoppix in run level 1 (single-user mode), which you can use to perform rescue operations. |
| knoppix 2 | Starts at run level 2, which provides a text-mode shell prompt only. |
| knoppix acpi=off | Disables ACPI (Advanced Configuration and Power Interface). |
| knoppix atapicd | Uses the ATAPI CD-ROM interface instead of emulating a SCSI interface for IDE CD-ROM drives. |
| knoppix desktop=wmname | Uses the specified Window Manager instead of the default KDE desktop= *wmname* (where *wmname* is fluxbox, icewm, kde, larswm, twm, wmaker, or xfce). |
| knoppix dma | Enables direct memory access (DMA) for all IDE drives. |
| knoppix floppyconfig | Runs the shell script named knoppix.sh from a floppy. (The shell script contains Linux commands that you want to run.) |
| knoppix fromhd=/dev/hda1 | Boots from a previously copied image of Live CD that's in the specified hard drive partition. |
| knoppix hsync=80 | Uses an 80 kHz horizontal refresh rate for X. (Enter the horizontal refresh rate you want X to use.) |
| knoppix lang=xx | Sets the keyboard language as specified by the two-letter code xx (where xx is cn = Simplified Chinese, de = German, da = Danish, es = Spanish, fr = French, it = Italian, nl = Dutch, pl = Polish, ru = Russian, sk = Slovak, tr = Turkish, tw = Traditional Chinese, or us = U.S. English). |

*(continued)*

### Table 3-2 (continued)

| Boot Command | What It Does |
|---|---|
| knoppix mem=256M | Specifies that the PC has the stated amount of memory (in megabytes). |
| knoppix myconf=/dev/hda1 | Runs the shell script knoppix.sh from the /dev/hda1 partition. (Enter the partition name where you have the knoppix.sh file.) |
| knoppix myconf=scan | Causes Knoppix to search for the file named knoppix.sh, scan, and execute the commands in that file, if it exists. |
| knoppix noeject | Doesn't eject the Live CD after you halt Knoppix. |
| knoppix noprompt | Doesn't prompt you to remove the Live CD after you halt Knoppix. |
| knoppix nowheel | Forces the PS/2 protocol for a PS/2 mouse or touchpad (as opposed to the mouse being detected automatically). |
| knoppix noxxx | Causes Knoppix to skip specific parts of the hardware detection (where xxx identifies the hardware or server that shouldn't be probed: apic = Advanced Programmable Interrupt Controller, agp = Accelerated Graphics Port, apm = Advanced Power Management, audio = sound card, ddc = Display Data Channel, dhcp = Dynamic Host Configuration Protocol, fstab = file system table, firewire = IEEE 1394 high-speed serial bus, pcmcia = PC Card, scsi = Small Computer System Interface, swap = hard drive space used for virtual memory, usb = Universal Serial Bus). |
| knoppix pci=bios | Uses BIOS directly for bad PCI controllers. |
| knoppix pnpbios=off | Skips the plug-and-play (PnP) BIOS initialization. |
| knoppix screen=resolution | Sets the screen resolution in pixels (where resolution is the resolution you want, such as 1024x768, 800x600, 640x480, and so on). |
| knoppix testcd | Checks the data integrity of the Live CD by using the MD5 sum. |
| knoppix tohd=/dev/hda1 | Copies the Live CD to the specified hard drive partition and runs from there (requires 1GB of free space on the partition). A performance boost can be obtained by changing tohd to toram and utilizing RAM. |
| knoppix toram | Copies the Live CD to RAM (memory) and runs from there (requires 1GB of RAM). |
| knoppix vga=ext | Uses a 50-line text mode display. |
| knoppix vsync=60 | Uses a vertical refresh rate of 60 Hz for X. (Enter the vertical refresh rate you want X to use.) |
| knoppix wheelmouse | Enables the IMPS/2 protocol for wheel mice. |
| knoppix xmodule=modname | Causes the X server to load the module specified by modname so that X works on your video card (where modname is ati, fbdev, i810, mga, nv, radeon, savage, svga, or s3). |
| knoppix xserver=progname | Starts the X server specified by progname (where progname is XFree86 or XF86_SVGA). |
