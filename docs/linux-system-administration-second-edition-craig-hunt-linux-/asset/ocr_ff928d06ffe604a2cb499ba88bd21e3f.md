+   3. Edit the automounter's configuration file, /etc/auto.master. It normally contains a single line that lists the base automount point (/misc by default), the configuration file for that mount point (/etc/auto.misc by default), and a timeout value (60 by default). Change any of these parameters as needed. If this line is commented out, uncomment it to activate it.
4. Edit the /etc/auto.misc configuration file. This file should list specific subdirectories within the base automount point (/misc), filesystem type codes, and device files for each device you want auto—mounted. For example:

```
```
floppy	-fstype=auto	:/dev/fd0
maczip	-fstype=hfs	:/dev/sda
```
```

This example sets the automounter to check /misc/floppy for floppy disk accesses using any filesystem (type auto) and /misc/maczip for HFS filesystems mounted on a SCSI Zip drive (/dev/sda).

+   5. Start the automounter by typing /etc/rc.d/init.d/autofs start. It should start up automatically when you reboot the computer, as well. (If you're not using Red Hat, you may need to use another startup script, or start the automounter manually by typing automount /misc file /etc/auto.misc.

You do *not* create directories within the /misc directory for each mount point. Instead, the automounter detects attempts to access nonexistent directories and dynamically creates them when mounting the device. This fact can make the automounter ineffective if you use a file manager, since these programs typically only let you access existing directories. The automounter is useful, however, when you use command-line tools.

**Note** In addition to autofs, a second automounter implementation, the automounter daemon (amd), is available for Linux. See "Linux NFS and Automounter Administration," by Erez Zadok, for the most complete documentation of amd available.

# # Using Swap Space

One type of disk access is critically important to Linux but has not yet been mentioned in this chapter: *swap space*. This is disk space that's set aside as auxiliary to system memory (RAM). Suppose your computer has 256MB of RAM, but you want to run 380MB worth of programs on the system. Swap space allows you to accomplish this, by treating disk space as if it were RAM. The result is that you can run all 380MB worth of programs—albeit more slowly on this 256MB computer than on a machine that has in excess of 380MB of RAM.

Linux typically assigns one or more disk partitions as swap space. These partitions use the type code **0x82** (*Linux swap*), as described in "Disk Partitioning." It's also possible to use an ordinary disk file as swap space. Normally, Linux sets up a swap partition during system installation, so this feature is handled automatically. You may want to adjust this default configuration, however.

You can find out how much swap space your system currently has by typing **free**, which produces output like the following:

|			total	used	free	shared	buffers	cached|
|:-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|-------------:|
| Mem:				127752	121416	6336	61108	26748	53316|
| -/+ buffers/cache:	41352	86400|
| Swap:			136512	4928	131584|

Pay particular attention to the line labeled Swap. Under the Total column is the number of kilobytes of swap space available to the system. The Used and Free columns list how much of that space is