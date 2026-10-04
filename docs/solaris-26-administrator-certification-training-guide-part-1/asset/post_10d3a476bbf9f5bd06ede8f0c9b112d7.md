
## Chapter 5 Setting Up User Accounts 90
- Adding User Accounts with Admintool 92
- Deleting a User Account with Admintool 95
- Modifying a User Account with Admintool 96
- Adding a Group with Admintool 97
- Setting Up User Initialization Files 98
- Customizing User Initialization Files 98
- Directories 101

## Chapter 6 Software Package Administration 104
- Tools for Managing Software 105
- Adding and Removing Software Packages 106
  - Adding Software Packages 107
  - Removing Software Packages 108
- Listing and Verifying Installed Packages 110
- Software Patches 111
  - Installing a Patch 112
  - Removing a Patch 113
- General Guidelines 114

## Chapter 7 Administration and Configuration of the CDE 116
- The Login Manager 117
  - Starting the Login Server 118
  - Stopping the Login Server 118
  - Displaying a Login Screen on a Local Display 119
- The Session Manager 120
  - Sourcing the .dtprofile Script 121
  - Sourcing the Xsession.d Scripts 121
  - The Welcome Message 122
  - Setting Desktop Search Paths 122
  - Making Modifications to a Search Path 123
  - Gathering Available Applications 123
  - Sourcing a User .profile or .login File 123
  - Starting the ToolTalk Messaging Daemon 123
  - Loading Session Resources 124
  - Starting the Color Server 124
  - Starting the Workspace Manager 124
    - Changing the Number of Workspaces on a System-Wide Basis 125
    - Providing System-Wide Workspace Names 126
  - Starting the Session Applications 126
- Customizing the Front Panel 126
  - Customizing Workspaces 127
    - Customizing Workspace Controls 129
- The Front Panel Switch Area 129
- Adding an Application or Other Icon to a Subpanel 129
- Removing All User Customizations 130
- Actions and Data Types 130
- The Application Manager 133
- The dtksh Shell 135
- To Customize or Not to Customize 135

## Chapter 8 Writing Shell Scripts and Programs 136
- What Shell to Use? 137
- Bourne Shell Variables 138
- Built-Ins 141
- Shell Conditionals 142
- && and || 142
- if 143
- Case 145
- Repeated Action Commands 146
  - For Loop 146
  - While Loop 147
  - Until Loop 147
- Shell Functions 148

## Chapter 9 The LP Print Service 150
- The UNIX Print Service 151
- The Print Spooler 151
- The Print Daemon 152
- Setting Up the Hardware 152
  - Ethernet Connection 153
  - Parallel Connection 153
  - Serial Connection 153
- Setting Up the Software 153
- BSD Versus SVR4 Printing Software 154
- BSD Print Service 154
- SystemV Print Service 155
- Print Server Versus Print Client 155
- Configuring Software for a Solaris Printer 157
- Using a Printer Not Listed in the Printer Types Menu 161
- Administering Printers 162
  - Deleting Printers and Printer Access 162
  - Checking Printer Status 163
  - Restarting the Print Scheduler 164
  - Setting a User's Default Printer 165
  - Modifying the Printer with Admintool 165

## Chapter 10 Process Control 168
- Viewing a Process 169
- Signals 172
- Scheduling Processes 175
  - Scheduling Priorities 175
  - Changing the Priority of a Time-Sharing Process with nice 176
  - Changing the Scheduling Priority of Processes with priocntl 177
- Solaris Batch-Processing Facility 178
  - crontab 178
    - How to Create or Edit a crontab File 179
    - Controlling Access to crontab 180
  - Scheduling a Single System Event (at) 180

## Chapter 11 Backup and Recovery 184
- Solaris Backup and Restore Utilities 185
  - tar 183
  - dd 187
  - cpio 188
    - Backing Up Files with Copy-Out Mode 189
    - Restoring Files with Copy-In Mode 190
    - Pass-Mode 190
  - pax 191
  - ufsdump 193
  - Restoring a File System with ufsrestore 198
    - Additional Notes About Restoring Files 201

## Chapter 12 Device Administration 204
- Hardware Terminology 205
  - Ports 205
  - Terminals 205
  - Modems 206
  - Cabling 206
