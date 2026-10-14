
## Administer Processes, Start and Stop the System

- unalias—Removes an alias name
- uname—Shows the name of the operating system (Linux)
- unset—Deletes a shell variable
- bg—Continues an interrupted process in the background
- chkconfig—Enables or disables system services
- fg—Moves a process running in the background to the foreground
- fuser—Displays the PIDs of processes using the specified files or file systems
- halt—Ends all processes currently running (shut down)
- init—Allows switching to another runlevel or reloading the /etc/inittab file without changing the runlevel
- insserv—Creates symbolic links in the /etc/init.d/rcrunlevel.d directories
- jobs—Lists all processes that have been started from the shell and run in the background
- kill—Passes on signals to processes (the PID is specified)
- killall—Passes on signals to processes (the command name of the process is specified)
- lsof—Lists open files
- netstat—Shows which network ports are offering services and what connections are established
- nice—Sets the nice value of a process with its start
- nohup—Starts a process or program, which then continues running after logout
- poweroff—Ensures an immediate, controlled system halt
- ps—Lists processes
- pstree—Displays currently running processes in the form of a process tree
- reboot—Ends all running processes and then reboots the computer
- renice—Changes the nice value of a running process (PID required)
- shutdown—Shuts down the Linux system
- top—Lists processes according to computer time used

## Monitor the System

- df—Specifies where hard drives and their partitions or other drives are mounted in the file system, and how much space they occupy
- dmesg—Shows the content of the kernel ring buffer
- du—Provides information about the space occupied by files and directories
- hdparm—Lets you view information about your hard drive and manage certain hard drive parameters
- hwinfo—Generates and displays a list of specific information about the devices installed on your Linux system
- iostat—Displays CPU and input/output (I/O) statistics for devices and partitions
- logrotate—Monitors size and age of log files
- lspci—Displays information on all PCI buses in your Linux system and all devices connected to them
- rpcinfo—Displays information on the portmapper
- showmount—Displays information on the exported directories of an NFS server
- siga—Collects various information on your system and outputs it in HTML or ASCII format
- uptime—Displays the current time, the length of time the system has been running, the number of users on the system, and the average number of jobs in the run queue over the last 1, 5, and 15 minutes

## Install Software

- configure—Creates and customizes a makefile
- ldconfig—Updates the /etc/ld.so.cache file
- ldd—Provides information about the libraries required by a program, where they are located, and which ones are missing
- make—Compiles a program
- rpm—Manages packages in the RPM Package Manager format
- rpmbuild—Builds RPM Packet Manager packages

## Manage Hard Disks and File Systems

- fdisk—Partitions a hard drive
- mke2fs—Creates an ext2 or ext3 file system
- mkfs—Creates a file system on a storage medium
- mkreiserfs—Creates a file system in the Reiser file system format
- mount—Mounts a device file into the file system
- reiserfstune—Adjusts tunable file system parameters on a Reiser file system
- resize_reiserfs—Shrinks or enlarges a Reiser file system
- resize2fs—Shrinks or enlarges an ext2 or ext3 file system
- tune2fs—Adjusts tunable file system parameters on ext2 and ext3 file systems
- umount—Removes a device file from the file system

## Automate Tasks

- `at`—Executes commands at a specified time
- `atq`—Lists the at jobs
- `atrm`—Deletes at jobs, identified by their job number
- `crontab`—Maintains crontab files for individual users

## Repair the System

- `badblocks`—Searches for bad blocks on a partition
- `chroot`—Creates a new root directory
- `debugfs`—Is an ext2 file system debugger
- `debugreiserfs`—Is a debugging tool for the Reiser file system
- `dumpe2fs`—Provides information on the state of the file system
- `e2fsck`—Checks and repairs an ext2 or ext3 file system
- `fsck`—Checks the consistency of the file system and carries out repairs if necessary
- `reiserfsck`—Checks and repairs a Reiser file system

## Use Online Help

