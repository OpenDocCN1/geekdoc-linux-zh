
Summary Table 22 describes the fields in the crontab file for scheduling jobs to run on a regular basis.

## SUMMARY TABLE 22
### THE crontab FILE

| Field | Description | Values |
|---|---|---|
| 1 | Minute | 0–59. An * in this field means every minute. |
| 2 | Hour | 0–23. An * in this field means every hour. |
| 3 | Day of month | 1–31. An * in this field means every day of the month. |
| 4 | Month | 1–12. An * in this field means every month. |
| 5 | Day of week | 0–6 (0 = Sunday). An * in this field means every day of the week. |
| 6 | Command | Enter the command to be run. |

## SCHEDULING A SINGLE SYSTEM EVENT (at)

The at command is used to schedule jobs for execution at a later time. Unlike crontab, which schedules a job to happen at regular intervals, a job submitted with at executes once, at the designated time.

## THE LP PRINT SERVICE

Many methods can be used to define a printer on a Solaris system. Summary Table 23 describes the tools Solaris provides for adding printers.

## SUMMARY TABLE 23
### SOLARIS PRINTER UTILITIES

| Utility | Description |
|---|---|
| SunSoft Print Client Software | An interface that was previously available only with the Solstice AdminSuite set of administration tools. It is now available as part of the standard Solaris distribution software and is used to set up print clients. |
| Admintool | A graphical user interface used to create, modify, and delete printers on a local system. This is the recommended way for novice users to add printers. |
| Solstice Print Manager | A graphical user Print Manager interface used to manage printers in a name service environment. Available only with the Solaris 8 server software distribution. |
| LP Print Service Commands | The command-line utilities used to set up and manage printers. These commands provide complete functionality; Admintool and the AdminSuite packages are somewhat limited for advanced tasks. |

Summary Table 24 lists the lp commands, which are the command line means for controlling printers and print queues.

## SUMMARY TABLE 24
### SOLARIS LP COMMANDS

| Command | Description |
|---|---|
| accept/reject | Enables or disables any further requests for a printer or class entering the spooling area. |
| cancel | Lets the user stop the printing of information. |
| enable/disable | Enables or disables any more output from the spooler to the printer. |
| lp | The user's print command. Places information to be printed into the spooler. |
| lpadmin | Allows the configuration of the print service. |
| lpmove | Moves print requests between destinations. |
| lpsched | Starts the print service. |
| lpshut | Stops the print service. |
| lpstat | Displays the status of the print service. |

| Utility | Description |
|---|---|
| pax | Copies files and directory subtrees to a single tape. This command provides better portability than tar or cpio, so it can be used to transport files to other types of UNIX systems. |
| ufsdump | Backs up all files in a file system. |
| ufsrestore | Restores some or all of the files archived with the ufsdump command. |

## WRITING SHELL SCRIPTS AND PROGRAMS

The Solaris 8 operating environment offers three commonly used shells:

- The Bourne shell (/sbin/sh). The default shell. It is a command programming language that executes commands read from a terminal or a file.
- The C shell (/bin/csh). A command interpreter with a C-like syntax. The C-shell provides a number of convenient features for interactive use that are not available with the Bourne shell, including filename completion, command aliasing, and history substitution.
- The Korn shell (/bin/ksh). A command programming language that executes commands read from a terminal or a file.

The login shell is the command interpreter that runs when you log in. The Solaris 8 operating environment offers the three most commonly used shells, as described in Summary Table 26.

## BACKUP AND RECOVERY

Solaris provides the utilities listed in Summary Table 25. They can be used to copy data from disk to removable media and restore it.

## SUMMARY TABLE 25
### BACKUP UTILITIES

| Utility | Description |
|---|---|
| tar | Archives data to another directory, system, or medium. |
| dd | Copies data quickly. |
| cpio | Copies data from one location to another. |

## SUMMARY TABLE 26
### BASIC FEATURES OF THE BOURNE, C, AND KORN SHELLS

