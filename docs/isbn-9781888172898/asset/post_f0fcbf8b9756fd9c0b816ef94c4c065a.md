
## Disk Partitions and MS-DOS

Most MS-DOS systems, as they come from the vendor, have one hard disk which contains one large partition. In order to install Red Hat Linux, you need to make that partition smaller, and then create a partition for Red Hat Linux in the space that's left. There are two ways to accomplish this:

- **Destructive Repartitioning** This procedure destroys any data in the disk partition(s) you are resizing; you should make a complete, reliable backup of everything you wish to keep from the disk you are repartitioning. Then, use the MS-DOS disk partitioning utility, called `fdisk`, to delete the large partition and create a smaller MS-DOS partition. Restore your data to the new partition from your backup.

- **Non-Destructive Repartitioning** This procedure is not supposed to destroy data in the disk partition(s) you are resizing; however, we recommend making reliable backups of data you wish to keep in any case. You can use the `fips` utility, included on the Red Hat Linux CD in the `dosutils` directory, to resize your MS-DOS partition; we highly recommend reading the `fips` documentation, located the `fipsdoccs` subdirectory, before doing so.

After repartitioning, you can use the Red Hat Linux installation system to create partitions for your Red Hat Linux system as described in *Step-By-Step Installation*.

## Disk Partitions and Other Operating Systems

Information on creating disk partitions to be compatible with other operating systems is available in several HOWTOs and Mini-HOWTOs, available on the Red Hat Linux CD in the `doc/HOWTO` and `doc/HOWTO/mini` directories.

## How Many Partitions?

If you wish to you, you can install Red Hat Linux in a single large partition. However, we recommend the following (**Please Note:** If you plan to install all the software packages accompanying Red Hat Linux, you may need to use even larger partitions):

- A **swap partition** for virtual memory. If your computer has 16 MB of memory or less, you must create a *swap partition*; even if you have more memory, a swap partition is recommended. The size of your swap partition should be at least 16 MB or the same as the amount of memory in your computer, whichever is larger.

- A **root partition** to be mounted as `/` (the root directory) when your Red Hat Linux system boots; it only needs to contain things necessary to boot your system, as well as system configuration files. 50–80 MB works well for most systems.

- A **/usr partition**, where much of the software on a Red Hat Linux system lives; this partition should be 200–500 MB, depending on how many packages you plan to install.

- A **/home partition**, where users’ *home directories* go; the size of /home depends mostly on how many users you plan to have on your Red Hat Linux system and what they might store in their home directories.

Additionally, you may wish to create any of the following:

- A **/tmp partition** for temporary files. This is a good idea for larger, multiuser systems or network server machines.

- A **/usr/src partition** if you wish to install a large amount of the source code included with Red Hat Linux.

- A **/usr/local partition** to hold things you wish to keep separate from the rest of your Red Hat Linux system, such as software that is not available as an RPM package.

### 2.3 Preparing to Install

#### 2.3.1 Creating the Boot and Supplemental Floppies

Your Red Hat Linux/Intel CD set may include a boot diskette and supplemental diskette. If so, you may skip to Section 2.3.2. If not, you must create them.

You need only a boot diskette if you are installing Red Hat Linux from CD-ROM or via NFS. You also need a supplemental diskette if you are installing from a hard disk, via FTP, or from a PCMCIA device.

To create the boot and supplemental floppies, you need two blank, formatted, high-density (1.44 MB), 3.5-inch diskettes. The diskette images are located in the images directory on the Red Hat Linux CD or the FTP site where you got Red Hat Linux. Each image is a *snapshot* of the appropriate floppy diskette, which you need to transfer onto an actual floppy; you can do this using either MS-DOS or Linux.

##### Making Floppies Under MS-DOS

To make floppies under MS-DOS, use the rawrite utility included on the Red Hat Linux CD in the dosutils directory. First, label a formatted 3.5-inch floppy “Boot Diskette” or something similar and insert it into the floppy drive. Then, use the following commands (assuming your CD is drive d:):

```
d: \
    cd \images \
    \dosutils\rawrite.exe
```

rawrite first asks you for the filename of a diskette image; enter boot.img. Then it asks you for a diskette drive to write the image to; enter a:. If you need to make a supplemental floppy, label a second diskette and then run rawrite again, using supp.img.

##### Making Floppies Under Linux

To make floppies under Linux, you must have permission to write to /dev/fd0 (the 3.5-inch floppy drive). Label a blank, formatted diskette “Boot Diskette” or something similar and insert it into the floppy drive (but don’t mount it). After mounting the Red Hat Linux CD, change to the images directory and use the following command:

```
dd if=boot.img of=/dev/fd0 bs=1440k
```

If you need to make a supplemental floppy, label a second diskette, insert it in the floppy drive, and then use the following command:

```
dd if=supp.img of=/dev/fd0 bs=1440k
```

#### Installing Without Using a Boot Floppy

Alternatively, if you have MS-DOS installed on your computer, you can boot the installation system directly from the CD without making floppies. To do this, use the following commands (assuming your CD is drive d:):

```
d:
 cd \dosutils
 autoboot.bat
```

#### 2.3.2 A Note About Virtual Consoles

The Red Hat Linux installation system is more than simply the dialog boxes it presents as it guides you through the installation procedure. In fact, the installation system presents several different kinds of diagnostic messages while running, and it gives you a means to enter commands from a shell prompt. It presents the installation dialogs, shell prompt, and messages on five *virtual consoles* which you can switch between using a single keystroke. These virtual consoles can be very helpful if you encounter a problem while installing Red Hat Linux; messages displayed on the install log or system log can help to pinpoint the problem. Please see Figure 2.1 for a listing of the virtual consoles, the keystrokes to switch to them, and their contents.

| Console | Keystroke | Contents |
| :---- | :---- | :---- |
| 1 | Alt-F1 | installation dialog |
| 2 | Alt-F2 | shell prompt |
| 3 | Alt-F3 | install log (messages from install program) |
| 4 | Alt-F4 | system log (messages from kernel, etc.) |
| 5 | Alt-F5 | other messages |

Figure 2.1: Virtual Console Information

#### 2.3.3 Using the Dialog Boxes

You can navigate around the installation dialogs using a simple set of keystrokes. In most dialog boxes there is a *cursor or highlight* which you can move using the arrow keys ([⬅][➡][⬆][⬇], `Tab`), and `Alt`+`Tab`. A summary of movement commands is presented at the bottom of each screen.

To “press” a button (such as `OK`), `Tab` to the button and press `Space`. To select an item from a list of items, move the highlight to the item you wish to select and press `Enter`. To select any number of items from a *checklist*, move the highlight to the item you wish to select and press `Space` to select an item. To deselect an item, press `Space` a second time.

Pressing `F12` accepts the current values and proceeds to the next dialog; it is usually equivalent to pressing the `OK` button.

**Please Note:** Do not press random keys during the installation process; it may result in unpredictable behavior.

## 2.4 Step-By-Step Installation

### 2.4.1 Starting the Installation System

#### Booting

To begin installing Red Hat Linux, insert the boot floppy you just created into the floppy drive and reboot the machine (if you have MS-DOS installed on your machine, you can start installing directly from the CD-ROM; see Section 2.3.1 above). The *boot:* prompt appears; press `Enter` to boot. Watch the boot messages to see whether the Linux kernel detects your hardware. If it does not properly detect your hardware, you may need to reboot and enter some options at the *boot:* prompt, e.g.:

```
boot: linux hdc=cdrom
```

Press `Enter` to boot using those options. If you do need to specify some boot options, please make note of them; they will be needed later.