- `apropos`—Searches names and descriptions of manual pages
- `info`—Starts the online help system with the same name
- `man`—Displays online information for a given command
- `whatis`—Displays manual page descriptions

## Work with Kernel and Modules

- `partprobe`—Gets the kernel to use a new partition table
- `depmod`—Generates dependencies of individual modules
- `insmod`—Loads a module into the kernel
- `lsmod`—Lists the kernel modules
- `modinfo`—Displays information about kernel modules
- `modprobe`—Loads a module into the kernel, taking into account module dependencies
- `rmmod`—Removes a module from the kernel

## Printing (CUPS)

- `accept`—Sets queue to accept print jobs after it was set to reject print jobs with reject
- `cancel`—Removes a print job from the queue
- `disable`—Stops a queue
- enable—Enables a queue that was disabled
- lp—Sends off a print job
- lpadmin—Manages the print queue
- lpoptions—Configures the print queue
- lpq—Displays print jobs
- lpr—Sends off a print job
- lprm—Removes a print job from the queue
- lpstat—Displays print jobs
- mpage—Converts ASCII to PostScript and enables printing of multiple pages on a single sheet
- pr—Formats text files for printing and prints the pages with a header (date, time, filename, number of pages)
- reject—Sets a queue to reject print jobs

## Administer the X Window System

- sax2—Configures the X server
- startx—Starts the X server (log out from the graphical environment to stop the X server again)
- xinit—Starts the X server
- xvidtune—Configures the screen dimension (width, height)

## Work with MS-DOS Floppy Disks

- mcd—Changes to a directory on an MS-DOS floppy disk
- mcopy—Copies files from or to MS-DOS floppy disks
- mdel—Deletes a file on an MS-DOS floppy disk
- mdir—Displays the contents of an MS-DOS floppy disk
- mformat—Formats a floppy disk in MS-DOS format
- mlabel—Displays the name of the MS-DOS floppy disk and offers to change the name
- mmd—Creates a new directory on an MS-DOS floppy disk
- mmove—Moves a file on an MS-DOS floppy disk to another directory, or renames a file or directory on an MS-DOS floppy disk
- mrd—Deletes an empty directory from the MS-DOS floppy disk
- mren—Moves a file on an MS-DOS floppy disk to another directory or renames a file or directory on an MS-DOS floppy disk
- mtype—Displays the text file of an MS-DOS floppy disk on the screen (cf. cat)

## Use the Network

- ping—Checks network connections between two hosts
- scp—Copies files securely between two computers using SSH
- sftp—Is an interactive file transfer program, similar to FTP
- ssh—Connects and logs in to a remote machine
- ssh-add—Adds RSA or DSA identities to the authentication agent (ssh-agent)
- ssh-agent—Holds private keys used for public key authentication (RSA, DSA)
- ssh-copy-id—Installs your identity.pub in a remote machine’s authorized_keys
- ssh-keygen—Generates, manages, and converses authentication keys
- ssh-keyscan—Gathers SSH public keys
- nmblookup—Is used for NetBIOS name resolution and testing
- smbclient—Provides access to SMB file and print services

## Use vi

- ESC—Returns to normal mode

## Normal Mode

- i—Switches to insert mode so you can insert text
- dd—Copies lines. 10dd copies 10 lines
- p—Inserts copied text below or after the cursor
- v—Allows you to select text using the up, down, left, and right arrow keys
- y—Copies the highlighted text, or, if text is not highlighted, the line where the cursor is
- /searchterm—Searches the text for searchterm; jump to the next occurence of searchterm with n
- ZZ—Saves and quits

## Command-Line Mode

- :w—Writes the file to the disk
- :w filename—Writes the file to filename; you continue to edit the original file, not filename
- :e filename—Opens filename for editing
- :syntax on—Turns on syntax highlighting
- :q—Quits vi
- :wq—Quits vi, saving changes
- :q!—Quits vi, discarding changes
- :x—Saves and quits
