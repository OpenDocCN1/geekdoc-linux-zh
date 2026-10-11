
A short name for file /var/lib/crontab, which contains a list of Linux commands to be performed at specific times. The fact that the commands are timed means that they occur chronologically, thus the name crontab.

A program that runs in the background, usually performing some essential service. Web servers and FTP servers often run as daemons.

A disk portioning utility used with Linux.

An e-mail client for Linux.

The native filesystem for Linux that offers long filenames, permissions, error tolerance, and high throughput.

A shell command that will take a process and run it in the foreground.

File Transfer Protocol, which enables a user to transfer files electronically from remote computers back to the user’s computer.

Graphics Image Manipulation Program. A graphics program much like Adobe Photoshop.

GNU Network Object Model Environment. A GUI for Linux.

GNU is not Unix.

The most recent boot loader for Linux.

Linux abbreviation for get regular expression. A grep tool lets you search through a set of text files for a pattern. The item you are looking for is a regular expression.

Graphical user interface. There are a number of GUIs available for Linux. The most popular are KDE and GNOME.

A boot initiated by hardware. An example would be pressing the power switch.

A shell command that will list commands the user has previously entered.

The first process to run after the system boots and always has a process ID of 1. It is responsible for starting the system in single-user mode or spawning a shell to read the startup files, and for opening ports that are designated as login ports. init also spawns getty processes for each one.

K Desktop Environment. A commonly used GUI for Linux.

**kernel**
The core of an operating system.

**LAN**
Local area network.

**Lilo**
A commonly used boot loader for Linux.

**mbr**
Master boot record, which is the first sector of the disk; this is the sector that the BIOS reads in and starts when the machine is first booted.

**mkdir**
This makes a new directory.

**mv**
Moves or renames files or directories.

**Mozilla**
A very commonly used Web browser for Linux.

**Open Office**
An office suite complete with word processor, presentation tools, and spreadsheet tool. It is available as a free download.

**shell**
A command-line interface where you type in commands. There are a number of shells available, including the Bourne shell, Bourne-again shell (bash), Korn shell, and C shell.

**tar**
A file compression and decompression utility.

## Appendix C: Answers to Review Questions

### Chapter 1

- 1. What operating system are both Minix and Linux based on?
- 2. What does GNU stand for?
- 3. Who invented Linux?
- 4. List two advantages of Linux over Windows.
- 5. List two advantages of Windows over Linux.
- 6. What filesystem does Linux use by default?
- 7. What filesystem does Windows XP use by default?

### Answers

- 1. Unix
- 2. GNU is not Unix.
- 3. Linus Torvalds
- 4. Stability and price.
- 5. Availability of software and availability of technical support.
- 6. ext2
- 7. NTFS

### Chapter 2

- 1. What are the four options for selecting packages?
- 2. If your PC has two NICs, what would the second one be named, when you look at firewall or network configuration?
- 3. What is Disk Druid?
- 4. What is the minimum size for your SWAP partition?
- 5. What is the maximum size for your SWAP partition?
- 6. What is GRUB?
- 7. What is LILO?
- 8. What is a NIC?
- 9. What is RAM?

### Answers

- 1. Personal Deskstop, Workstation, Server, Custom
- 2. eth1
- 3. A disk partitioning utility.
- 4. The same as the size of your memory.
- 5. Two and one half times the size of your memory.
- 6. Grand Unified Boot Loader, a boot loader for Linux.
- 7. Linux Load—an older boot later for Linux.
- 8. A network interface card.
- 9. Random access memory.

### Chapter 3

- 1. What does the man command do? 
- 2. What is the shell command to delete a directory? 
- 3. What is the default shell used by Linux? 
- 4. What is the Linux command to delete a file? 
- 5. What is found in KDE under Extras? 
- 6. What is the Linux equivalent of the Windows Recycle Bin? 
- 7. The File Manager in Linux operates much like what other type of application? 
- 8. What is the Linux command to view all the files in a directory?

### Answers

- 1. It brings up a manual page for a specific command. 
- 2. rm -r (with strikethrough 'rm') 
- 3. bash (Bourne-again shell) 
- 4. rm 
- 5. Additional items for the other major categories. 
- 6. Trash Bin 
- 7. Windows Explorer 
- 8. ls

![](img/12d790664598bbf390261087fbe55bbc_456_0.png)

### Chapter 4

- 1. What are the three most common means of Internet connection?  
- 2. How many different desktops does KDE provide, by default?  
- 3. Under desktop settings, what does the common background setting do?  
- 4. What is the rule of thumb for changing hardware settings?  
- 5. What is the default browser for KDE?  
- 6. What drop-down menu do you select in Mozilla to set up your Internet connection settings?  
- 7. What is the default e-mail client for KDE?  
- 8. Favorites in Internet Explorer are called what in Mozilla?

![](img/12d790664598bbf390261087fbe55bbc_457_0.png)

### Answers

- 1. Modem, Ethernet, and cable/DSL  
- 2. Four  
- 3. It forces all the various desktops to use the same background.  
- 4. If you do not know what it is, do not touch it!  
- 5. Mozilla  
- 6. Edit  
- 7. Evolution  
- 8. Bookmarks

### Chapter 5

- 1. What is the biggest difference between Kate and KWrite?
- 2. Kate is most like what Windows application?
- 3. Which offers more graphics functionality, Windows Paint or Image Magick?
- 4. Do you use the Print Screen button to do screen captures in KDE?
- 5. What are sticky keys?
- 6. What are bounce keys?

![](img/12d790664598bbf390261087fbe55bbc_458_0.png)

### Answers

- 1. KWrite has a spell checker.
- 2. Notepad
- 3. Image Magick
- 4. No, you must use the screen capture utility.
- 5. Sticky keys cause the machine to remember any key press for a few seconds and to put it with the subsequent key press if the combination creates a command the software recognizes.
- 6. With bounce keys turned on, the software will ignore the second press of the same key if it occurs in less than a specified number of seconds.

### Chapter 6

- 1. What is a daemon?
- 2. What daemon is responsible for scheduling tasks?
- 3. Why is your birth date not a good password?
- 4. What protocol is used for sending e-mail?
- 5. What protocol is used for receiving e-mail?
- 6. What KDE utility would you use to find out how much memory is being used by your system?
- 7. What is the purpose of the KDE control center?

### Answers

- 1. A program that runs in the background. In Windows, this is called a service.
- 2. crond
- 3. It would be too easy for someone to guess.
- 4. SMTP (Simple Mail Transfer Protocol)
- 5. POP3 (Post Office Protocol)
- 6. The System Monitor
- 7. To provide a single, convenient location from which to accomplish many common administration tasks.

### Chapter 7

- 1. Which Linux word processor has an interface most like Microsoft Word?
- 2. What file types can GNumeric Worksheet import?
- 3. Which graphics program is ideal for cataloging images?
- 4. What does GNOME stand for?
- 5. When was GNOME 1.0 released?
- 6. Can GNOME run on non-Linux machines?
- 7. GNOME's equivalent of Microsoft Paint is called what?

![](img/12d790664598bbf390261087fbe55bbc_460_0.png)

### Answers

- 1. AbiWord
- 2. Microsoft Excel, Quatro Pro, and Lotus 1-2-3
- 3. gThumb
- 4. GNU Network Object Model Environment
- 5. March 1999
- 6. Yes, GNOME can run on any Unix-like system that uses GTK.
- 7. GPaint
