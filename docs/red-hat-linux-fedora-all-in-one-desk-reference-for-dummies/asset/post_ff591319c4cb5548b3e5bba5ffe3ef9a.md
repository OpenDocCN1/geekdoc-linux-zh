
same protocol that Web servers use. The client application uses IPP to inquire about capabilities of a printer, submit print jobs, and inquire about — or cancel — print jobs.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_515_0.png)

If you have set up a CUPS print queue for a printer connected to your Red Hat Linux system (following the directions in Book I, Chapter 3), you can print on that printer from Windows XP and 2000 systems on your local area network. Windows 2000 and XP have built-in support for IPP — the protocol used by CUPS. To print on a CUPS print queue from a Windows XP system, add a network printer on the XP. In the Add Printer Wizard, select Connect to a Printer on the Internet or on a Home or Office Network and then enter the URL for the CUPS print queue. For example, for a CUPS print queue named HPLaserJetRoom210 on a Red Hat Linux host whose IP address is 192.168.0.8, I enter the following URL for the print queue:

```
http://192.168.0.8:631/printers/HPLaserJetRoom210
```

As a Red Hat Linux user, you use a client program — lp or lpr — to send the files to be printed to a print scheduler called cupsd over a TCP/IP network connection. The cupsd scheduler then queues the files, processes them according to their file extensions (such as .txt or .ps), and sends them to the printer one by one. Thanks to various configuration files, the cupsd scheduler knows what to do to make sure that the file — be it a text file or an image file — gets printed properly.

Although you typically have only one printer connected to your PC, one advantage of the CUPS printing system is the capability to print on a printer connected to another system on a network. Printing to a remote printer is handled in the same fashion as printing to a local printer: The local lp or lpr program simply sends the files to the remote system's cupsd scheduler.

## Printing with the lp command

You can print a file by using the lp or lpr command. For example, to print the file /etc/inittab, type the following in a terminal window:

```
lp /etc/inittab
```

The lp command queues a print job by sending the file and appropriate control information to the cupsd print scheduler. By default, the cupsd print scheduler accepts files to be printed, holds them in the print queue, and forwards them to the default printer (or to another system if the default printer is attached to a remote system on the network). The default printer is identified by the <DefaultPrinter queuename> entry in the CUPS configuration file /etc/cups/cupsd.conf (where queuename is the name of the print queue).

## Checking the print queue using lpq

You can embellish the simple lp command with some options. If you have many different print queues defined, you can specify the destination of the print job with the -d option. For example, to send a print job to the Hewlett-Packard LaserJet print queue named HPLaserJetRoom210 you would type the following command (the print queue name appears in the /etc/cups/printers.conf file):

```
lp -d HPLaserJetRoom210 testprint.ps
```

If you mistakenly print a large file and want to stop the print job before you waste too much paper, you can use the lpq command to look at the current print jobs and then cancel the large print job. Following is a typical a listing of print jobs I get when I type lpq after submitting a file to the HPLaserJetRoom210 print queue:

```
HPLaserJetRoom210 is ready and printing
Rank Owner Job File(s) Total Size
active root 2 testprint.ps 15360 bytes
```

The lpq command shows the job number (2) and the name of the file that I am printing (testprint.ps).

## Canceling the print job using cancel

To remove a job from the print queue, use the cancel command. For example, to remove print job 2, type the following command:

```
cancel 2
```

You can get the same result with the following lprm command:

```
lprm 2
```

If you're in a hurry and want to cancel all print jobs you have submitted so far, use cancel with -a as the argument, as follows:

```
cancel -a
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_516_0.png)

## Checking the printer status using lpstat

To see the status of print jobs, use the lpstat command. Here is a typical output from the lpstat command:

```
lpstat
HPLaserJetRoom210-2 root 15360 Wed 25 Jan 2003 04:25:48 PM EST
```

## Controlling the print queue

The first field of the output shows the name of the queue with a job number appended to it (that number identifies the print job). You need that job number to cancel the print job.

To see the names of printers connected to your system, use the `lpc status` command. On my system, the `lpc status` command shows the following:

```
lpc status
HPLaserJetRoom210:
    printer is on device 'parallel' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present
