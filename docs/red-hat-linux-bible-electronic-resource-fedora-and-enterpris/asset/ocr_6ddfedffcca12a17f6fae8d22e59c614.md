+   * **X Settings** There are several X settings (beginning with $\_x)$ that let you change things such as the title in the DOS window, the font used, and the cursor blink rate.

+   * **Floppy Disks** — Floppy disk A ($/dev/fd0$) is set to a 3.5-inch floppy (three-inch) and floppy disk B ($/dev/fd1$) is not assigned. Either disk can be assigned to be 3.5-inch (three-inch), 5.25-inch (five-inch), atapi, or empty.

+   * **Hard Disk Images** — The file system that appears when you start DOS is actually a disk image file stored in /var/lib/dosemu. By default, dosemu uses hdimage.first (which is linked to hdimage.freedos). You can change that to another DOS image or to a DOS file system (such as $/dev/hda1$ if that partition were a DOS partition).

+   * **Serial Ports** — No serial ports are assigned by default. You can assign any of the serial ports ($\_com1$ to $\_com4$) to a device such as a modem ($/dev/modem$), a mouse ($/dev/mouse$), or a terminal line ($/dev/tty0$).

Dosemu is set up for the root user. It is not very secure to allow multiple users to have access to DOS because DOS does not have the same security protections for files and devices that Linux does. If you want other users on your Linux system to use DOS, however, edit the /etc/dosemu.users file so that it includes the following lines:

```
root c_all
all c_all

```

For more information on dosemu, visit the dosemu home page at www.dosemu.org.

# Running Windows applications with WINE

The WINE project (www.winehq.com) has been making great strides in getting applications that were created for Microsoft Windows to run in Linux and other operating systems. WINE is not really an emulator, because it doesn't emulate the entire Windows operating system. Instead, because it implements Win32 application programming interfaces (APIs) and Windows 3.x interfaces, the WINE project is more of a “Windows compatibility layer.”

To get WINE for your Red Hat Linux system, there are several places you can go:

+   * **Download sites** — You can download WINE free of charge from several different Web sites. Check winehq.com for a list of download sites. I downloaded the latest RPMs built for Red Hat Linux from this site:
+     	  http://sourceforge.net/projects/wine/. WINE daily builds (in RPM format) are available from http://wine.dataparty.no.

+   * **WineX** — A commercial version of WINE, called WineX, is available from TransGaming, Inc. (www.transgaming.com). TransGaming focuses on running Windows games in Linux, using WINE as its base. See Chapter 7 for descriptions of WineX.