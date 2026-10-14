
## /etc/sudoers
Configuration file that determines what actions regular users are permitted to perform using the `sudo` command. Must be edited using the `visudo` command.

## /proc file system
A collection of information about the Linux kernel and other system resources that you access as a file system.

## $@
A special shell variable that includes all of the parameters on the command line.

## .bashrc
A configuration script that is executed each time the user starts a bash shell.

## .exrc
A configuration file for vi, which can be stored in any directory. Any vi settings stored in this file are applied when vi is used to edit any text file in the same directory.

## .forward
Configuration file placed in a user's home directory to define where e-mail messages should be forwarded by sendmail.

## .profile
A configuration script that can be located in each user's home directory. A script that is executed each time any user on the system starts a bash shell. This script is not included by default on all Linux distributions, but can be created if needed.

## .hosts
A file stored within a user's home directory to determine who is allowed to access that user's account via r-utilities commands such as `rsh` and `rlogin`. See also `/etc/hosts.equiv`.

## .Xauthority
Configuration file containing tokens (cookies) used by the `xauth` program to enable remote display of graphical programs.

## absolute path
A complete description of how to access a desired subdirectory or file, specified from the root of the file system to the subdirectory or file. It must begin with a forward slash. See also relative path.

## action
A field in the syslog.conf configuration file that determines what to do with messages matching the selector on that line.

## active partition
The bootable partition; the partition that the MBR passes control to if the MBR does not itself contain a boot manager.

## Address Resolution Protocol (ARP)
A protocol that broadcasts a message to an entire network segment in order to obtain a host's MAC address, or, if the MAC address is known, to obtain a host's IP address.

## alias
A string of characters that the shell substitutes for another string of characters when a command is entered. Created in the shell using the `alias` command.

## alternatives printing system
A method used in Red Hat Linux and Fedora to permit both LPRng and CUPS printing systems to reside on the same Linux system using symbolic links for commonly used printing commands.

## Apache
A popular Web server program.

## Apache modules
Program code that can be loaded independently into the Apache Web server.

## application
A program (such as a word processor or spreadsheet) that provides a service to a person using the computer, rather than simply managing the computer's resources.

## ARP cache
A list of IP address-to-hardware mappings maintained by the ARP protocol to assist in routing packets. Viewed using the `arp` command.

## background application
An application that does not prevent the program that started it from immediately interacting further with the user.

## backup
A copy of data on a computer system.

## backup level
A description of how much data is stored in a backup operation. A backup level is only relevant in comparison with another backup level. When performing a backup operation at a given level, all of the data that has changed since the last backup of the previous level is recorded.

## backup media
A device on which data can be stored, such as a tape cartridge, writeable CD or DVD, or floppy disk.

## backup plan
A written document that outlines when, how, and why various files and file systems are backed up, stored, and—when necessary—restored to prevent permanent data loss.

## bang
In Linux jargon, an exclamation point character.

## bash
Short for Bourne Again shell, an enhanced and extended version of the Bourne shell created by the GNU project for use on many UNIX-like operating systems; bash is the default Linux shell.

## binary file
See executable file.

## binary code
Machine-readable instructions used to execute a program.

## BIOS (Basic Input/Output System)
Information stored in ROM that provides instructions to the operating system for using the devices on a computer.

## bit
A binary digit; a bit can hold a value of either one or zero.

## block
A unit of hard disk space; typically one that contains 1024 bytes, or two sectors.

## bootable CD-ROM drive
A CD-ROM drive that can start an operating system (or other program) directly from a CD without accessing the hard disk. (This feature of the CD-ROM drive must be enabled by the BIOS.)

## boot disk
A removable disk that can start an operating system, especially one that starts a Linux installation program.

## boot image
A Linux kernel that can be started by a boot loader.

## boot manager
A program that lets you start one or more operating systems each time you start a computer. (Examples include GRUB and LILO.)

## boot parameter
A parameter provided to a boot loader, which is in turn passed to the Linux kernel at boot time in order to control how the kernel operates or to assist the kernel in working with hardware components.

## BOOTP
A protocol used by diskless computers to obtain configuration information. Rarely used now, but similar to DHCP, which is backward compatible with BOOTP.

## boot record
A small area on each partition that contains a program to start the operating system on that partition.

## Border Gateway Protocol (BGP)
A widely used external routing protocol.

## Bourne shell
The original shell for UNIX, written by Stephen Bourne.

## broadcast address
An IP address that a computer on a network can use to send a packet to all computers on that network.

## buffer
Memory used by an application for data storage.

## buffer overflow attack
A technique for gaining access to a computer system by exploiting a weakness in the design of a computer program. When a cracker follows a specific sequence of steps or provides specific input to a program, the program becomes confused and tries to use computer memory inappropriately; consequently, the buffer, or memory space, reserved for a part of the program overflows. The result can be either corruption of system data, a crashed server, or even direct root access.

## byte
Storage space sufficient to store one character; eight bits.

## C shell
A shell developed by Bill Joy in the 1970s. He focused on adding easy-to-use features for interactive work at the shell prompt. (Most of these features were later added to the bash shell as well.) The C shell is not popular for shell programming because its syntax is more complex than that of the Bourne, bash, and Korn shells.

## caching name server
A DNS server that contains no preconfigured information on domains (except localhost), but simply queries other DNS servers and caches the results.

## CERT Coordination Center (CERT/CC)
A federally funded software-engineering institute that focuses much attention on computer security issues and provides information to security and system administration professionals around the world; operated by Carnegie-Mellon University.

## chained boot loaders
Multiple boot loaders that refer to each other, located at different positions on one or more hard disks in a single computer, such as on the MBR, and on one or more boot records of distinct partitions.

## chief information officer (CIO)
The executive in an organization who determines how information systems are used within the organization to further its goals or mission effectively.

## child directory
A subdirectory of a parent directory.

## child process
A process that was started by another process. All processes are child processes of the init process, some further removed than others.

## client
A program or computer that is requesting information or service from another program or computer. See also server.

## CMOS RAM
A special memory chip in which computer configuration details are stored. The data is maintained by a tiny battery and is modified as needed using a BIOS utility.

## command history
A feature of the shell that records in a list (the history list) each of the commands that you enter at the shell prompt.

## command interpreter
A program that accepts input from the keyboard and uses that input to start commands or otherwise control the computer system.

## command-line interface (CLI)
A method of communicating with the operating system by entering textual commands at a prompt.

## comment
A line in a script or source code that is not processed by the interpreter or compiler, but is only included to help someone reading the file understand the purpose or operation of the script or source code. Comments in shell scripts and many other languages are created by beginning a line with the # character.

## Common Gateway Interface (CGI)
A method of communication between two programs using the standard input and standard output channels.

## Common UNIX Printing System (CUPS)
A printing system that permits browser-based configuration and print management. Intended to eventually replace the LPRng printing system.

## compiled language
A computer language for which the source code is converted to a binary file before the program is executed.

## compiler
A program that converts the source code of a compiled language into a binary file.

## computer language
A set of words and syntax rules that can be arranged in predefined ways to cause a computer to perform tasks defined by the person using the language.

## console
A text-only interface to the operating system, providing a command-line interface. Not part of a GUI.

## container
A special type of Apache configuration directive that activates other directives only if a condition is met or only within a particular context.