- Software Terminology 206
  - Service Access Controller (SAC) 207
  - Port Monitors 207
    - ttymon 208
    - listen 208
    - Port Monitor Tag (pmtag) 208
    - Service Tag (svtag) 209
  - Administering Terminals, Modems, and Ports 209
    - Adding a Modem Through the Admintool 209
  - Service Access Facility (SAF) 213
    - sacadm 214
    - pmadm 215
- ttyadm 217
- nlsadmin 219
- Setting Up Modems and Terminals by Using SAF 219
- Using the Modem 220
- Adding a Terminal Through the Admintool 222

## Chapter 13 Networking 224
Network Fundamentals 225
Network Topologies 225
LAN 225
WAN 225
Network Protocols 226
Packet 226
TCP/IP 226
Ethernet 226
FDDI 227
ISDN 227
Network Hardware 228
NIC 228
Host 228
Hub 229
Router 229
Planning the Network 229
Setting Up the Network 229
/etc/hostname.interface 230
/etc/nodename 230
/etc/defaultdomain 230
/etc/inet/hosts 230
Network Security Files 232
IP Addressing 232
Name Service 233
TCP/IP Commands 234
telnet 234
rlogin 234
ftp 234
rcp 235
rsh 235
rexec 235
rwho 235
finger 236
Network Maintenance 236

## Appendix A The History of UNIX 238
How It All Began 239
1965–1969 239
1970 240
1970–1972 240
1973–1979 240
1982–1983 241
1984–1987 242
1988–1992 242
1993 243
Late 1990s 244
Solaris 244
Milestones in the Development of UNIX 244
## Appendix B The Fundamentals of Client-Server Computing 246
The First UNIX Server 247
An OS Designed for Speed 247
The Birth of the Workstation 247
Distributed Computing 248
UNIX Administration in a Mainframe Environment 249
## Appendix C Overview of SCSI Devices 250
## Appendix D On the Web 254
Mailing Lists 255
Newsgroups 255
Web Sites 256
UNIX-Related Publications Available on the Web 257
Index 258

## Chapter 1 Booting the Workstation

![](img/85737305a4c9aeecbcadd9986d604c02_21_0.png)

The following are the test objectives for this chapter:
- Booting the system
- Using OpenBoot PROM commands to record basic system configuration information
- Using OpenBoot PROM commands to alter the system boot device
- Using OpenBoot PROM commands to perform basic hardware testing
- Booting a system from more than one device
- System run states and startup scripts
- System shutdown

Bootstrapping is the process the computer follows to load and execute the bootable operating system. The name is coined from the phrase "pulling yourself up by your own bootstraps." The instructions for the bootstrap procedure are stored in the boot PROM (programmable read-only memory).

The boot process goes through the following phases:
1. **Boot PROM Phase.** The PROM displays system identification information and runs self-test diagnostics to verify the system's hardware and memory. Then the PROM loads the primary boot program, called bootblk.
2. **Boot Programs Phase.** The bootblk program finds and executes the secondary boot program (called ufsboot) from the ufs file system and loads it into memory. After the ufsboot program is loaded, it loads the kernel.
3. **Kernel Initialization Phase.** The kernel initializes itself and begins loading modules, using ufsboot to read the files. When the kernel has loaded enough modules to mount the root file system, it unmaps the ufsboot program and continues, using its own resources. The kernel starts the UNIX operating system, mounts the necessary file systems, and runs `/sbin/init` to bring the system to the "initdefault" state specified in `/etc/inittab`.
4. **Init Phase.** The kernel creates a user process and starts the `/sbin/init` process, which starts other processes by reading the `/etc/inittab` file.

The `/sbin/init` process starts the run control (rc) scripts, which execute a series of other scripts. These scripts (`/sbin/rc*`) check and mount file systems, start various processes, and perform system maintenance tasks.

## Boot PROM and Program Phases

The bootstrap process begins after power-up when information located in the hardware's PROM chip is accessed. Sun calls this the OpenBoot firmware, and it is executed immediately after you turn on your system. The primary task of the OpenBoot firmware is to boot the operating system either from a mass storage device or from a network.

OpenBoot contains a program called the monitor, which controls the operation of the system before the kernel is available. When a system is turned on, the monitor runs a quick self-test that checks such things as the hardware and memory on the system. If no errors are found, the system begins the automatic boot process. OpenBoot contains a set of instructions that locate and start up the system's boot program and eventually start up the UNIX operating system. The boot program is stored in a predictable area on the system hard drive, CD-ROM, or other bootable device and is referred to as the bootblock. The bootblock is
