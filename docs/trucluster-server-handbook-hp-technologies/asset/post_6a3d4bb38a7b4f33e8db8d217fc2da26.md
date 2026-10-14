
- Verifies that the member to be rolled is in single-user mode, is not the lead cluster member, and has not been rolled yet.
- Backs up all the member-specific files for the member to be rolled.
- Sets up `it(8)` scripts that will be executed on reboot. These `it` scripts actually perform the installation and update of the new software.

The resulting output of the `clu_upgrade roll` command very much mirrors what was done during the Install Stage. If a version update was performed, then the output from the `clu_upgrade roll` will look a great deal like the output from the installupdate command. The same will be true for the installation of a Patch Kit.

Now let’s show you what really happens during the Roll Stage:

First we need to shut down this cluster member to upgrade the system firmware. Again, please review the Warning in section 25.5.1.3.

```
# shutdown -ha now

Halting processes ...
```

Next we need to boot the system into single-user mode. As soon as this is done, we use `checkcrc` to check and mount all the file systems and the “lmf reset” command to reset all the License PAKs to make them active.

```
P0>>> boot -fl 0

INIT: SINGLE-USER MODE
#
```

```
# /sbin/checkcrc
```

```
# lmf reset
Combine OSF-USR ALS-NQ-2000NQ03-99 with OSF-USR UNIX-SERVER-TEMPLATE-USER
```

Now let’s start the roll or upgrade of this cluster member. Please note that one of the first tasks performed is backing up the member-specific files.

### 25.5.6.1 Rolling a Cluster Member after the installupdate Program

The output from rolling a cluster member after a version update installation will probably look very familiar. It should, as this is basically what occurred during the installupdate with a few differences at the end. For the sake of not being too redundant, we will note only the differences in this example.

```
# clu_upgrade roll
This is the cluster upgrade program.
You have indicated that you want to perform the 'roll' stage of the upgrade.
Do you want to continue to upgrade the cluster? [yes]:yes
```

```
Backing up member-specific data for member: 2
*** START UPDATE INSTALLATION (Thu Nov 8 13:39:22 PST 2001)***
Checking for installed supplemental hardware support...
Completed check for installed supplemental hardware support
Checking for retired hardware done.
Initializing new version information (OSF)...done
Initializing new version information (TCR)...done
Initializing the list of member specific files for member2...done
Update Installation has detected the following update installable products on your system:
Tru64 UNIX V5.1A-4 Operating System (Rev 1278)
Tru64 UNIX TruCluster(TM) Server Software V5.1A-4 (Rev 619)

These products will be updated to the following versions:
Tru64 UNIX V5.1A Operating System (Rev 1885)
Tru64 UNIX TruCluster(TM) Server Software V5.1A (Rev 1312)

It is recommended that you update your system firmware and perform a complete system backup before proceeding. A log of this update installation can be found at /var/adm/smlogs/update.log.
Do you want to continue the Update Installation? (y/n) [ ]: y
```

```
Do you want to select optional kernel components? (y/n) [n]: y
```

```
Do you want to archive obsolete files? (y/n) [n]: n
```

```
FLAGS:
*** Checking for conflicting software ***
The following software may require reinstallation after the Update Installation is completed:
COMPAQ C++ Version 6.3 for COMPAQ UNIX Systems
DEC C++ Class Libraries Version 4.0 for Tru64 UNIX
DECevent
Development Enhancement Tools for Tru64 UNIX
Do you want to continue the Update Installation? (y/n) [y]: y
```

```
*** Determining installed Operating System software ***
*** Determining installed Tru64 UNIX TruCluster(TM) Server Software X5.1A-4 (Rev 619) software ***
Working...
*** Determining kernel components ***
*** KERNEL OPTION SELECTION ***
```

```
Selection   Kernel Option
---------------------------------------------
 1          System V Devices
 2          NTP V3 Kernel Phase Lock Loop (NTP_TIME)
 3          Kernel Breakpoint Debugger (KDEBUG)
 4          Packetfilter driver (PACKETFILTER)
 5          IP-in-IP Tunneling (IPTUNNEL)
 6          IP Version 6 (IPV6)
 7          Point-to-Point Protocol (PPP)
 8          STREAMS pack module (PACKT)
 9          Data Link Bridge (DPLI V2.0 Service Class 1)
10          X/Open Transport Interface (XTIOS, TIMOD, TIRDWR)
11          Digital Versatile Disk File System (DVDFS)
12          ISO 9660 Compact Disc File System (CDFS)
13          Audit Subsystem
14          All of the above
15          None of the above
16          Help
17          Display all options again
---------------------------------------------
Choices (for example, 1 2 4~6): 1 2 3 4 8 11 12 13
```

```
You selected the following kernel options:
        System V Devices
        NTP V3 Kernel Phase Lock Loop (NTP_TIME)
        Kernel Breakpoint Debugger (KDEBUG)
        Packetfilter driver (PACKETFILTER)
        STREAMS packet module (PACKT)
        Digital Versatile Disk File System (DVDFS)
        ISO 9660 Compact Disc File System (CDFS)
        Audit Subsystem
Is that correct? (y/n) [y]: y
```

```
*** Checking for file type conflicts ***
*** Checking for obsolete files ***
*** Checking file system space ***

Update Installation is now ready to begin modifying the files necessary
to reboot the cluster member off of the new OS. Please check the
/var/adm/smlogs/update.log and /var/adm/smlogs/inst.log files for errors
after the installation is complete.

Do you want to continue the Update Installation? (y/n) [n]: y
*** Starting configuration merges for Update Install ***
```

Up to this point, it would be rather hard to differentiate this output from the output from installupdate. This next section of output is unique for the Roll Stage.

```
The critical files needed for reboot have been moved into place. The
system will now reboot with the generic kernel for Compaq Computer
Corporation Tru64 UNIX V5.1A and complete the rolling upgrade for this
member (member2).
```

## Chapter 25
