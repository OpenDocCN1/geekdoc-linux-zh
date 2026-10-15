

```
PROFILE IBMDFLT
SPOOL 000C 2540 READER **
SPOOL 000D 2540 PUNCH A
SPOOL 000E 1403 A
CONSOLE 009 3215 T
USER MAINT 0190 0190 RR
LINK MAINT 019D 019D RR
```

Figure 6-3 Sample MYDIR DOCUMENT

By issuing the following command, the response from DIRECTXA is shown in Figure 6-4.

```
DIRECTXA MYDIR DOCUMENT * (EDIT
```

```
z/VM USER DIRECTORY CREATION PROGRAM – VERSION 5 RELEASE 3.0
USER MAINT 0190 0190 RR
HCPDIR751E INVALID OPERAND – USER FOLLOWING PROFILE IBMDFLT
HCPDIR775E PROFILE DEFINITION IBMDFLT IS INVALID AND WILL NOT BE PROCESSED FOR ANY USER DEFINITIONS THAT INCLUDE IT.
EOJ DIRECTORY NOT UPDATED
```

Figure 6-4 Response from DIRECTXA

We now define the new user, with a user ID of TOSK, and define a corresponding 191 minidisk as shown in the USER DIRECT file in Figure 6-5.

```
01967 ******************************
01968 USER TOSK TOSK 32M 64M G
01969 INCLUDE IBMDFLT
01970 ACCOUNT ACT4 CMSTST
01971 MACH XA
01972 IPL 190
01973 MDISK 191 3390 2380 010 LX6W02 MR READ WRITE MULTIPLE
```

Figure 6-5 Statements to define user TOSK

The line numbers in the file (in Figure 6-5) indicate the following statements:

- Line 01968 Statement USER initiates the statements for the user. The first occurrence of TOSK is the user ID, the second is password. The 32M is the initial amount of storage defined to this user, 64M is the maximum amount of storage. The G is the privilege class (or classes) assigned to the user, in this example only a general user.
- Line 01969 Includes what is known or defined as a PROFILE in USER DIRECT, and should be seen as statements that are common for several users.
- Line 01970 Assigns an account code for the user.
- Line 01971 Sets the architecture for user TOSK.
- Line 01972 States that this user should be IPLed from 190, which corresponds to CMS.
- Line 01973 Assigns the minidisk 191 on a 3390 device; starting at cylinder 2380 for 10 cylinders on volume LX6W02 in multiple read, establishes passwords for READ (only), WRITE and MULTIPLE READ, respectively. These are used when other users access TOSK's 191.

Invoking the following command gives the response shown in Figure 6-6:

```
DIRECTXA USER DIRECT (EDIT
```

```
Ready: T=0.01/0.01 15:28:21
DIRECTXA USER DIRECT (EDIT
z/VM USER DIRECTORY CREATION PROGRAM – VERSION 5 RELEASE 3.0
EOJ DIRECTORY NOT UPDATED
Ready: T=0.01/0.01 15:28:33
```

Figure 6-6 Response from DIRECTXA without errors

To check for disk gaps or overlaps, issue the following command; the response is in Figure 6-7:

```
DISKMAP USER DIRECT (DOENDS
```

```
DISKMAP USER DIRECT (DOENDS
File USER DISKMAP A has been created.
Ready: T=0.04/0.04 15:39:12
```

Figure 6-7 DISKMAP response

Browsing the USER DISKMAP file shows no gaps or overlaps within this disk's extents, with the exception of MAINT, which is overlapping the same extent. This is because MAINT has this disk (and several others) defined as a minidisk from cylinder 0 to END. This is a normal way of defining CP-owned disks.

Issue the following command to compile the updated source to an object and bring it online to z/VM. User ID TOSK can now log on.

```
DIRECTXA USER DIRECT
```

## 6.3 Networking access

This section describes how to give network access to your guest operating systems. We discuss how you define that access for LANs and VSWITCHes.

### DEFINE LAN command

Use this command to create a guest LAN that can be shared among virtual machines on the same VM system. Each guest LAN is identified by a unique combination of owner ID and LAN name. A VM user can create a simulated network interface card (NIC) and connect it to this LAN segment.

> Note: The SET LAN command can modify attributes of the guest LAN.

You can also define a LAN during system initialization using the DEFINE LAN configuration file statement. The class B form of the command allows the invoker to create a LAN for another user (for example, OWNERID SYSTEM) and specify whether accounting is on or off for the LAN being defined.

### DEFINE VSWITCH command

Use this command to create a CP system-owned switch (a virtual switch) to which virtual machines can connect. Each switch is identified by a switch name. A z/VM user can create a simulated QDIO network interface card (NIC) and connect it to this switch with the NICDEF directory statement. Under the DEFINE VSWITCH statement, the VLAN parameter is important, but optional, if you want to isolate guest subnets based on VLAN IDs.

## 6.4 Linux on System z resource management

This section discusses the necessary steps to dynamically add new resources, such as disks, network interface cards, and CPUs, to a Linux guest.

Explaining the details of Linux on System z hardware detection and configuration is beyond the scope of this book. Nevertheless, providing a brief outline of the processes involved is necessary to help you understand the next section.

### 6.4.1 Hardware detection and configuration

This section discusses device drivers and the in-memory file system.

