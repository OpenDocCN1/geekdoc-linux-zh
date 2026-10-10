
Enter options as they appear in the following table, filling in specific values for the variables.

## The GRUB Boot Manager: Global Settings

| Option | Setting |
| --- | --- |
| color MENU_FOREGROUND / MENU_BACKGROUND SELECTED_FOREGROUND / SELECTED_BACKGROUND | Sets the colors that menu items and selected menu items display in.<br><br>The available colors are: black, blue, green, cyan, red, magenta, brown, and light gray.<br><br>The foregrounds can also use dark-gray, light-blue, light-green, light-cyan, light-red, light-magenta, yellow and white.<br><br>You can also add blink to make the foreground flash. |
| default NUMBER | Sets the default operating system.<br><br>0 is the operating system defined in the first stanza after the global one. If the default option is not used, then this stanza is automatically the default. |
| fallback NUMBER | Sets the second default operating system.<br><br>The fallback starts only if the default cannot. There is no default fallback. |
| timeout SECONDS | Sets the time before the default operating system starts. |

## Basic Settings for Linux Entries in the GRUB Boot Manager

| Setting | Comments |
| :--- | :--- |
| initrd PARTITION /boot/initrd.img | A symbolic link to the initrd file used by Linux. |
| title NAME | The name that appears in the GRUB menu. The distribution and version number is usually a good choice. |
| root=PARTITION | The Linux root partition, named using Linux's naming conventions.<br><br>Do not confuse with GRUB's root partition or use GRUB's naming convention. |
| kernel PARTITION KERNEL | Use GRUB's naming convention for the partition.<br><br>Usually, the kernel is `/boot/vmlinuz`. |

## Basic Settings for a Windows OS in the GRUB Boot Manager

| Setting | Comments |
|---|---|
| title NAME | The name that appears in the GRUB menu. The operating system and version number is usually a good choice. |
| root PARTITION | The partition that the operating system is on. |
| makeactive | Makes the partition bootable. The partition must be a primary one. |
| chainloader +1 | Needed to use Windows's own loader together with GRUB. GRUB displaces the Windows loader one sector from the start of the hard drive. |

## Basic Settings for a Floppy Drive in the GRUB Boot Manager

| Setting | Comments |
| :---- | :---- |
| title NAME | The name that appears in the GRUB menu. |
| root fd0 | The device that the operating system is on: generally, the first floppy drive. Use fd1 for the second floppy drive. |
| chainloader +1 | Needed to use a non-GRUB loader. The +1 looks for the loader one sector from the start of the hard drive. GRUB itself appears in the first sector of the hard drive. |

## Loading an Operating System Not on the First Hard Drive

GRUB generally reads from the first hard drive. For this reason, you sometimes need to temporarily remap additional hard drives to the first hard drive.

Add the following lines to each stanza that refers to an operating system on another hard drive:

```text
map (hd0) OTHER_HARD_DRIVE
map OTHER_HARD_DRIVE (hd0)
```

Place these lines before the `root` or `chainloader +1` options.

## Making a Bootable Recovery Disk

A boot disk is a basic recovery tool. To create a boot disk:

- Copy the boot image on the CD. This image is called `install-1.44`, and is in a directory below `/dists/progony/main/dskss-i386/` on the CD. Mount a floppy disk, then type: `dd if=PATH of=/dev/fd0 bs=1474560`.
- A floppy to use with a GRUB entry:
  1. Mount the floppy.
  2. Copy the kernel image to a floppy. Type: `dd if=/boot/vmlinuz-2.2.18 of=/dev/fd0 bs=8192`.
  3. Make an entry for the floppy in `/boot/grub/menu.lst`. See “Basic Settings for a Floppy Drive in the GRUB Boot Manager,” page 380.
- The utilities in the `/tools` directory of the CD to create a boot disk under Windows or DOS using `rawwrite1` or `rawwrite2`.

## Configuring Networks

In Linux terms, the subject of networking includes not only a network of individual machines, but also internet connections.

This section covers the basics of Linux networking in Progeny Debian, starting with the hardware and how to configure a connection, and ending with how to configure e-mail:

- Configuring an ethernet card.
- Checking a modem connection.
- Configuring a Network connection.
- Configuring a Dialup connection.
- Setting up electronic mail.

### Configuring an Ethernet Card

![](img/e36b94f8548b09d00212238f073b11d9_383_0.png)

1. At a command line, type: **dpkg-reconfigure etherconf**. The Ethernet Networking Configuration screen opens.
   - If your card is detected, the first screen notes the fact. If it is not, see “Troubleshooting With a Network Card,” page 383.
2. Follow the instructions on each screen. You may need to know:
   - Whether the network card is removable.
   - Whether the card can be configured with DHCP.
   - Your computer’s IP Address.
   - The network’s netmask.
   - The gateway.
   - The hostname.
   - The domain name.
   - The name server.
   
   If you do not know this information, consult your system administrator or Internet Provider.
3. When you are finished configuring, select **Exit**. Etherconf then attempts to connect to the network.
   - Watch the command line for messages about this effort. If the connection is unsuccessful after several minutes, press **Ctrl-Z**, then **Ctrl-C** to stop the effort. Then check the network card.

### Troubleshooting With a Network Card

Progeny Debian should detect most network cards automatically. However, if you are having trouble establishing a connection:

- Check that the card is properly installed.
- Check that your ethernet card or other network interface card is supported by Linux.
- Check that your network card is working. Type: `ifconfig -a`. A list of active interfaces displays. Your network card is probably `/dev/eth0`.
- Check that your network card is active. Type: `ifconfig DEVICE up`. The card is probably `/dev/eth0`.

### Checking a Modem Connection

Modems are useful for dialup connections to the internet, or for receiving faxes on your system.

Modems are probably the most difficult piece of hardware to work with under Linux. The problem is that many modems today, especially internal ones, are winmodems. That is, most of them require a running copy of Windows to work. While a few winmodems have Linux drivers available, these drivers are usually written for a specific kernel, and may not work if you upgrade the kernel.

An external modem or a PCMCIA card should generally work. However, research brands on the internet to see if they are Linux compatible before you buy.

To check that Linux recognizes your modem, type `dpkg-reconfigure pppconf` at the command line. `pppconf` is a tool for setting up a dialup connection. It starts by detecting the modem, then going on to configure a dialup connection.

If your modem does not respond:

- Check that it is not a winmodem.
- Check that it is properly connected to your system and to a live phone jack.
- To ensure that your system can find the modem, create a symbolic link between the serial port and the `/dev/modem` device. Type: `ln -sf /dev/port /dev/modem`.

### Setting up a Fax Modem

Progeny Debian does not automatically configure a fax modem for you. However, you can use the Debian package `hylafax-server` to receive faxes via a fax-modem. If you are a desktop user, then you might also install `tkhylafax` so that you have a graphical interface. Other fax packages are also available.

**Note**

Check that your modem is usable under Linux. See “Configuring a Sound Card,” page 359.

### Configuring a Network Connection

A Dynamic Host Configuration Protocol (DHCP) connection is the most common network connection today. In addition, a DHCP connection is also used for an ADSL or cable internet connection.

Nowadays, the connection is generally through an ethernet card. However, another type of network interface card may also be used.

#### Preparing to Configure a Network Connection

Before you start to configure the network, you need to know:

- The type of card you use to connect to the internet. On most modern computers, the card should be an ethernet card. If you are on a laptop, you are probably using an ethernet interface with a PCMCIA card. Consult the documentation that comes with the card.

Consult your system administrator or internet provider for:

- Your user account.
- Your domain name.
- Your computer's IP address and hostname.
- The IP address of your network.
