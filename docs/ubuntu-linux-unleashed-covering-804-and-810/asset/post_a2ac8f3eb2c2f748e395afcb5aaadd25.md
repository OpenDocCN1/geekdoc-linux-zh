
## Disk Quotas

Disk quotas are a way to restrict the usage of disk space either by user or by groups. Although rarely—if ever—used on a local or standard workstation, quotas are definitely a way of life at the enterprise level of computing. Usage limits on disk space not only conserve resources, but also provide a measure of operational safety by limiting the amount of disk space any user can consume.

Disk quotas are more fully covered in Chapter 10, “Managing Users.”

## Graphical Process and System Management Tools

The GNOME and KDE desktop environments offer a rich set of network and system-monitoring tools. Graphical interface elements, such as menus and buttons, and graphical output, including metering and real-time load charts, make these tools easy to use. These clients, which require an active X session and (in some cases) root permission, are included with Ubuntu.

If you view the graphical tools locally while they are being run on a server, you must have X properly installed and configured on your local machine. Although some tools can be used to remotely monitor systems or locally mounted remote file systems, you have to properly configure pertinent X11 environment variables, such as $DISPLAY, to use the software or use the ssh client’s -X option when connecting to the remote host.

A good graphical process and system management tool is GKrellM, which provides a neat interface and a host of additional plugins. You have to use this command to retrieve GKrellM:

```
$ sudo apt-get install gkrellm
```

or you can use synaptic and after installed it can be found under Applications, System Tools. GKrellM is shown in Figure 12.2.

Some of the graphical system- and process-monitoring tools that come with Ubuntu include the following:

- **vncviewer**—AT&T’s open source remote session manager (part of the Xvnc package), which can be used to view and run a remote desktop session locally. This software (discussed in more detail in Chapter 15, “Remote Access with SSH and Telnet”) requires an active, background, X session on the remote computer.
- **gnome-nettool**—A GNOME-developed tool that enables system administrators to carry out a wide range of diagnostics on network interfaces, including port scanning and route tracing.
- **ethereal**—This graphical network protocol analyzer can be used to save or display packet data in real time and has intelligent filtering to recognize data signatures or patterns from a variety of hardware and data captures from third-party data capture programs, including compressed files. Some protocols include AppleTalk, Andrew File System (AFS), AOL’s Instant Messenger, various Cisco protocols, and many more.

![](img/8f9e74e2b343ff525bebfb720a3d8441_328_0.png)

FIGURE 12.5 Keep a close eye on your free disk space.

- kdf—A graphical interface to your system’s file system table that displays free disk space and enables you to mount and unmount file systems with a pointing device.
- ksysguard—Another panel applet that provides CPU load and memory use information in animated graphs.

## Reference

- http://and.sourceforge.net/—Home page of the and auto-nice daemon, which can be used to prioritize and reschedule processes automatically.
- http://sourceforge.net/projects/schedutils/—Home page for various projects offering scheduling utilities for real-time scheduling.
- http://freetype.sourceforge.net/patents.html—A discussion of the FreeType bytecode interpreter patents.
- http://www.ethereal.com/—Home page for the Ethereal client.
- http://www.realvnc.com/—The home page for the Virtual Network Computing remote desktop software, available for a variety of platforms, including Ubuntu. This software has become so popular that it is now included with nearly every Linux distribution.

resources, and your budget constraints. The following sections look at each of these issues in detail, as well as offering some sample backup systems and discussing their use.

## Why Data Loss Occurs

Files disappear for any number of reasons: They can be lost because the hardware fails and causes data loss; your attention might wander and you accidentally delete or overwrite a file. Some data loss occurs as a result of natural disasters and other circumstances beyond your control. A tornado, flood, or earthquake could strike, the water pipes could burst, or the building could catch on fire. Your data, as well as the hardware, would likely be destroyed in such a disaster. A disgruntled employee might destroy files or hardware in an attempt at retribution. And any equipment might fail, and it all will fail at some time—most likely when it is extremely important for it not to fail.

## A Case in Point

A recent Harris poll of Fortune 500 executives found that roughly two-thirds of them had problems with their backups and disaster-recovery plans. How about you?

Data can also be lost because of malfunctions that corrupt the data as it attempts to write to the disk. Other applications, utilities, and drivers might be poorly written, buggy (the phrase most often heard is “still beta quality”), or might suffer some corruption and fail to correctly write that all-important data you have just created. If that happened, the contents of your data file would be indecipherable garbage of no use to anyone.

All of these accidents and disasters offer important reasons for having a good backup strategy; however, the most frequent cause of data loss is human error. Who among us has not overwritten a new file with an older version or unintentionally deleted a needed file? This applies not only to data files, but also to configuration files and binaries. While perusing the mail lists or the Usenet newsgroup postings, stories about deleting entire directories such as /home, /usr, or /lib seem all too common. Incorrectly changing a configuration file and not saving the original in case it has to be restored (which it does more often than not because the person reconfigured it incorrectly) is another common error.

### TIP

To make a backup of a configuration file you are about to edit, use the cp command:

```
$ cp filename filename.original
```

And to restore it:

```
$ cp filename.original filename
```

Never edit or move the *.original file, or the original copy will be lost.

Proper backups can help you recover from these problems with a minimum of hassle, but you have to put in the effort to keep backups current, verify their intactness, and practice restoring the data in different disaster scenarios.
