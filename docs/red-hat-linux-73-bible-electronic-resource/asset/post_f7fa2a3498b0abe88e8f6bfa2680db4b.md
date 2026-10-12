
This connects the new file system to the /mnt directory. Now change into the directory (cd /mnt) and use the *restore* command to recover the entire file system off of your backup tape. Of course, it is assumed that you have loaded the correct tape into the tape drive.

```
# cd /mnt
# restore rf /dev/nrft0
```

When the restore is finished, you can unmount the partition and remount it to the appropriate mount point. If you have restored the file system to a different physical partition than it was originally on, be sure to modify the /etc/fstab file appropriately so that the correct partition is mounted next time the system is rebooted.

## Recovering individual files

The *restore* command can also be used to recover individual files and directories. By using *restore* in interactive mode, you can type a series of *restore* commands to selectively restore files. To run *restore* in interactive mode, use the i parameter instead of r:

```
# restore if /dev/nrst0
```

The *restore* command will then read the file index from the backup tape and present you with a *restore* prompt. At this prompt, you can type the commands that enable you to select which directories and files to recover. You can navigate the directory structure of the backup index much the same way you navigate an actual file system using a shell prompt. The interactive *restore* command even has its own version of the familiar cd and ls commands, as shown in Table 13-6.

### Table 13-6: Interactive restore Commands

| Command | Description |
| :--- | :--- |
| Add | Add a file or directory to the list of files to be extracted. If a directory is marked for extraction, all of the directories and files within it will also be extracted. |
| Cd | Change the current directory being viewed within the dump archive. Works similar to the cd command used at a shell prompt. |
| Delete | Delete a file or directory from the list of files to be extracted. Deleting a directory from the list results in all of the files and directories within it also being deleted. |
| Extract | Extract all of the marked files and directories from the archive and write them back to the file system. |
| help | List the available commands. |
| ls | List the contents of the current directory. If a directory name is provided as an argument, list the contents of that directory. Files or directories marked for extraction have a * character in front of them. |
| pwd | Print the full path name of the current directory of the dump archive. |
| quit | Exit the interactive restore program. |
| setmodes | Do not restore the files; instead, set the modes of already existing files on the target disk to match the modes recorded in the dump file. This is useful for recovering from a restore that was prematurely aborted. |
| verbose | Toggles verbose output versus quiet output during the restore process. Verbose output mode will echo information to the screen for every file that is restored. |

As an example, let us pretend that the user joe has accidentally deleted his Mail subdirectory from his home directory. Joe happens to be your boss, so it is urgent that you recover his files. Here is how you may go about it.

Load the appropriate tape into the tape drive and log in as root. Use the cd command to go to the top of the /home partition, and then run the restore program in interactive mode:

```bash
# cd /home
# restore if /dev/nrf0
```

Verify that you have the backup tape for the /home partition by entering the ls command. You should see something like the following list of directories, representing users that have home directories in /home:

```
restore > ls
.
..      bob/      jane/      joe/      lost+found/ mary/      thath/
```

Yes, this is the home partition. Now change the current directory to Joe's home directory using the cd command. Type ls again to view the contents of his home directory.

```
restore > cd joe
restore > ls
./joe:
.netscape/    Desktop/      report.html
.tcshrc        Mail/         letter.txt
.xinitrc       News/         www/
```

Now mark the Mail directory for extraction using the add command:

```
restore > add Mail
```

If we use the ls command again, we see that the Mail directory is preceded with an asterisk (*) character, which means it has been marked for extraction.

```
restore > ls
./joe:
.netscape/ Desktop/ report.html
.tcshrc *Mail/ letter.txt
.xinitrc News/ www/
```

Now use the extract command to begin the extraction process. restore will prompt you for the number of the tape to start with. This is a single tape backup, so just enter the number 1. When it prompts you to “set owner/mode for ‘. ’? ” answer yes by typing y and pressing Enter. restore will then set the file permissions (if necessary) of the directory it is restoring to. This isn’t critical when extracting individual files like this, but you should always answer yes to this prompt when doing a full restore. Anyway, your screen should now contain the following:

```
restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you
should start with the last volume and work toward
the first.
Specify next volume #: 1
set owner/mode for ‘. ’? [yn] y
restore >
```

At this point, the files have been recovered and you can exit the restore program by issuing the quit command. That’s all there is to it. You now know the basics of using the dump and restore commands.

## Backing Up Over the Network

Using dump as described earlier works great when you have a tape drive physically connected to the system that you are backing up. But installing backup hardware in every single device on your network is hardly cost effective. Fortunately, dump has the capability to send data over the network to be written to a device on another server.

To direct the output of dump to a server on the network, you need to modify the backup device argument supplied with the -f option. Include the host name followed by a colon (:) character before the name of the backup device. The dump command will then look for that device on the remote system. For example, to make a backup of the /dev/hda7 partition but write it to a tape drive connected to the computer named ratbert, type the following:

```
# dump 0uBf 500000 ratbert:/dev/nrf0 /dev/hda7
```

Similarly, the restore command can also access devices connected to remote systems. Thus to restore the dump you just made, you would type:

```
# restore rf ratbert:/dev/nrft0
```

The dump and restore commands use the same authentication for remote access as the remote shell service, meaning that you must have appropriate entries in the `.rhosts` or `hosts.equiv` files on the remote system for this to work. Because dump usually runs with root privilege, this can be a security risk.

> **CROSS-REFERENCE:** Refer to Chapter 14 for an explanation of remote shell services and the risks involved using dump and restore over a network.

Another issue with remote dumps is the complications inherent in coordinating backups among many computers. The next section discusses a solution to that problem.

### Performing Network Backups with Multiple Computers

Backing up a single workstation is not a terribly complex job, but backing up an entire network of computers can be. When multiple computers all want to back up their data to the same network-accessible tape drive, coordinating the access so that each computer gets a turn can be difficult.

Simply setting different backup times with each system’s `cron` daemon is not sufficient to manage network backups. If a single backup runs long, all the backups scheduled after it could begin to collide. Fortunately, there is a tool that can help.

The software package Amanda, the Advanced Maryland Automatic Network Disk Archiver, is designed specifically for coordinating the network backup of many machines. With Amanda, you can turn your Red Hat Linux system into a backup server that will archive files for other Linux systems, UNIX, and even Windows 9x/2000 and Windows NT systems.

### Getting and installing the Amanda package

As of Red Hat Linux 7, Amanda is included as one of the standard packages in the Red Hat Linux distribution. Actually, it is split into three distinct packages: the base Amanda package, the client package, and the server package. The base package must be installed before you can install either the client package or the server package. Furthermore, the Amanda server cannot be installed unless the `gnuplot` utility has been installed on your system. Thus, to install Amanda, you should obtain the following four RPM files either from your Red Hat CD media or from a Red Hat Linux FTP site.

- gnuplot
- amanda
- amanda-client
- amanda-server
