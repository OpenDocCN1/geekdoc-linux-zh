

+ signals to control timing sensitive applications, and can support alarms. You will have to provide additional settings elsewhere in the software to ensure that the hardware time stays correct.

- **Line 41** displays the RAM disk drive, which allocates a portion of your physical RAM for saving files and for accessing often used files. This is not always the most effective use of RAM since the Linux buffer cache does the same automatically. Most commonly RAM drives are used during the initial Linux install process.
- Next, Linux determines what types of physical hard drives, CD-ROMs, and floppy drives are installed on the computer. This is covered on lines 42–53. There is one Maxtor 20 gigabyte IDE drive, one ATAPI CD-ROM, and no floppy drives.
- On lines 54–64, the startup process initializes the RAID code and optimizes the fastest method of computing checksums on the RAID. Locating and mounting RAID devices comes later.
- **Lines 65–67** list the partition check results. These are the partitions as you set them up during the initial install.
- **Lines 68–70** show the kernel detecting any additional RAID arrays and beginning the autorun sequence, which attempts to find all drives that belong to each RAID set.
- Next, on line 71, the root file system is mounted using the ext2 file format.
- **Lines 72–79** define the SCSI controller card and verify that certain requirements are met in order for the card to function properly under Linux. The “0:2:0” notation means “channel # : SCSI ID # : LUN”.
- Once the SCSI card has been properly detected, any peripheral devices are then displayed. The two devices displayed are both SCSI tape backup devices. Linux displays their makeup under lines 80–85. The first has a SCSI ID number of 2 and is an internal HP auto tape loader, while the second is an external single-tape backup device. They are assigned the same driver and identity.

## NOTE

Rather than poring over the dmesg file once the operating system has been loaded, you can reaffirm the identity of your SCSI devices by typing *cat /proc/scsi*. This will display all devices attached to your SCSI card.

- Lines 86 and 87 show how Linux un-mounts the old root boot file and then mounts the root file.
- Line 88 shows how much memory is released during the startup.
- Line 89 displays the amount of physical swap space mounted for the system's use.
- Line 90 sets the buffer size for the SCSI tape device, or /dev/st.
- Lines 91 and 92 describe the SCSI devices in more detail, now that the kernel is running. Here again you can see the LUN numbers assigned to each respective drive.
- The last series of lines, 93–110, show how Linux begins the networking aspect by detecting the two Ethernet cards. Both are Intel Express 10/100 cards. The first is assigned the designation of eth0, or Ethernet interface 0, and the second eth1. (Remember that Linux begins counting with the number 0 and not the number 1.)

The dmesg command shows only the startup sequence for the hardware and kernel variables. The loading of daemons is yet another aspect to the bootup process and is not handled by the dmesg command. Daemons do not have to be successful in their initialization in order for the machine to start properly or to reach a login prompt. The hardware, however, must boot up properly. Certain daemons might fail to load and will time out. If this occurs, the machine will continue booting but will not load all the daemons. This is true in the case of the sendmail daemon, which hangs if not on a network or if it is unable to determine the machine name. This will not prevent Linux from loading, but will cause a delay in the boot process.

Each system's configuration varies slightly depending upon the distribution, the hardware installed, and the configuration of the kernel. Once all the variables have passed the initial startup sequence, only then will Linux attempt to load any daemons or scripts. This topic will be covered in the next section.

Finally, when all is running the console will display the Red Hat release name and number. This information is based on the text loaded in the /etc/issue file. You can customize this to your own specifications and enter any additional text particular to that machine. Under the release number will be the kernel version and the type of machine on which it is operating. You will then see a login prompt awaiting a username and password.

# Running Daemons in the Background

Linux keeps many processes continuously running. In addition to starting up separate programs when the user calls them, Linux finds it also effective to run daemons, or processes that are continuously operational. These can either await requests from the user or that run various operations in the background as determined by system needs. In this manner, background processes can handle programs more quickly and effectively.

A Linux daemon is a *background process*—a process that runs without outputting information to the screen, but which constantly observes and monitors system status and performs tasks automatically. These may or may not be dependent upon the user. You can query a daemon at any time about its status but it will not normally make itself known to the user. Certain daemons are modularized and kept out of the running kernel so that they do not increase the kernel’s size and thus slow down Linux’s performance. Daemons are started at bootup, right after kernel initialization, and continue to function for as long as the system is running or until the administrator changes their status. This is the second stage of the bootup process and follows the hardware recognition portion. Linux users can start and shut down daemons as different needs arise or when system changes require initialization or updating. However, the entire system manages itself with minimal interaction with users.

Daemons have the responsibility to sort out the incoming stream of data, looking for input that matches the parameters specified by the daemons, and then to determine what priority each command receives. Think of a daemon as a security guard who sits in a back room, watching a vast array of monitors, taking care of specific issues when the need arises. For more information about how processes are managed and prioritized, see Chapter 7, “Identifying Processes.”

One function of a daemon is to monitor conditions on the system. One of the most well-known daemons is the *cron* daemon. Short for *chronological*, cron works at particular time intervals to manage automatic processes. It is a text file containing times and specific commands that are initiated by the system at specific intervals. Every few moments it wakes up and checks one of the many *cron files*, or text files containing programs or daemons, to see whether any commands need to be executed. If not, the daemon goes back to sleep, awaiting the next time that it must check for programs. If, upon checking the various files, cron finds a command or text file with a start time that corresponds to the same time on the system clock, the daemon will carry out that command, running until the task is complete.

## Starting Daemons with inetd

As daemons gained popularity among early UNIX, and now Linux, users, they began to slow down system performance since they all started at boot. With so many processes running and vying for memory and CPU usage, serious performance problems developed. BSD created the *inetd* daemon, or **inetd**, in response to this issue. This command is a daemon that spawns other daemons when the needs arises. The inetd command became so successful that other versions of UNIX decided to include it as well. Linux is optimized to use inetd for most all its network daemon management. It is this program that sets the standards and limits for many daemon processes. The inetd command is commonly recognized by many today as being the prime daemon and is crucial in maintaining network integrity on Linux systems. Because Linux is most commonly used for Internet-related systems—such as web and FTP servers, telnet, and so on—inetd carries the burden of making sure that these Internet services are configured and started properly. When a request is made to the system for one of these services, it is inetd that spawns the additional Internet daemons as required.

## Understanding System-Specific Daemons

The very first process to start when Linux is powered up is init. It is considered the most important process and as such receives a process ID number, or PID, of 1. PIDs, or process ID numbers, help Linux keep track of each process and also helps the user to make changes or track what the system is doing. Thus init is the first process and spawns many of the later processes. All other processes other than those created by the Linux kernel are descendants of init.

Inetd is the daemon that controls and manages several other daemons, aside from those handled by the kernel or by client processes such as cron, atd, and database daemons. It calls those daemons that are needed by the system to perform various duties. Once they have completed their task, init allows them to die gracefully. Like most other daemons, inetd requires root access to run. Since it is what spawns the other daemons, it requires special permissions to perform those tasks that can be done only by or as superuser or root. As such, inetd is extremely powerful and can call certain processes into life and kill them as well.

