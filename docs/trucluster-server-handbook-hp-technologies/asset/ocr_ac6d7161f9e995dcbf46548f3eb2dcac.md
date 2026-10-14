```
```text
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

```
```text
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

```
```text
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
```

Up to this point, it would be rather hard to differentiate this output from the output from installupdate. This next section of output is unique for the Roll Stage.

```
```text
The critical files needed for reboot have been moved into place. The
system will now reboot with the generic kernel for Compaq Computer
Corporation Tru64 UNIX V5.1A and complete the rolling upgrade for this
member (member2).
```
```

# Chapter 25