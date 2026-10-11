
If present, the X Window System uses simultaneous left+right mouse buttons to emulate the middle button (should be used on two button mice).

After options, the mouse type may be specified as one of the following:

```
alpsps/2, ascl, asclips/2, atibm, generic, generic3, genericps/2, generic3ps/2, geniusmm, geniusnmps/2, geniusnpsp2, thinking, thinkingps/2, logitech, logitechnc, logibm, logimann, logimannps/2, logimann+, logimannp5/2, microsoft, mswen, msintelli, msintellips/2, msbm, mousesystems, mmeries, mhhitab, sun, none
```

If the mouse command is given without any arguments, or it is omitted, the installation program will attempt to autodetect the mouse (which works for most modern mice).

## F.5.12 network

**network** (optional)

Configures network information for the system. If it is not given, and the kick-start installation does not require networking (in other words, it’s not installed over NFS), networking is not configured for the system. If the installation does require networking, Anaconda assumes that the install should be done over eth0 via a dynamic IP address (BOOTP/DHCP), and configures the final, installed system to dynamically determine its IP address. The network command configures the networking information for the installation for network kickstarts as well as for the final, installed system.

### --bootproto

One of **dhcp**, **bootp**, or **static** (defaults to DHCP, and **dhcp** and **bootp** are treated the same). Must be **static** for static IP information to be used.

### --ip

IP address for machine to be installed.

### --gateway

Default gateway as an IP address.

### --nameserver

Primary name server, as an IP address.

### --netmask

Netmask for the installed system

There are three different methods of network configuration:

- DHCP
- BOOTP
- static

The DHCP method uses a DHCP server system to obtain its networking configuration. As you might guess, the BOOTP method is similar, requiring a BOOTP server to supply the networking configuration.

The static method requires that you enter all the required networking information in the kickstart file. As the name implies, this information is static, and will be used during the installation, and after the installation as well.

To direct a system to use DHCP to obtain its networking configuration, use the following line:

```
network --bootproto dhcp
```

To direct a machine to use BOOTP to obtain its networking configuration, use the following line in the kickstart file:

```
network --bootproto bootp
```

The line for static networking is more complex, as you must include all network configuration information on one line. You’ll need to specify:

- IP address
- netmask
- gateway IP address
- name server IP address

Here’s an example static line:

```
network --bootproto static \
      --ip 10.0.2.15 \
      --netmask 255.255.255.0 \
      --gateway 10.0.2.254 \
      --nameserver 10.0.2.1
```

> **Note**
> The entire network configuration *must* appear on one line! We’ve wrapped it here to make it easier to read.

There are two restrictions you must keep in mind should you use the static method:

- All static networking configuration information must be specified on *one* line; you cannot wrap lines using a backslash, for example.
- You can only specify one name server here. However, you can use the kickstart file’s `$post` section (described in Section F.5.23, *$post -- Post-Installation Configuration Section*) to add more name servers, if needed.

## F.5.13 partition

**part** (required for installs, ignored for upgrades)

Create a partition on the system. Partition requests are of the form:

```
part <mntpoint> --size <size> [--grow] [--onpart <partco>] [--ondisk <diskname>]
```

The `<mntpoint>` is where the partition will be mounted, and must be of one of the following forms:

`/\<mntpoint\>`
(i.e. `/`, `/usr`, `/home`)

**swap**
The partition will be used as swap space.

`raid.\<id\>`
The partition will be used for software RAID (see the `raid` command later).

`--size \<size\>`
Sets the minimum size for the partition

`--grow`
Tells the partition to grow to fill available space (if any).

`--onpart \<part\>`
Tells the installation program to put the partition on the *already existing* device `<part>`. For example, `partition /home --onpart hda1` will put `/home` on `/dev/hda1`, which must already exist.

`--ondisk \<disk\>`
Forces the partition to be created on a particular disk. For example, `--ondisk sdb` will put the partition on the second disk on the system.

All partitions created will be formatted as part of the installation process.

## F.5.14 raid

**raid** (optional)

Assembles a software RAID device. This command is of the form:

```
raid <mntpoint> --level <level> --device <mdddevice> <partitions*>
```

The `<mntpoint>` is the location to mount the RAID filesystem. If it is `/`, the RAID level must be 1 unless a boot partition (`/boot`) is present in which case the `/boot` partition has to be level 1 and the root (`/`) partition can be any of the available types. The `<partitions*>` (which denotes that multiple partitions can be listed) lists the RAID identifiers to add to the RAID array.

### --level \<level\>

RAID level to use (0, 1, or 5).

### --device \<mdddevice\>

Name of the RAID device to use (such as md0 or md1). RAID devices range from md0 to md7, and each may only be used once.

Here’s an example of how to create a RAID level 1 partition for `/`, and a RAID level 5 for `/usr`, assuming there are three SCSI disks on the system. It also creates three swap partitions, one on each drive.

```
part raid.01 --size 60 --ondisk sda
part raid.02 --size 60 --ondisk sdb
part raid.03 --size 60 --ondisk sdc

part swap --size 128 --ondisk sda
part swap --size 128 --ondisk sdb
part swap --size 128 --ondisk sdc

part raid.11 --size 1 --grow --ondisk sda
part raid.12 --size 1 --grow --ondisk sdb
part raid.13 --size 1 --grow --ondisk sdc

raid / --level 1 --device md0 raid.01 raid.02 raid.03
raid /usr --level 5 --device md1 raid.11 raid.12 raid.13
```

## F.5.15 reboot

**reboot** (optional)

Reboot after the installation is complete (no arguments). Normally, kickstart displays a message and waits for the user to press a key before rebooting.

## F.5.16 rootpw

**rootpw** (required)

usage: `rootpw [--iscrypted] <password>`

Set the system’s root password to the `<password>` argument.

### --iscrypted

If this is present, the password argument is assumed to already be encrypted.

## F.5.17 skipx

**skipx** (optional)

If present, X is not configured on the installed system.

## F.5.18 timezone

**timezone** (required)

`timezone [--utc] <timezone>`

Sets the system time zone to `<timezone>` which may be any of the time zones listed in "timeconfig".

### --utc

If present, the system assumes the hardware clock is set to UTC (Greenwich Mean) time.

## F.5.19 upgrade

**upgrade** (optional)

Tells the system to upgrade an existing system rather than install a fresh system.

## F.5.20 xconfig

**xconfig** (optional)

Configures the X Window System. If this option is not given, the user will need to configure X manually during the installation, if X was installed; this option should not be used if X is not installed on the final system.

### --noprobe

Don’t probe the monitor.

### --card *\<card\>*

Use card *\<card\>*; this card name should be from the list of cards in Xconfigurator. If this argument is not provided, Anaconda will probe the PCI bus for the card.

### --monitor *\<mon\>*

Use monitor *\<mon\>*; this monitor name should be from the list of monitors in Xconfigurator. This is ignored if **--hsync** or **--vsync** is provided; if no monitor information is provided, the monitor is probed via plug-and-play.

### --hsync *\<sync\>*

Specifies the horizontal sync frequency of the monitor.

### --vsync *\<sync\>*

Specifies the vertical sync frequency of the monitor.

### --startxonboot

Use a graphical login (runlevel 5) for the installed system.

## F.5.21 zerombr – Partition table initialization

**zerombr** (optional)