| Feature | Bourne | C | Korn |
|---|---|---|---|
| Syntax compatible with sh | Yes | No | Yes |
| Job control | Yes | Yes | Yes |
| History list | No | Yes | Yes |
| Command-line editing | No | Yes | Yes |
| Aliases | No | Yes | Yes |
| Single-character abbreviation | No | Yes | Yes |
| Protect files from overwriting | No | Yes | Yes (noclobber) |
| Ignore Ctrl+D (ignoreeof) | No | Yes | Yes |
| Enhanced cd | No | Yes | Yes |
| Initialization file separate | No | Yes | Yes |
| Logout file | No | Yes | No |

| ISO/OSI Layer | Function |
|---|---|
| Data Link | Layer 2 splits data into frames for sending on the physical layer and receives acknowledgement frames. It performs error checking and retransmits frames not received correctly. |
| Network | Layer 3 manages the delivery of data via the Data Link layer and is used by the Transport layer. The most common network layer protocol is IP. |
| Transport | Layer 4 determines how to use the Network layer to provide a virtual error-free, point-to-point connection so that host A can send messages to host B, and they will arrive uncorrupted and in the correct order. |
| Session | Layer 5 uses the Transport layer to establish a connection between processes on different hosts. It handles security and creation of the session. |
| Presentation | Layer 6 performs functions such as text compression and code or format conversion to try to smooth out differences between hosts. Allows incompatible processes in the application layer to communicate via the Session layer. |
| Application | Layer 7 is concerned with the user's view of the network (that is, formatting electronic mail messages). The Presentation layer provides the Application layer with a familiar local representation of data independent of the format used on the network. |

## The Solaris Network Environment

In the ISO/OSI model, individual services that are required for communication are arranged in seven layers that build on one another. Think of the layers as steps that must be completed before you can move on to the next step and ultimately, communicate between systems. Summary Table 27 describes the function of each individual layer.

## SUMMARY TABLE 27
### NETWORK LAYERS

| ISO/OSI Layer | Function |
|---|---|
| Physical | Layer 1 describes the network hardware, including electrical and mechanical connections to the network. |

## Network Definitions

Following are network definitions:

- Packet. A packet is the basic unit of information to be transferred over the network.
- Ethernet. Ethernet is a standard that defines the physical components a machine uses to access the network and the speed at which the network runs. It includes specifications for cabling, connectors, and computer interface components.
- FDDI. Fiber Distributed Data Interface (FDDI) is a standard for data transmission on fiber-optic lines in a LAN that can extend up to 200km (124 miles). The FDDI protocol is based on the token-ring protocol.

## Network Hardware

The network hardware is the physical part of the network you can actually see. The physical components connect the systems and include the NIC, host, cabling, connectors, hubs, and routers. Following are definitions of these components:

- NIC. The computer hardware that lets you connect it to a network is known as a Network Interface Card (NIC) or network adapter.
- Hosts. If you are an experienced Solaris user, you are no doubt familiar with the term host, often used as a synonym for “computer” or “machine.” From a TCP/IP perspective, only two types of entities exist on a network: routers and hosts.
- Hubs and cabling. Ethernet cabling is run to each system from a hub. The hub does nothing more than connect all the Ethernet cables so that the computers can connect to one another. It does not boost the signal or route packets from one network to another.
- Routers. A router is a machine that forwards Ethernet packets from one network to another. In other words, the router connects LANs, and the hub connects computers.

## TCP/IP Commands

Following are TCP/IP commands:

- telnet. telnet is used to log into another system on the network.
- rlogin. rlogin is also a command for logging into another system on the network. Unlike telnet, rlogin has a mechanism whereby you don’t have to enter a login name and password if the /.rhosts and /etc/hosts.equiv files are in place.
- ftp. The File Transfer Protocol (FTP) is used to transfer one or more files between two systems on the network.
- rcp. You can also use the rcp (remote copy) command to transfer one or more files between two hosts on a network. The other system must trust your ID on the current host.
- rsh. You use the rsh (remote shell) command to execute a shell on another system on the network. The other system must trust your ID on the current system.
- rexec. The rexec command is also used to execute a shell on a remote system. This command differs from rsh in that you must enter a password. At many sites, rsh is disabled for security reasons and rexec is used as a replacement.
- finger. The finger command displays information about users logged on to the local system or other systems.
- rup. The rup command shows the host status of remote systems, similar to the uptime command.
- ping. Use the ping command to test network connectivity to a particular host.
