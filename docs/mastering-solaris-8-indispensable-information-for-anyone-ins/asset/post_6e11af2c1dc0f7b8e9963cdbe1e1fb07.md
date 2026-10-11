
## Planning Ahead

of the motherboard will in most cases have diagnostics tools within the BIOS. These tools tend to be very limited. Most of them find only IDE hard drives and change BIOS chip default options.

If the hardware on the server is working properly, the server's operating system is the next layer of failure. For an operating system to work, it must have the following hardware:

- A system disk or CD-ROM drive (diskless workstations are not covered here)
- A CPU
- The minimum required memory
- A functional system board
- A keyboard or terminal (required in most cases)

Other optional components, such as a printer or a modem, will not cause the operating system to fail to boot up. These devices add extra functionality to the server but are not required for the minimum operation of a server or workstation. Sun Microsystems provides a wide range of built-in tools for diagnosing operating system problems. The operating system also includes some detailed tracking logs that can indicate when and where a problem has occurred. Most of these logs are in the /var/adm directory. Boot information can be reviewed with the command dmesg. There are cases in which the operating system will save a copy of the system's memory to a file before a system crash. The core dump file can then be sent to Sun support engineers for troubleshooting, provided the warranty or service-level agreement covers the computer.

The final layer of troubleshooting consists of the applications themselves. The applications can be the applications bundled with the operating system (such as FTP or NFS), or they can be applications purchased separately (such as Netscape's Web server). It is extremely difficult to troubleshoot software errors because they can be confused with or intermingled with operating system errors. Most software developers provide troubleshooting tools and troubleshooting logs to track error messages that relate directly to their software. Sun's bundled applications are covered in the docs.sun.com Web page. Third-party vendors' applications are usually covered by some type of support Web page on their respective sites.

There are many situations in which troubleshooting is aided by the system administrator's documentation and by a backup that was performed before a crash or emergency happened. The two key items that must be present before a backup can take place are system documentation and a previous system backup.

### Documentation

System documentation answers the basic question, What is on the computer? The documentation can be in the form of a notebook, a Web page, or a text document. No matter where the documentation is or what form it's in, it must be readily accessible during the troubleshooting process. The system's documentation should never reside only on the system itself. Ask yourself if you will be able to access the documentation if the system goes down. Most large companies put their servers' documentation on secure Web pages. This allows any member of the team to access the information from any location (even at home late at night). This Web page should have all the servers' critical information, such as the host name, IP address, disk labels, and so on. Critical pieces of information not directly related to the server should also be saved:

- The IT manager's home and office telephone numbers
- The in-house software developer's home and office telephone numbers
- The security guard's contact information, to gain access to remote facilities if needed
- Contact information of others who are directly related to the server, such as the system administrator, the computer director, or anyone with superuser status
- Sun telephone support numbers and/or the names of Sun engineers who have worked with the server before
- The location and schedule of backup tapes or the backup server
- Previous notes on past emergency and repair work
- The terminal server's IP address and access information
- The actual location of the server

This information is critical to the fast recovery of a server. Most network teams will hire a junior system administrator to maintain this type of documentation because it tends to be rather boring work.

The Web page should also have some form of username/password security. Hackers will take any piece of information they can in order to compromise a network's security. Ideally, the Web site should be replicated to another offsite server. This eliminates a sitewide location fault.

### Backups

A complete backup is paramount in maintaining an efficient and ongoing system. Backups should be performed on a regular basis and tested to make sure they will restore when needed. Some sites are backed up completely each week and then a copy of the backup is made in case of failure with the first copy. Establish a policy concerning backups and follow it faithfully. It can mean the difference between success and failure when something goes wrong with your system.

### Troubleshooting

A full system backup is sometimes the only thing that will bring a server or workstation back to life. All hardware—particularly computer chips, disks, and cables—have a useful service life; some components have longer MTBF (Mean Time Before Failure) intervals than others. It is therefore inevitable that a backup will be needed at some time in the future, especially if you have numerous servers. The question is not *if* it will be needed; it’s *when* it will be needed.

Mirrored disks and clustered servers can lead some system administrators to develop a false sense of security. Although these concepts do help with system uptime, there are times when corrupt data is introduced to the system. There is also the human factor—accidentally deleting the wrong file or directory, for example. Solaris does not have a file undo/option that is native to the operating system.

There is a wide variety of backup solutions available. Most backup solutions eventually end up with a tape somewhere in the loop. Tape media is the least expensive backup solution to date. Tape also tends to be the slowest media to read and write to. In any case, you need to have a complete backup of the data on your system. It can be either a full backup or an older full backup and any up-to-date incremental changes to the file system since the last full backup. Partial backups of changes occur frequently (sometimes daily). A full backup is done usually on a monthly basis. It includes all the programs and software. Incremental backups include only the changes or additions made since the last full backup.

If a full backup is not available at the time of a system crash, try to perform a full backup as soon as possible. There are situations in which the system will have limited functionality. Perhaps the server cannot communicate over the network but the hard drives and tape drive are still accessible through the terminal server. In these cases, it might be possible to do a full backup before continuing on with the troubleshooting. The main point is that it’s important to have a full backup or to make a full backup of the system before troubleshooting. Once a file or directory is deleted in Solaris, it cannot be recovered.

> When working on a critical system text file, make a backup copy before editing it even if the file exists on tape. Some partitions are several terabytes in size. It can be extremely time consuming to try to recover a single file. Also, Solaris is very sensitive to hidden characters and incorrect spaces in some files. It isn’t too difficult to make tar archives of the /etc directory before troubleshooting.

## The Psychology of Troubleshooting

This section is without a doubt the most important section in this chapter. Being in the right frame of mind during an emergency troubleshooting situation is 90 percent of the battle. A frantic “poke around–change something–try something else” method is the worst possible method in a troubleshooting situation. When an individual becomes panicked, compounded errors can make a problem situation worse. It can become impossible to retrace one’s steps.

![](img/256e02a6afce528d264a8d911fa0ff20_816_0.png)

> **TIP** One of the most important steps in troubleshooting is to try to relax, collect your thoughts, and formulate a recovery plan.

Frantically editing files and making changes can make the situation worse. Although there may be times this technique will bring a server back to life very quickly, in most cases, unfortunately, it only produces a false sense of security and accomplishment. An emergency situation can be a learning process that can highlight weaknesses in documentation and backups. The quick-and-dirty session may be regarded as a victory while critical documentation and backup problems are allowed to persist and may lead to future problems such as an unrecoverable system crash. If the backup system, for whatever reason, failed to produce a useable backup, the server’s data may never be retrieved.

![](img/256e02a6afce528d264a8d911fa0ff20_816_1.png)

> **TIP** Test your backups frequently to see if you can actually use them to restore data. Make sure your backup media contains the data you think it contains.

When troubleshooting, try to avoid taking any irreversible steps. Most changes to the system can be reversed if documented. Copy a file before making changes. Instead of deleting a file, change its name or location to nullify the file’s function (provided disk space exists). Make a copy of a disk before you change the size of the slices. Don’t throw away a component before the new component is proven to work. There are countless examples of situations that can’t be reversed.
*Don’t guess.* Guessing rarely works, and it can take more time to repair damage done by guessing than to repair the original problem. The chance of your Sun workstation or server and the Solaris operating system having a unique problem that has not been encountered and solved before is rare. If you become skilled at using SunSolve Online
