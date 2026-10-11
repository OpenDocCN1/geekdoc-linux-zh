
- If **DHCP** is specified and the "**bootfile**" begins with something other than a /, that file is looked for in the /kickstart directory on the NFS server.
- If **DHCP** did not specify a "**bootfile**," then the installation program tries to read the file /kickstart/1.2.3.4-kickstart, where 1.2.3.4 is the numeric IP address of the machine being installed.

## F.4 The Kickstart File

Now that you have some background information on kickstart installations, let's take a look at the kickstart file itself. The kickstart file is a simple text file, containing a list of items, each identified by a keyword. You can create it by editing a copy of the sample.ks file found in the /doc directory of the Red Hat Linux CD-ROM, or you can create it from scratch. You should be able to edit it with any text editor or word processor that can save files as ASCII text.

First, some ground rules to keep in mind while creating your kickstart file:

- Items must be specified in order. It is not a good idea to try to change the order of the required items.
- Items that aren't required can be omitted.
- Omitting any required item will result in the installation program prompting the user for an answer to the related item, just as during a typical installation. Once the answer is given the installation will continue unattended (unless it comes across another missing item).
- Lines starting with a pound sign ("#") are treated as comments, and are ignored.
- For kickstart upgrades, the following items are required:
  - language
  - installation method
  - device specification (if device is needed to perform installation)
  - keyboard setup
  - the upgrade keyword
  - LILO configuration

If any other items are specified for an upgrade, those items will be ignored (note that this includes package selection).

Kickstart files are split into three sections: commands, package list, and scripts. The file must be of the form:

- <kickstart commands>
- %packages
- <package list>
- %post
- <post script>

The order matters; it can’t be random. The post section goes to the end of the file and ends the file, no marker is necessary to end the file other than the post section itself.

## F.5 Kickstart Commands

The following commands can be placed in a kickstart file.

### F.5.1 auth – Authentication Options

**auth** (required)

Sets up the authentication options for the system. It’s similar to the authconfig command that can be run after the install. By default, passwords are normally encrypted and are not shadowed.

- `--enablemd5`
  Use md5 encryption for user passwords.
- `--enablenis`
  Turns on NIS support. By default, --enablenis uses whatever domain it finds on the network. A domain should almost always be set by hand (via --nisdomain).
- `--nisdomain`
  NIS domain name to use for NIS services.
- `--nisserver`
  Server to use for NIS services (broadcasts by default).
- `--useshadow`
  Use shadow passwords.

### F.5.2 clearpart – Removing partitions based on partition type

**clearpart** (optional)

Removes partitions from the system, prior to creation of new partitions. By default, no partitions are removed.

- `--linux`
  Erases Linux (type 0x82, 0x83, and 0xfd [RAID]) partitions
- `--all`
  Erases all partitions from the system.

### F.5.3 device --opts

**device** (optional)

On most PCI systems, the installation program will autoprobe for Ethernet and SCSI cards properly. On older systems, and some PCI systems, kickstart needs a hint to find the proper devices, however. The device command tells Anaconda to install extra modules. It is of the form:

```
device <type> <moduleName> --opts <options>
```

`<type>` should be one of "scsi" or "eth", and `<moduleName>` is the name of the kernel module which should be installed.

**--opts**
Options to pass to the kernel module. Note that multiple options may be passed if put in quotes. For example:
`--opts "aic152x=0x340 io=1"`

### F.5.4 driver disk

**driverdisk** (optional)

During kickstart, driver disks can be used by copying the contents of a driver disk to the root directory of a partition on the system's hard drive and using the `driverdisk` command to tell the installation program where to look for it.
`driverdisk <partition> [--type <fstype>]`
`<partition>` is the partition containing the driver disk.

**--type**
Filesystem type (for example, VFAT or ext2).

### F.5.5 install

**install** (optional)

Tells the system to install a fresh system rather than upgrade an existing system. This is the default mode.

### F.5.6 Installation methods

You must use one of these three commands to specify what type of kickstart is being done:

**NFS**
Install from the NFS server specified.

- `--server <server>`
  Server from which to install (hostname or IP).
- `--dir <dir>`
  Directory containing the Red Hat installation tree.

For example:
`nfs --server <server> --dir <dir>`

**CD-ROM**
Install from the first CD-ROM drive on the system.
For example:
`cdrom`

**hard drive**
Install from a Red Hat installation tree on a local drive, which must be either VFAT or ext2.

- `--partition <partition>`
  Partition to install from (such as, sdb2).
- `--dir <dir>`
  Directory containing the Red Hat installation tree.

For example:
`harddrive --partition <partition> --dir <dir>`

### F.5.7 keyboard

**keyboard** (required)

Sets system keyboard type. Here’s the list of available keyboards on i386 and Alpha machines:

```
azerty, be-latin1, be2-latin1, fr-latin0, fr-latin1, fr-pc, fr, 
wangeb, ANSI-dvorak, dvorak-l, dvorak-r, dvorak, pc-dvorak-latin1, 
tr_f-latin5, trf, bg, cf, cz-lat2-prog, cz-lat2, defkeymap, 
defkeymap_V1.0, dk-latin1, dk. emacs, emacs2, es, fi-latin1, fi, 
gr-pc, gr, hebrew, hu10l, is-latin1, it-ibm, it, it2, jp106, 
la-latin1, lt, lt-l4, nl, no-latin1, no, pc10, pl, pt-latin1, 
pt-old, ro, ru-cpl251, ru-ms, ru-yaverty, ru, ru1, ru2, ru-win, 
se-latin1, sk-prog-qwerty, sk-prog, sk-qwerty, tr_q-latin5, tralt, 
trf, trq, ua, uk, us, croat, cz-us-qwertz, de-latin1-nodedeadkeys, 
de-latin1, de, fr_CH-latin1, fr_CH, hu, sg-latin1-lk450, 
sg-latin1, sg, sk-prog-qwertz, sk-qwertz, slovene
```

Here’s the list for SPARC machines:

```
sun-pl-altgraph, sun-pl, sundvorak, sunkeymap, sunt4-es, 
sunt4-no-latin1, sunt5-cz-us, sunt5-de-latin1, sunt5-es, 
sunt5-fi-latin1, sunt5-fr-latin1, sunt5-ru, sunt5-uk, sunt5-us-cz
```

### F.5.8 language

**lang** (required)

Sets the default language for the installed system. The language you specify will be used during the installation as well as to configure any language-specific aspect of the installed system. For example, to set the language to English, the kickstart file should contain the following line:

```
lang en_US
```

Valid language codes are:

```
cs_CZ, en_US, fr_FR, de_DE, hu_HU, is_IS, id_ID, it_IT, 
ja_JP, ujis, no_NO, pl_PL, ro_RO, sk_SK, sl_SI, es_MX, 
ru_RU, KOI8-R, uk_UA
```

### F.5.9 lilo

**lilo** (required)

Specifies how the boot loader should be installed on the system. By default, LILO installs on the MBR of the first disk, and installs a dual-boot system if a DOS partition is found (the DOS/Windows system will boot if the user types **dos** at the **LILO:** prompt).

- **--append** *<params>*
  Specifies kernel parameters.
- **--linear**
  Use the `linear` LILO option; this is only for backwards compatibility (and `linear` is now used by default).
- **--location**
  Specifies where the LILO boot record is written. Valid values are **mbr** (default), **partition** (installs the boot loader on the first sector of the partition containing the kernel), or **none**, which prevents any bootloader from being installed.

### F.5.10 lilockcheck

**lilockcheck** (optional)

If this is present, the installation program checks for LILO on the MBR of the first hard drive, and reboots the system if it is found -- No installation is done in this case. This can prevent the kickstart from reinstalling an already installed system.

### F.5.11 mouse

**mouse** (required)

Configures the mouse for the system, both in GUI and text modes. Options are:

- **--device** *<dev>*
  Device the mouse is on (such as --device ttyS0)
- **--emulthree**
