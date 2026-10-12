
called Mtools lets you work with DOS files and directories from within Linux. A DOS emulator called dosemu lets you run DOS applications from within a DOS environment that is actually running within Linux (much the way a DOS window runs within a Windows operating system).

## Using mtools

Mtools are mostly DOS commands that have the letter m in front of them and that run in Linux (though there are a few exceptions that are named differently). Using these commands, you can easily work with DOS files and file systems. Table 5-5 lists mtools that are available with Linux (if you have the mtools package installed):

### Table 5-5: Mtools Available with Linux

| Command | Function |
| :--- | :--- |
| mattr | The DOS attrib command, which is used to change an MS-DOS file attribute flag. |
| mbadblocks | The DOS badblocks command, which is used to test a floppy disk and mark any bad blocks contained on the floppy in its FAT. |
| mcd | The DOS cd command, which is used to change the working directory to another DOS directory. (The default directory is A:\) that is used by other mtools. |
| mcheck | The DOS check command, which is used to verify a file. |
| mcopy | The DOS copy command, which is used to copy files from one location to another. |
| mdel | The DOS del command, which is used to delete files. |
| mdeltree | The DOS delttee command, which is used to delete an MS-DOS directory along with the files and subdirectories it contains. |
| mdir | The DOS dir command, which is used to list the contents of a directory. |
| mdu | The Linux du command, which is used to show the amount of disk space used by a DOS directory. |
| mformat | The DOS format command, which is used to format a DOS floppy disk. |
| minfo | This command is used to print information about a DOS device, such as a floppy disk. |
| mkmanifest | This command is used to create a shell script that restores Linux filenames that were truncated by DOS commands. |
| mlabel | The DOS label command, which is used to make a DOS volume label. |
| mmkd | The DOS md command, which is used to create a DOS directory. |
| mmount | This command is used to mount a DOS disk in Linux. |
| mmove | The DOS move command, which is used to move a file to another directory and/or rename it. |
| mrd | The DOS rd command, which is used to remove a DOS directory. |
| mread | The DOS copy command, which is used to copy a DOS file from one location to another. |
| mren | The DOS ren command, which is used to rename a DOS file. |
| mshowfat | This command is used to show the FAT entry for a file in a DOS file system. |
| mtoolstest | This command is used to test the mtools configuration files. |
| mtype | The DOS type command, which is used to display the contents of a DOS text file. |
| mz | This command is used to perform operations with Zip disks, including eject, write protect, and query. |

I usually use the mtools to copy files between my Linux system and a Windows system that is not on my network. I most often use mcopy, which lets me copy files using drive letters instead of device names. In other words, to copy the file vi.exe from floppy drive A: to the current directory in Linux, I would type:

```
# mcopy a:/vi.exe
```

> **CAUTION:** By default, the floppy-disk drive can be read from or written to only by the root user and the floppy group. To make the floppy drive accessible to everyone (assuming it is floppy drive A:), type the following as root user: `chmod 666 /dev/fd0`.

## Using dosemu and xdosemu

The DOS emulator packages dosemu and xdosemu no longer come with the Red Hat Linux distribution. These packages were previously part of the Red Hat PowerTools. Now you can obtain these packages from a Red Hat Linux FTP site or by using the rpmfind command.

With the utilities that come with the **dosemu** and **xdosemu** packages, you can run DOS applications, as well as use your computer as if it were running DOS. This includes accessing hardware, working with DOS configuration files, and using the DOS file system.

The following commands can be used to start dosemu within Linux:

- `dos` — Starts the DOS emulator in any shell.
- `xdos` — Starts the DOS emulator in its own X window.
- `xtermdos` — Starts the DOS emulator in an xterm window.
- `dosdebug` — Starts a debug program to view information and error messages about a running DOS program.

Basic information about your DOS environment is set in the `/etc/dosemu.conf` file. The following list contains information about how the DOS environment is set up and how to change it:

- **CPU** — The CPU is set to emulate an 80386 (Intel 386-compatible). You can change the `$_cpu` value to 80486 or 80586 (for Pentium).
- **Keyboard** — The keyboard is set to `auto`, which tries to set the keyboard based on the current Linux console settings. You can specifically change the keyboard type by setting the `$_layout` value to a variety of other country/language combinations listed in the `dosemu.conf` file (such as `us` for United States/English, `de` for German, or `it` for Italian).
- **X Settings** — There are several X settings (beginning with `$_x`) that enable you to change such things as the title in the DOS window, the font used, and the blink rate for the cursor.
- **Floppy Disks** — Floppy disk A (`/dev/fd0`) is set to a 3.5-inch floppy (`threeinch`) and floppy disk B (`/dev/fd1`) is not assigned. Either disk can be assigned to be 3.5-inch (`threeinch`), 5.25-inch (`fiveinch`), `atapi`, or `empty`.
- **Hard Disk Images** — The file system that appears when you start DOS is actually a disk image file stored in `/var/lib/dosemu`. By default, dosemu uses `hdimage.first` (which is linked to `hdimage.freedos`). You can change that to another DOS image or to a DOS file system (such as `/dev/hda1`, if that partition were a DOS partition).
- **Serial Ports** — No serial ports are assigned by default. You can assign any of the serial ports (`$_com1` to `$_com4`) to a device such as a modem (`/dev/modem`), a mouse (`/dev/mouse`), or a terminal line (`/dev/tty0`).

Dosemu is set up for the root user. It is not very secure to allow multiple users to have access to DOS because DOS does not have the same security protections for files and devices that Linux does. If you want other users on your Linux system to use DOS, however, edit the `/etc/dosemu.users` file so that it includes the following lines:

```
root c_all
all c_all
```

For more information on dosemu, visit the dosemu home page at www.dosemu.org.

## Running Windows applications with WINE

The WINE project (www.winehq.com) has been making great strides in getting applications that were created for Microsoft Windows to run in Linux and other operating systems. WINE is not really an emulator, because it doesn't emulate the entire Windows operating system. Instead, because it implements Win32 application-programming interfaces (APIs) and Windows 3.x interfaces, the WINE project is more of a “Windows compatibility layer.”

WINE is still under development, although a preliminary version comes with Red Hat Linux on the CDs included with this book. While it's true that you can run many Windows applications using WINE, some fiddling is still required to get most Windows applications to work. If you are considering moving your desktop systems from Windows to Linux, the current state of WINE provides an opportunity to see if some Windows applications you need might run in Linux.

> **CAUTION:** I suggest that you don't use WINE on a computer that is a critical part of your work. Although I haven't done any serious damage to my computer, WINE will still freeze up your desktop under certain conditions.

Besides developing software, the WINE project maintains a database of applications that run under WINE. More than 1000 applications are listed, although many of them are only partially operational. The point is, however, that the list of applications is growing, and special attention is being paid to getting important Windows 3.1, 95, and 98 applications running.

> **TIP:** Although not an open source product, VMware is another good way to run Windows applications along with a Linux system on the same running computer. With VMware you can simultaneously run Windows 98, Windows NT, Windows 2000 and Linux operating systems on the same PC. You can get more information about VMware from www.vmware.com.

The following sections describe how to set up your Linux system to run Windows applications using WINE.

> **NOTE:** A separate project called WineX, from Transgaming, Inc. (www.transgaming.com) has focused on bringing Windows games to Linux, using WINE as its underlying technology. See Chapter 7 for a description of WineX.
