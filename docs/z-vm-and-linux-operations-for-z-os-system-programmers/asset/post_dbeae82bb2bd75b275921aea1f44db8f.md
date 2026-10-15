
## CP INDICATE SPACES

Use this command to display information about a user's address space and paging usage, as shown in Example 7-5.

### Example 7-5 INDicate SPaces command

```
ind spaces

Spaceid=MAINT:BASE  Owned size=123M  PRIVATE
Pages: Main=1400  Xstore=0  Dasd=0  Locked=---
Private paging:
  Xstore: Reads=0        Writes=0          Migrates=0
  Dasd:   Reads=1        Writes=1
Shared paging:
  Xstore: Reads=0        Writes=0          Migrates=0
  Dasd:   Reads=0        Writes=0
Ready; T=0.01/0.01 10:12:58
```

This commands corresponds to z/OS DISPLAY ACTIVE command.

## CP QUERY

The CP QUERY commands can display information about the system and users. We introduce several query commands that are useful when you investigate performance problems. If you have a z/OS background, you can benefit from z/OS hints related to z/VM commands.

### CP QUERY ALLOC

Use this command to display the number of cylinders or pages that are allocated, in use, and available for DASD volumes attached to the system. See Example 7-6 on page 328.

Use QUERY ALLOC PAGE for detailed information about paging space.

> Note: Do not confuse this command with the z/OS command ALLOCATE. They are very different, despite the name similarity.
> z/OS analogy: CP QUERY ALLOC command corresponds to z/OS command D ASM.

### Example 7-6 Query ALLOC command

```
q alloc
DASD 1A20 LX6RES 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000020 INUSE=0000000001 AVAIL=0000000019, ACTIVE
DASD 1A21 LX6SPL 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000338 INUSE=0000000803 AVAIL=00000002535
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
DASD 1A22 LX6PAG 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000338 INUSE=0000000000 AVAIL=0000000338
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
DASD 1A23 LX6W01 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
DASD 1A24 LX6W02 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
......
IPL NUCLES ACTIVE ON VOLUME LX6RES
Ready; T=01.01 01:16:51
```

### CP QUERY CHPIDS

Use this command to display all of the machine’s 256 channel paths and their physical status. I/O performance problems can occur if CHPIDs are offline or not available. See Example 7-7 on page 329.

### Example 7-7 Query CHPIDS command

```
q chpids
 0 1 2 3 4 5 6 7 8 9 A B C D E F
0x + + + + + + + + + + + + + + +
1x + + + + + + + + + + + + + + +
2x . . . . . . . . . . . . . . .
3x - + . . . . . . . + + + + . .
4x + + + + + + + + + + + + + +
5x + + + + + + + + + + + + +
6x + + + + + + + + + + + + + +
7x + + + + + + + + + + + . . . +
8x . . . . . . . . . . . . . . .
9x . . . . . . . . . . . . . . .
Ax . . . + . . . + . . . . . . .
Bx . . . . . . . . . . . . . . .
Cx . . . . . . . . . . . . . . .
Dx . . . . . . . . . . . . . . .
Ex . . . . . . . . . . . . . . .
Fx + + + + + + + + + + + + + + +
```

+ Available
- Offline
. Not configured
Ready; T=0.01/0.01 10:18:45

> z/OS analogy: This command acts like the z/OS D M=CHP command. Both commands display the machine's channel paths and their physical status.

### CP QUERY CPLOAD

Use this command to display information regarding the last CP IPL. The information displayed includes the location of the CP module that was last used, the location of the parm disk, and how CP was started.

### Example 7-8 Query CPLOAD command

```
q cpload
Module CPLOAD was loaded from minidisk on volume LX6RES at cylinder 39.
Parm disk number 1 is on volume LX6RES, cylinders 39 through 158.
Last start was a system IPL.
Ready; T=0.01/0.01 10:21:13
```

> z/OS analogy: This command is similar to the D IPLINFO command on z/OS.
