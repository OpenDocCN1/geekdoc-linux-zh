
## cleanPR show

    cleanPR Version: 1.5

Checking device 5 1 100
    Key Entry 0: 0x30001
    Key Entry 1: 0x30002
    Key Entry 1: 0x30002
    Key Entry 3: 0x30001
    Key Entry 6: 0x30001
    Key Entry 6: 0x30002
    Key Entry 6: 0x30001
    Key Entry 6: 0x30002

Total of 5 devices found w/Persistent Reservations
Total of 0 devices cleared of Persistent Reservations

You can also check the devices on your storage controller (HSG80> show <unit>) to see if they are listed as "persistent reserved" under "State" in the output.

```
HSG80> show d100

LUN                         Uses                 Used by
------------------------------------------------------------
D100
    LUN ID:        6000-1F21-000B-1A40-0009-0361-3888-0062
    NOIDENTIFIER
    Switches:
    RUN           NOWRITE_PROTECT          READ_CACHE
    READ_AHEAD_CACHE    WRITEBACK_CACHE
    MAX_READ_CACHED_TRANSFER_SIZE = 32
    MAX_WRITE_CACHED_TRANSFER_SIZE = 32
    Access:
        ALL
    State:
        ONLINE to this controller
        Persistent reserved
        NOPREFERRED_PATH
    Size:           17769177 blocks
    Geometry (C/H/S): ( 5258 / 20 / 169 )
```

If you find that indeed there are persistent reservations on your storage, you can boot the Emergency Repair Disk (which means shutting down the cluster) and use the "cleanPR clean" command to clear all the persistent reservations.

## cleanPR clean

                    cleanPR Version: 1.5

                              WARNING

          This shell script will clear all Persistent Reservations
          from the HSX80 devices attached to this system.

                              WARNING

Do you wish to proceed ? <y/n> [n] : y

          Removing Persistent Reservations from all HSX80 devices...

Checking HSG80 at /dev/rdsk/dsk108a (SCSI #5 (SCSI ID #2), (SCSI LUN #100))
Checking HSG80 at /dev/rdisk/dsk6a (SCSI #9 (SCSI ID #9), (SCSI LUN #15))

Total of 0 devices found w/Persistent Reservations
Total of 0 devices cleared of Persistent Reservations

If the “cleanPR clean” command doesn’t resolve all the PRs, you can run the scu command manually to clear them.

```
# scu

scu> set nexus bus 2 target 0 lun 3

scu> preserve clear
```

> **WARNING:**
> 
> **Never clear** persistent reservations from a cluster member! You will remove needed reservations. Always shut down the cluster and boot a standalone version of the OS, such as the Emergency Repair Disk, if you need to run the “cleanPR clean” command or if you need to use “scu” to clean them manually.

## A.1.8 Upgrading the KGPSA Firmware Causes HOST_ID Changes

After upgrading the firmware on the KGPSA host bus adapter, the HOST_ID connection for the KGPSA may change. If this happens, any storage accessed through it that is isolated using selective storage presentation (SSP) at the HSG80 seems to “disappear.” The reason it seems to disappear is that we use the HOST_ID to configure the connections at the HSG80 (when using SSP). If the HOST_ID changes, the SSP settings no longer apply since the connection names are different. For example, consider one such connection:

Before the firmware update:

```
HSG80> SHOW CONNECTION
Connection
Name      Operating system  Controller  Port  Address  Status  Offset
UNIX01    TRU64 UNIX         THIS        2     000008   OL      this    00
          HOST_ID=1000-0000-C123-ABCD  ADAPTER_ID=1000-0000-C123-ABCD
```

After the firmware update:

```
HSG80> SHOW CONNECTION
Name      Operating system  Controller  Port  Address  Status  Offset
INEWCON02 TRU64 UNIX         THIS        2     000008   OL      this    00
          HOST_ID=2000-0000-C123-ABCD  ADAPTER_ID=1000-0000-C123-ABCD
UNIX01    TRU64 UNIX         THIS        2     000008   Offline 00
          HOST_ID=1000-0000-C123-ABCD  ADAPTER_ID=1000-0000-C123-ABCD
```

Once discovered, you can quickly resolve this problem by deleting the old connection and renaming the new one at the storage controller (HSG80). See Chapter 4 for more information about storage configurations including selective storage presentation.

## A.1.9 CAA daemon (caad) Doesn't Start When Booting

The explanation here is that there probably isn't a TruCluster Server license registered on that member. Each member must have the TCS-UA license. See the Cluster Administration manual (Chapter 11). The boot messages will probably look like this:

```
TruCluster Software is not licensed for use on this system.
This system will continue running but Cluster Availability
will not function. Please install the TCS-UA license and reboot this member.Error:
CAA daemon not started.
CAA dependent system services will not start.
NFS mount daemon started
NFS export service started
Cannot communicate with the CAA daemon.
...
14-Sep-2002 18:01:37 [600] esmd: System Error: The CAA daemon has failed and cannot be restarted
```

And you may also see messages in the /var/adm/messages file:
