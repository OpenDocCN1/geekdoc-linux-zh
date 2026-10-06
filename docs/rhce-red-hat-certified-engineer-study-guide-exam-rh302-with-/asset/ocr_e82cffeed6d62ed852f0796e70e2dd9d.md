# Linux Support for Systems 21

The RHCE exam covers the administration of Red Hat Linux for only Intel architecture PCs, so this chapter describes only that architecture. Note that many companies other than Intel Corporation manufacture hardware is compatible with the Intel architecture.

For more information on non-Intel architectures, see the Red Hat Hardware Compatibility List at www.redhat.com/support/hardware.

# Hardware Compatibility

There are two main sources of information on hardware that is compatible with Linux. This section describes these sources.

# The Linux Hardware Compatibility HOWTO

The Linux Documentation Project (www.linuxdoc.org) intends to "create the canonical set of free Linux documentation." Toward that end, they publish a useful series of HOWTOs, guides, and pages. One of the most important and useful documents is the Linux Hardware Compatibility HOWTO. This HOWTO identifies hardware devices and components that are compatible with Linux and gives hints and tips for choosing compatible hardware and getting to it.

Beginning with the Red Hat Linux 6.2 distribution, the HOWTOs are available in over one dozen languages and several formats, including text, HTML, and PDF. You'll find the HOWTOs on the documentation CD-ROM, rather than on the installation CD-ROM—and enough—you should probably copy them to the /usr/doc/HOWTO directory of your system's hard disk. To do so, mount the CD-ROM and issue the following commands:

```
# mkdir /usr/doc/HOWTO
# cd /mnt/cdrom/HOWTOS
# cp -R *-HOWTO *.html /usr/doc/HOWTO
```

If the /usr/doc/HOWTO exists, the mkdir command will fail; not be concerned. If you mount the CD-ROM at a mount point other than /mnt/cdrom, you should revise the command appropriately. You'll find non-English HOWTOs in the HOWTO/translations directory and HTML and PDF HOWTOs in the HOWTO/other-formats directory.

Copyright©2000 SYTEX, Inc., Alameda, CA www.sysex.com