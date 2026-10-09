
- /sbin/update is executed by inittab to flush dirty buffers.
- /etc/rc.d/rc*.d directories contain scripts executed by init during startup and shutdown. The most commonly used runlevels are 3 and 5. 3 is the default command-line runlevel and 5 is the default GUI runlevel.

There are seven different runlevels.

- 0 Halt
- 1 Single-user mode
- 2 Not used (user-definable)
- 3 Full multiuser mode
- 4 Not used (user-definable)
- 5 Full multiuser mode with an X-based login screen (GUI)
- 6 Reboot

Runlevels 2 through 5 have virtual consoles, accessed through the Ctrl+Alt+F1-7 key entry.

Shutting down the Linux system ensures that files are saved and file systems are unmounted. Turning off a system without shutting down can result in damaged files.

Users are identified by username and authenticated by password. Users are easily added with the useradd command, and passwords are changed with the passwd command. Users are also identified by their UID, a unique identifier with a value of 500 or greater. There are GUI tools to easily add users and groups.

Users always belong to a group. A group can have one or many users. Groups are used to ease administrative issues when dealing with file permissions.

Files in Linux are classified as sharable and unsharable, variable, and static. Sharable files are made available to multiple users, and unsharable files are made available to only one user. Variable files can be changed as needed, and static files have a constant value.

The File system Hierarchy Standard (FHS) defines common directories for Linux systems. The file system hierarchy starts with the root (/) directory and contains many common directories and other user-defined directories.

File permissions are assigned for the owner, group, and everyone else. Permissions indicate read, write, and execute privileges. In a long file listing, the 10 characters at the beginning of each file list indicate the file type and the permissions for the owner, group, and others. Permissions are assigned with the chmod command.

## SELF-TEST

1. The _______ program contains all the code required to control the keyboard, display, disk drives, and other devices attached to the computer.
   a. BIOS
   b. PnP
   c. init
   d. PnP

2. Which of the following is the correct sequence for system startup?
   a. Look for bootable media, POST, load boot loader, load kernel, execute init
   b. Look for bootable media, POST, load kernel, load boot loader, execute init
   c. POST, look for bootable media, load boot loader, load kernel, execute init
   d. POST, look for bootable media, load kernel, load boot loader, execute init

3. Which of the following is the correct startup sequence for the init process?
   a. Read /etc/inittab file, run /etc/rc.d/rc.sysinit script, start background processes
   b. Read /etc/inittab file, start background processes, run /etc/rc.d/rc.sysinit script
   c. Start background processes, run /etc/rc.d/rc.sysinit script, read /etc/rc.d/rc.sysinit file
   d. Run /etc/rc.d/rc.sysinit script, read /etc/inittab file, start background processes

4. The **configuration file** is handled by the Ctrl+Alt+Delete key sequence.
   a. /etc/inittab
   b. /etc/rc.d/rc.sysinit
   c. /etc/init
   d. /etc/lilo

5. Which runlevel provides full multi-user mode and a command-line interface?
   a. 0
   b. 1
   c. 3
   d. 5
   e. 6

6. Which configuration file contains the default runlevel information?
   a. /etc/inittab
   b. /etc/rc.d/rc.sysinit
   c. /etc/init
   d. /etc/lilo

7. Which runlevel provides full multiuser mode with an X-based login screen?
   a. 0
   b. 1
   c. 3
   d. 5
   e. 6

8. The proper command to restart the Linux operating system is ________.
   a. /sbin/reboot -r now
   b. /sbin/reboot -h now
   c. /sbin/shutdown -r now
   d. /sbin/shutdown -h now

9. Which of the following are characteristics of a strong password? (Choose three.)
   a. It is at least eight characters in length.
   b. It contains word sequences to make it easier to remember.
   c. It contains uppercase and lowercase letters.
   d. It contains special characters and numbers.
   e. It should have numbers in sequence or dates.

10. Use the ______ command to add a user.
    a. su
    b. useradd
    c. groupadd
    d. usermod
    e. passwd

11. Use the ______ command to add users to a group.
    a. su
    b. useradd
    c. groupadd
    d. usermod
    e. passwd

12. Permissions are identified by ten characters displayed on a long file listing. What is represented by the last three characters?
    a. Directory or file
    b. others
    c. group
    d. owner

13. To change permissions of file myfile to include execute for the owner, use the command ______.
    a. chmod o+x myfile
    b. chmod o+w myfile
    c. chmod u+x myfile
    d. chmod u+w myfile

14. True or False: Strong passwords should be changed every 30 to 90 days.

15. The command **chmod 754 myfile** assigns which of the following permissions?
    a. Read/write/execute for the owner, group, and others
    b. Read/write/execute for the owner, read/write for the group, and read/write for all others
    c. Read/write/execute for the owner, read/execute for the group, and read/write for all others
    d. Read/write/execute for the owner, read/execute for the group, and read only for all others

16. To remove the /home/jsmith/mydir directory, you use which of the following commands?
    a. rmkdir /home/jsmith/mydir
    b. rm /home/jsmith/mydir
    c. rm -r /home/jsmith/mydir
    d. cd /home/jsmith/mydir

17. The BIOS program is stored in _____________.
    a. RAM
    b. CMOS
    c. ROM
    d. MBR

18. True or False: After running the command **chmod 755 myfile**, myfile is assigned read, write, and execute permissions for the owner of the file.

19. What does the BIOS load into memory?
    a. RAM
    b. CMOS
    c. ROM
    d. MBR

20. Any programs that are needed by the Linux operating system during startup are started by the ____________ script.
    a. /etc/rc.d/rc.sysinit
    b. /sbin/update
    c. /etc/sysconfig
    d. /etc/rc.d/rc3.d

21. True or False: The command **usermod -G jsmith -U dbrown** adds the user dbrown to the group jsmith.

22. Which of the following statements is true concerning the file /etc/rc3.d/$S5sshd? (Choose two.)
    a. It is a startup file.
    b. It is executed in runlevel 3.
    c. It is a kill script.
    d. It is the 55th script to be executed.

23. Which runlevel is user-definable? (Choose two.)
    a. 1
    b. 2
    c. 3
    d. 4
    e. 5

24. True or False: Single-user mode is entered by making runlevel 5 the default runlevel.

25. True or False: Usernames must be a combination of the first initial and the last name of the user.

## Linux Command Line

CHAPTER 5

### CHAPTER OBJECTIVES

- Set environment variables
- Describe and use the features of the multi-user environment
- Use common shell commands and expressions
- Create, edit, and save files using vi

### USING THE COMMAND-LINE SHELL

Most, if not all, commands can be accomplished through the GUI tools. However, knowledge of the command-line interface (CLI) can make Linux administration much faster for most tasks. Some commands can be accomplished only through the command line. Using GUI tools requires mouse movements and finding commands through a maze of menus and toolbars, a cumbersome procedure for most administrators.

An experienced user can also write shell scripts. A shell script is a collection of commands stored in a file. The file is given execute permission and is used to do a wide variety of tasks. Scripts are discussed in the next chapter.

The first operating systems used a command line interpreter to interact with users. A command interpreter accepts input from a user via keyboard and translates every word, or interprets the words, and then does whatever action is called for. The first command interpreters were pretty basic and didn’t offer very many features. To provide a better way of interacting with the operating system, the shell (Figure 5–1) was developed. The first shell program was the Bourne shell (sh), developed by S. R. Bourne. Since then, other shells have been developed, including C shell (csh), the Korn shell (ksh), and the bash shell (Bourne Again Shell).

### Command Line Basics

The bash shell (see http://www.gnu.org/software/bash/bash.html) is the product of the Free Software Foundation and is used by most Linux operating systems. Several shells are typically available in Linux, but the bash shell is the default shell for users.

If you booted the system into runlevel 3, you are at a command line prompt. If you are using the X window system (GUI), you need to open a terminal window. A terminal window is a terminal emulator program that opens in a window and then runs a shell program. There are several different terminal programs: gnome-terminal, xterm, and others. Typically, within the GUI, you can right-click the screen and select terminal from the displayed pop-up menu.

A virtual terminal, discussed in Chapter 2, can also be used. Pressing Ctrl+Alt+F1 displays the first virtual terminal, Ctrl+Alt+F2 displays the second, and so on. Linux usually has six virtual terminals, and the seventh displays the GUI. The virtual terminals work with the CLI, but the GUI is still active and can be displayed by pressing Ctrl+Alt+F7. When the terminal displays the **login:** prompt, enter a valid ID and then a password to display the bash shell. The CLI prompt will be displayed. Typically, the prompt will be $,
