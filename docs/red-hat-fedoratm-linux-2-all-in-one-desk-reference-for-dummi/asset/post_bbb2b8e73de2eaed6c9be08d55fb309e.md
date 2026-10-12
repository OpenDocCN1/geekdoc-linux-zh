
# Managing USB Devices

USB2, for short) ups the ante by raising the data transfer rates to a whopping 480 Mbps, slightly faster than the competing IEEE 1394 (FireWire) bus. Nowadays many devices, such as CD burners and scanners, come with the high-speed USB2 interface. If your PC has older USB 1.1 ports, the USB2 devices can still work, albeit at lower data-transfer rates. Fedora Core supports both USB 1.1 and USB2 interfaces.

Using USB devices in Fedora Core is easy. You can hotplug a device into a USB port, and the Linux kernel can detect and load the appropriate device drivers so applications can make use of the device. To be more precise, the kudzu hardware detection utility takes care of the chores necessary to make the USB device accessible to applications. For USB mass storage devices, such as CD drives or hard drives, kudzu can also mount the device on the Linux file system. For examples of using USB mass-storage devices, see Book II, Chapter 4 where I discuss how Linux detects a USB CD burner and how to access the photos in a digital camera through the USB interface.

To use a USB printer in Fedora Core, simply connect the printer to the USB port, power it up, and then follow the steps in Book I, Chapter 3 to configure a locally connected queue for the printer. The printer shows up with a device name such as `/dev/usb/lp0` (for the USB printer detected by kudzu) or `/dev/usb/lp1` (for the second USB printer), and so on.

Using USB scanners in Fedora Core is as simple as using USB printers. Just plug the scanner into the USB port, power it up, and you can access it by using `xsane` -- a graphical front end for scanners that you can start by choosing Main Menu > Graphics > Scanning. Of course, `xsane` must support the USB scanner make and model. To quickly check whether kudzu has detected your USB scanner, log in as root and type `sane-find-scanner` in a terminal window.

The kernel can also automatically mount a USB mass storage device for easy access. Consider, for example, the USB keychain storage device. Just as the name says, these are small memory cards, capable of storing anywhere from 32MB to 1GB. You can carry them around on a keychain -- in effect, taking all your data with you wherever you go. Here's how you can use a USB keychain storage device that's already formatted for use in Microsoft Windows:

1. Plug the keychain storage device to the PC's USB port.

   Sometimes the device plugs directly into the port, but for some devices you have to attach the keychain device to a USB cable and then plug the cable into the USB port.

   Some USB keychain devices have a small switch on the side that controls whether the keychain is write-protected. If you plan to write to the device, first make sure it's not write-protected or locked.

   ![](img/9f89727199836b0f871f1745838aa8b2_513_0.png)
   ![](img/9f89727199836b0f871f1745838aa8b2_513_1.png)
   ![](img/9f89727199836b0f871f1745838aa8b2_513_2.png)

2. Kudzu detects the USB storage device and adds an entry in `/etc/fstab` that associates the USB device with the mount point `/mnt/flash`. Mount the device with the command:

   ```
   mount /mnt/flash
   ```

3. To check that the USB device is mounted, type the following command and look for a line in the output that shows `/mnt/flash`:

   ```
   df
   ```

   For example, the following line of output is for a 32MB USB keychain device:

   ```
   /dev/sda1 31520 64 31456 1% /mnt/flash
   ```

   If you don't have any other USB device plugged in, the device name is `/dev/sda1` (USB storage devices appear as SCSI devices). The next USB storage device gets the `/dev/sda2` device name and so on.

   Now you can access the files on the keychain at the `/mnt/flash` directory. To save a file to the USB keychain storage device, use a command of the following form:

   ```
   cp filename /mnt/flash
   ```

   where *filename* is the name of the file you want to save.

   When you're done using the device, unmount the USB keychain with this command:

   ```
   umount /dev/sda1
   ```

   That's it!

# Managing Print Queues in Fedora Core

PCs typically come with one parallel port, typically used to connect the printer to the PC. You can set up a printer fairly easily by using Fedora Core's graphical printer-configuration utility, but you also have to know how to manage the print queue.

## Spooling and print jobs

