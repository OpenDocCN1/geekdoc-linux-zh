```
U
ICK030001 CPVOL REPORT FOR 8228 FOLLOWS:

CYLINDER ALLOCATION CURRENTLY IS AS FOLLOWS:
TYPE      START      END      TOTAL
----      ----      ----      -----
PAGE         1      3338      3338

ICK000011 FUNCTION COMPLETED, HIGHEST CONDITION CODE WAS 0
14:14:42  05/14/08

ENTER INPUT COMMAND:
END

ICK000021 ICKDSF PROCESSING COMPLETE. MAXIMUM CONDITION CODE WAS 0
Ready; T=0.06/0.15 14:14:42
```

# Registering the disks to the system

After a DASD is formatted, make sure that the system recognizes them as available storage. This information is stored in the SYSTEM CONFIG file. Being recognized as available storage is analogous to (assuming the device is defined in the HCD IOCDS) issuing a VARY xxxx ONLINE command and eventually putting that command in COMMNDxx or IEACMD00 of PARMLIB concatenation, if defined with OFFLINE attribute in z/OS (any mount usage attributes must also be considered). Linux systems do not have an equivalent step since disks are discovered in boot time by a hardware probing program and automatically appear as devices under /dev after the system finishes booting up.

Example 4-7 uses the same steps to access the MAINT CF1 disk read-write that you used earlier. It is good to remember the sequence of steps shown in Example 4-7.

# Example 4-7 Accessing the MAINT CF1 disk read-write

```
==> q cpdisk
Label Userid Vdev Mode Stat Vol-ID Rdev Type StartLoc EndLoc
MNTCF1 MAINT OCF1 A R/O 530RES 0200 CKD 39 83
MNTCF2 MAINT OCF2 B R/O 530RES 0200 CKD 84 128
MNTCF3 MAINT OCF3 C R/O 530RES 0200 CKD 129 188
==> cprel a
CPRELEASE request for disk A scheduled.
HCPZAC6730I CPRELEASE request for disk A completed.
==> link * cfl cf1 mr
==> acc cf1 f
```