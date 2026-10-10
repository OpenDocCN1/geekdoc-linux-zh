# # Local Printing from Caldera

In this chapter we will explore the options available to print within Caldera. Many print functions are available, and we need to cover a multitude of programs and supporting files. Caldera gives you the option to print from your local machine, from another machine that is connected to a local area network, or even to a printer remotely situated (if it can be addressed over either a WAN or the Internet). All that is required is permission to use the printer, which you supply to yourself for a locally attached printer.

If you have permission to use the printer, the rest is easy. It is, however, just a bit detailed. We will cover the simple case—printing locally to a parallel printer—as well as the complicated case—printing remotely over the Internet to a PostScript printer running off a serial port that is behind a firewall.

Caldera has many utilities that make installing a printer a snap. If you are using a local parallel printer, you should be up and running in about 10 minutes. But just to verify that the hardware works, it is always a good idea to boot from a DOS floppy and attempt to print a file on the printer before getting involved with setting up a Linux printer. Many times I have spent an hour trying to get a printer to work under Linux only to discover that there was a hardware problem or a setup issue that prevented the printer from ever working. This simple DOS test first would have saved all the frustration.

# ## How Does Caldera Locate My Printer?

Caldera, like all other flavors of UNIX, “talks” to all hardware devices through special device files. These device files are merely entries in Linux’s file structure that are handled by a “device driver” located in the kernel. If you were to do a listing of the printer device special files on the default install of Caldera, you would see something similar to the following:

```
<command used is #ls -1 /dev/lp*>

crw-rw----    1 root            lp        0,  0 Apr  3 16:47 /dev/lp0  (Printer at address 0x38C)
crw-rw----    1 root            lp        0,  1 Apr  3 16:47 /dev/lp1  (Printer at address 0x378)
crw-rw----    1 root            lp        0,  2 Apr  3 16:47 /dev/lp2  (Printer at address 0x278)
```

It is important for you to know that the c in the first column of the device entries stands for character special device, which tells the operating system not to write data to the file system on the disk, but rather to give any data destined for this printer to the driver in