```

Notice that queuing and printing are both enabled for this printer. The last line tells you that the `cupsd` daemon (a server that runs all the time) is running and available to handle print jobs.

You can use the `accept` and `reject` commands to enable or disable queuing for a print queue. For example, to stop queuing further print jobs for the `HPLaserJetRoom210` printer, I type

```
reject HPLaserJetRoom210
```

This command disables queuing jobs for this printer. If anyone tries to send a print job using the `lp` command, the user receives an error message like this:

```
lp: unable to print file: server-error-not-accepting-jobs
```

If you want to allow queuing of print jobs, but want to start or stop the printing, use the `enable` and `disable` commands. When you disable printing, users can submit print jobs, but nothing gets printed until you enable printing again. For example, here is the command I use to disable printing on the `HPLaserJetRoom210` printer: `disable HPLaserJetRoom210`

![](img/a7eec43a54473e95dc5ea333fecf1bd7_517_0.png)

If you're trying to print, but nothing seems to be coming out of the printer, check the printer status with the `lpc status` command and make sure that the `cupsd` scheduler is present and that both queuing and printing are enabled. To allow the queuing of print jobs, use the `accept` command and to start printing, use the `enable` command.

## Chapter 6: Upgrading and Customizing the Kernel

### In This Chapter

- ✔ Upgrading with a Red Hat kernel RPM
- ✔ Configuring the kernel
- ✔ Building a new kernel
- ✔ Building and installing the modules
- ✔ Installing the kernel and setting up GRUB

One reason Linux is so exciting is that many programmers are constantly improving it. Some programmers, for example, write drivers that add support for new hardware, such as a new sound card or a new networking card. All these innovations come to you in the form of new versions of the Linux kernel.

Although you don’t have to upgrade or modify the Linux operating system — the kernel — every time a new version is available, sometimes you have to upgrade simply because the new version corrects some problems or supports your hardware better. On the other hand, if an earlier kernel version has everything you need, there is no need to rush out and upgrade.

Sometimes you may want to rebuild the kernel even when there are no fixes or enhancements. The Linux kernel on the companion DVD is generic and uses modules to support all types of hardware. You may want to build a new kernel that links to the drivers for only the devices installed on your system. In particular, if you have a SCSI hard drive, you may want to create a kernel that supports your SCSI adapter. Depending on your needs, you may also want to change some of the kernel configuration options, such as creating a kernel that’s specific for your processor (instead of a generic Intel 386 processor).

In this chapter, I explain how to upgrade a kernel using a kernel RPM as well as how to rebuild and install a new Linux kernel.

## Upgrading with a Red Hat Kernel RPM

Red Hat distributes all software updates, including new versions of kernels, in the form of RPM files. To download and install the kernel RPMs, follow these steps:

- 1. **Use a Web server to download the kernel RPM files from Red Hat's FTP server (I explain the details in the next section).**
- If you want to rebuild the kernel, you have to download the `kernel-source` RPM corresponding to the new version of the kernel.
- 2. **Install the RPMs by using the `rpm -i` command.**
- 3. **Create a new, initial RAM disk by running the `/sbin/mkinitrd` command.**
- 4. **Reconfigure GRUB to boot the new kernel.**
- 5. **Try out the new kernel by rebooting the system.**

I further describe these steps in the next few sections.

### Downloading new kernel RPMs

Red Hat makes software updates available in the form of RPMs — packages — at its FTP server or one of the mirror sites listed at www.redhat.com/download/mirror.html. The updates are organized in directories according to Red Hat Linux version numbers. For example, any updates for Red Hat Linux 9 for Intel x86 systems reside in the 9/en/os/i386 directory. Use a Web browser (for example, Mozilla) to visit the FTP site and download any kernel RPMs available at that site.

### Installing the kernel RPMs

To install the kernel and the modules, follow these steps:

- 1. **Log in as root.**
- 2. **Use the `cd` command to change the directory to where the RPM files (the ones you have downloaded from Red Hat's FTP server) are located.**
- 3. **Type the following command to install the kernel RPM:**
  `rpm -ivh kernel*.rpm`

You have to install the `kernel-source` RPM only if you want to build a new kernel.
