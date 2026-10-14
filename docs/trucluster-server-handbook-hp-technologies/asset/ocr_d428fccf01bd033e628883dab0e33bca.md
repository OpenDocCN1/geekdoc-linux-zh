```
HSG80> show d100
LUN                Uses                 Used by
------------------------------------------------------------
D100               DISK30100
LUN ID:            6000-1FE1-000B-1A40-0009-0361-3888-0062
WORLDWIDE IDENTIFIER
Switches:
RUN                NOWRITE_PROTECT      READ_CACHE
READAHEAD_CACHE    WRITEBACK_CACHE
MAX_READ_CACHED_TRANSFER_SIZE = 32
MAX_WRITE_CACHED_TRANSFER_SIZE = 32
Access:
ALL
State:
ONLINE to this controller
Persistent reserved
MOREPREFERRED_PATH
Size:              17769177 blocks
Geometry (C/H/S): ( 5258 / 20 / 169 )
```

Did you notice the "Persistent reserved" under "State"? That tells us that unit D100 has a PR. Let’s continue to track this particular unit down and see who set the PR. We happen to know that unit D100 on the HSG80 is dsk108 on our cluster (if we didn’t know this, we could track it down based on the WWID).

```
# hwmgr -show scsi -full | grep -E "dak|6000-1fe1-000b-1a40-0009-0361-3888-0062*"
272: 22    skipper   disk   none   2   4   dsk105 [5/1/105]
274: 18    skipper   disk   none   2   8   dsk106 [5/1/62]
563: 11    skipper   disk   none   0   8   dsk108 [5/1/100]
        WWID:01000010:6000-1fe1-000b-1a40-0009-0361-3888-0062
64:  0     skipper   disk   none   2   1   dsk9  [0/0/0]
67:  3     skipper   disk   none   2   4   dsk1  [5/1/1]
68:  4     skipper   disk   none   2   4   dsk2  [5/1/2]
69:  5     skipper   disk   none   0   5   dsk3  [5/2/3]
74:  8     skipper   disk   none   0   4   dsk15 [5/1/9]
75:  9     skipper   disk   none   0   4   dsk8  [5/1/8]
151: 23    skipper   disk   none   2   4   dsk20 [5/1/20]
```

```
# hwmgr -show scsi -full -id 563 | more
SCSI  DEVICEID HOSTNAME DEVICE DEVICE SUBTYPE OWNER PATH NUM DEVICE FIRST VALID PATH
HWID: DEVICEID          TYPE   SUBTYPE      PATH FILE
------------------------------------------------------------
563: 18    gilligan   disk   none   0   8   dsk108 [5/1/100]
        WWID:01000010:6000-1fe1-000b-1a40-0009-0361-3888-0062
BUS   TARGET LUN   PATH STATE
-----------------------------
5     1      100   valid
5     2      100   valid
5     3      100   valid
5     4      100   valid
```