Any UNIX operating system, including Slackware Linux, recognizes your drives as device files. This means you can write to such a file, execute it, and read it, just as you would any other file in UNIX.

![](bbox=[0.16, 0.19, 0.25, 0.27])

To get the most drive support, be sure to recompile the kernel with the appropriate options.

# SCSI Versus IDE

Here we go—wading into the "religious" debate about hardware—though not too far. I can say my system runs just fine on IDE; you can do a great deal more with SCSI, partly because SCSI drives enable you to daisy-chain up to eight drives. SCSI performance is noticeably better than that of IDE, and many types of media are available for SCSI but not for IDE—including optical drives, lomega Jaz drives, and some higher-performance CD-Rs and CD-RWs.

That said, both types of hardware have advantages and disadvantages. IDE is usually easy to configure, well supported, and cheap. SCSI is fast, usually difficult to configure, and generally works extremely well. IDE supports about four devices at a time; SCSI supports six to eight. Although some more advantageous hardware is available on SCSI, generally you can get along just fine with IDE.

![](bbox=[0.16, 0.59, 0.25, 0.67])

Because many computers come with an IDE drive as standard equipment, I take an IDE-oriented approach to this chapter.

# Drive Locations

On any variety of UNIX, including Slackware Linux, your hardware is recognized as a collection of files. Most of these files are listed in the /dev directory. This section covers a sampling of what you may find.

# ADVANCED POWER-MANAGEMENT BIOS

The following shows the advanced power-management BIOS. It's a great feature for laptops, as it suspends the CPU if idle and shuts down the power after running the shutdown command.

```
crw-r--r-- 1 root root 10, 134 Jun 7 1996 apm_bios
```