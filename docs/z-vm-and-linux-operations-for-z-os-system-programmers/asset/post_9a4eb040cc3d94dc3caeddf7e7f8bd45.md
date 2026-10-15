
## 2.8.1 CP

Interaction with CP is primarily through a command line interface. You issue commands to CP by typing them on the command line and pressing Enter to submit them for processing.

CP commands are always from 1 to 12 characters in length, and are not case-sensitive. A command often accepts parameters, all of which are separated by a space (as in most command line environments).

Many commands can be abbreviated but are more cryptic. For example, the QUERY NAMES command can be shortened to Q N. Executing either version of the command accomplishes the same task.

This chapter always uses the complete command and not the abbreviation. If you want to know the abbreviation for a command, refer to the help command or to CP Commands and Utilities Reference, SC24-6073.

## Getting to CP mode

After logging in, any number of things could be going on, depending on the guest operating system your virtual machine is running. Because we are only interested in CP at this point, in our scenario we are going to shut down the guest operating system that is running and get into CP mode so we can issue commands directly to CP.

Your virtual machine is likely to be running the CMS operating system. To determine if you are running CMS, look at the output you get when you log on. If the output is similar to Example 2-10, you are running CMS. The last line (starting with z/VM V5.3.0) is the first line of output from CMS.

Example 2-10 Output seen when running CMS at logon

```
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: 0001 RDR,  NO PRT,  NO PUN
LOGON AT 09:54:43 EDT MONDAY 06/04/07
z/VM V5.3.0    2007-05-02 16:25
```

If no output appears, you might still be running CMS. Enter the QUERY CMSLEVEL command to check further. If the output is similar to Example 2-11 on page 67, then you are running CMS.

## Example 2-11 Output from QUERY CMSLEVEL command

```
QUERY CMSLEVEL
CMS Level 23, Service Level 701
Ready; T=0.01/0.01 09:57:17
```

Important: To stop CMS and enter CP mode, issue the #CP SYSTEM CLEAR command. Note, however, that if you are not running CMS, this command can work, but it could damage your guest operating system. Issuing a SYSTEM CLEAR command is the equivalent of pulling your desktop personal computer's power cord out of the wall socket. It halts the system immediately and does not give the operating system a chance to finish what it is doing and perform cleanup tasks. If the operating system is engaged in writing a file when this happens, you could lose the contents of the file or even permanently corrupt the file system.

Therefore, if you are not running CMS, consult your guest operating system's manual for proper shutdown instructions.

z/OS analogy: For z/OS users this is like doing a SYSTEM RESET on the HMC for your LPAR

## Example 2-12 Output from #CP SYSTEM CLEAR command

```
#CP SYSTEM CLEAR
Storage cleared - system reset.
```

This command clears your virtual machine's memory, and stops and resets all of its virtual processors.

If you are truly in CP mode and not running a guest operating system, you should be able to issue the BEGIN command and see the output displayed in Example 2-13.

## Example 2-13 Output of BEGIN command when not running a guest operating system

```
BEGIN
HCPGIR453W CP entered; program interrupt loop
```

If different content is displayed, chances are you are still running a guest operating system.

## Examining your virtual machine

CP has many commands that involve getting information about your virtual machine and defining its virtual hardware configuration. In this section, we examine the commands for obtaining information about your virtual machine.

First, we discuss the QUERY command, which provides useful information about your virtual machine and the system on which it is running. The command accepts several arguments, most of which have sub-arguments of their own. We will only look at a subset of the capabilities of the query command.

z/OS analogy: Query is similar to the various DISPLAY commands in z/OS

### CP version

The QUERY CPLEVEL command indicates which version of CP you are running. You run this command when you log on to your virtual machine. Version is commonly referred to as level in z/VM terminology. See Example 2-14.

z/OS analogy: For z/OS, the similar information is displayed when system command D IPLINFO is issued. It can also be displayed from variables in TSO and ISPF.

Example 2-14 Output from QUERY CPLEVEL command

```
QUERY CPLEVEL
z/VM Version 5 Release 3.0, service level 0701 (64-bit)
Generated at 05/02/07 16:28:04 EDT
IPL at 05/03/07 13:06:26 EDT
```

### Your guest name

If you just logged in, you probably know what your guest name is (a guest name is the uniquely identifying name given to your virtual machine). But, if you have more than one terminal open at the same time and forget which terminal goes with which guest, you can use the CP command QUERY USERID to determine the guest name; see Example 2-15.

z/OS analogy: In z/OS (when logged into ISPF), your user ID is normally displayed in the primary option panel

Example 2-15 Output from the QUERY USERID command

```
QUERY USERID
TUX1 AT VMLINUX6
```
