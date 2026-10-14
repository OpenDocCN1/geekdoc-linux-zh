# linuxrc

linuxrc is started during the boot of the kernel, usually as a prelude to a Linux system installation, before the “actual” booting commences (the kernel must first be properly configured, of course). This allows you to boot a small, modularized kernel and to load the few drivers needed as modules from a floppy disk.
If needed, linuxrc assists in loading the related drivers. However, YaST2’s automatic hardware detection is usually quite reliable.
You can also use linuxrc as a boot tool for an already installed system. You can even start a totally independent RAM disk-based rescue system, for example, if something serious should happen to your hard disk or you have simply forgotten your root password. More about this below, in Section *The SuSE Rescue System* on page 285.

# Main Menu

After you have selected the language and keyboard, find yourself in linuxrc’s main menu (see Figure 3.2 on page 34). Normally, linuxrc is used to start Linux. Go to the start menu to start an installation (‘Start installation / system’).

# Settings / Preferences

Specify your settings in respect to ‘Language’, ‘Screen’ (Color/monochrome), ‘Keyboard Layout’, and ‘Debug (Experts)’.

# System Information

In ‘System Information’ (Figure 11.1 on the following page), check a number of other things, besides kernel messages, such as the I/O addresses of PCI cards or the size of the main memory recognized by Linux.
You can check some system information in ‘System information’. Here, check the used interrupts, I/O ports used, main memory, and recognized PCI devices as detected by Linux.
The next lines show how a hard disk and a CD-ROM connected to an (E)IDE controller announce their start. In this case, you do not need to load additional modules:

```
hda: ST32140A, 2015MB w/128kB Cache, LBA, CHS=1023/64/63
hdb: CD-ROM CDU-51G, ATAPI CD-ROM drive
Partition check:
 hda: hda1 hda2 hda3 < hda5 >
```