*Spooling* refers to the capability to print in the background. When you print from a word processor in Windows, for example, the output first goes to a file on the disk. Then, while you continue working with the word processor, a background process sends that output to the printer. The Fedora Core printing environment also supports spooling.

*Print job* refers to what you print with a single print command. The printing environment queues print jobs by storing them in the spool directory. A background process periodically sends the print jobs from the spool directory to the printer.

Fedora Core uses the Common UNIX Printing System (CUPS) for its printing environment. CUPS is a printing system based on the Internet Printing Protocol (IPP) — a protocol for distributed printing using Internet technologies. IPP assumes a client/server model with the client being an application and the server a “Printer” — an abstraction of an output device or a printing service provider. IPP supports a distributed printing environment with the clients and Printer servers communicating over the Internet. You could use an IPP client to print on a printer anywhere on the Internet. The client and Printer exchange data using the HTTP 1.1 protocol — the same protocol that Web servers use. The client application uses IPP to inquire about capabilities of a printer, submit print jobs, and inquire about — or cancel — print jobs.

![](img/9f89727199836b0f871f1745838aa8b2_515_0.png)

If you have set up a CUPS print queue for a printer connected to your Fedora Core system (following the directions in Book I, Chapter 3), you can print on that printer from Windows XP and 2000 systems on your local-area network. Windows 2000 and XP have built-in support for IPP — the protocol used by CUPS. To print on a CUPS print queue from a Windows XP system, add a network printer on the XP. In the *Add Printer Wizard*, select **Connect to a Printer on the Internet or on a Home or Office Network** and then enter the URL for the CUPS print queue. For example, for a CUPS print queue named `HPLaserJetRoom210` on a Fedora Core host whose IP address is 192.168.0.8, I enter the following URL for the print queue:

```
http://192.168.0.8:631/printers/HPLaserJetRoom210
```

As a Fedora Core user, you use a client program — `lp` or `lpr` — to send the files to print to a print scheduler called `cupsd` over a TCP/IP network connection. The `cupsd` scheduler then queues the files, processes them according to their file extensions (such as `.txt` or `.ps`), and sends them to the printer one by one. Thanks to various configuration files, the `cupsd` scheduler knows what to do to make sure that the file — be it a text file or an image file — gets printed properly.

Although you typically have only one printer connected to your PC, one advantage of the CUPS printing system is the capability to print on a printer connected to another system on a network. Printing to a remote printer is handled in the same fashion as printing to a local printer; the local `lp` or `lpr` program simply sends the files to the remote system's `cupsd` scheduler.

## Printing with the lp command

You can print a file by using the `lp` or `lpr` command. For example, to print the file `/etc/inittab`, type the following in a terminal window:

```
lp /etc/inittab
```

The `lp` command queues a print job by sending the file and appropriate control information to the `cupsd` print scheduler. By default, the `cupsd` print scheduler accepts files to be printed, holds them in the print queue, and forwards them to the default printer (or to another system if the default printer is attached to a remote system on the network). The default printer is identified by the `<DefaultPrinter queuename>` entry in the CUPS configuration file `/etc/cups/cupsd.conf` (where *queuename* is the name of the print queue).

You can embellish the simple `lp` command with some options. If you have many different print queues defined, you can specify the destination of the print job with the `-d` option. For example, to send a print job to the Hewlett-Packard LaserJet print queue named `HPLaserJetRoom210`, you type the following command (the print queue name appears in the `/etc/cups/printers.conf` file):

```
lp -d HPLaserJetRoom210 testprint.ps
```

## Checking the print queue using lpq

If you mistakenly print a large file and want to stop the print job before you waste too much paper, you can use the `lpq` command to look at the current print jobs and then cancel the large print job. Following is a typical listing of print jobs I get when I type `lpq` after submitting a file to the HPLaserJetRoom210 print queue:

```
HPLaserJetRoom210 is ready and printing
Rank   Owner Job    File(s)
active root    2     testprint.ps                 Total Size
                                                      15360 bytes
```

The `lpq` command shows the job number (2) and the name of the file that I am printing (*testprint.ps*).

## Canceling the print job using cancel

To remove a job from the print queue, use the `cancel` command. For example, to remove print job 2, I type the following command:

```
cancel 2
```
