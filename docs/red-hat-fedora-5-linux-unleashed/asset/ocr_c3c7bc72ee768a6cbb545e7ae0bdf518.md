# NOTE

If you have trouble configuring and using a PCMCIA card, browse to the Linux PCMCIA home page at http://kernel.org/pub/linux/utils/kernel/pcmcia/pcmcia.html/. Click the known problems link to see whether other users with the same card are having problems, or if the card is not fully supported. If a new version of the PCMCIA kernel drivers is available and changes have been made to your card's drivers (or if a new driver has been developed), download and install the newer software. See Chapter 39 for information on installing the new PCMCIA modules, or follow the directions included with the PCMCIA software.

# Controlling PCMCIA Service

Although PCMCIA cards can be inserted or removed while using Fedora, be careful when using these cards. For example, do not remove a network card while connected to a remote computer. Do not pull a compact flash card or other storage media card (such as an IBM microdrive) while the card's filesystem is mounted and in use—you could corrupt the media's filesystem and experience loss of data.

You can control a PCMCIA device from the command line, and insert and remove the card without physically removing and then inserting the card. Use the cardctl command to control PCMCIA service to one or more card slots on your notebook or desktop PC with a PCMCIA adapter. The cardctl command is used to get and print information about an inserted card, suspend or resume power to a card, reset a card, perform a software insertion or removal, or configure a card according to a particular, predefined scheme (such as using a network in the office or at home). The format of the command is cardctl command slot_number (such as 0 or 1).

For example, if you have inserted a compact flash card, eject the card (after unmounting its filesystem) using the cardctl command and its eject option, along with the card's slot number like this:

```
# cardctl eject 0
```

This can save power when running a notebook. When the card is needed again, you can subsequently “insert” the card like so:

```
# cardctl insert 0
```

# Configuring and Using CD, DVD, and CD-RW Drives

Linux provides support for using a variety of CD and DVD devices and media. This section shows how to determine what device has been assigned to your CD drive and how to get additional drive information if the drive supports recording on optical media.

AT Attachment Packet Interface, or ATAPI, IDE-based CD drives, are recognized during installation and work through the ide-cd kernel module. A symbolic link named /dev/cdrom will be created and will point to your CD's device (perhaps /dev/hdb or