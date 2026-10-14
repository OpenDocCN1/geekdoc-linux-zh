The “ldb” file contains information for the other hardware components (adapters, cpu, keyboard, mouse, etc.) as well as some storage device information (user_name, phys_location, etc.). Component information can be seen in the following example:

```
```text
# hwmgr -show component

HWID:  HOSTNAME  FLAGS SERVICE COMPONENT NAME
----- ---------- ----- ------- ----------------
  1:  sheridan   r---  none    CPU0 AlphaStation XP900 466 MHz
  2:  sheridan   r---  none    CPU0
  4:  sheridan   r-d-  none    scp
  5:  sheridan   r-d-  none    kenv
  6:  sheridan   r-d-  none    pci0

 53:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0019-9fbe
 54:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0019-9492
 55:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0018-ba75
 57:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0018-9f1f
 58:  sheridan   -cd-  iomap   SCSI-WWID:0c000008:0000-0e11-0018-9f33
 59:  sheridan   -cd-  iomap   SCSI-WWID:0c000008:0000-0e11-0018-9f1a
```
```

+   - `dec_scsi_db`

This file is owned by the SCSI/CAM subsystem and is used to store the WWIDs and track the SCSI devices that are known to the system. This binary data file is also used by the hwmgr command. For example:

```
```text
# hwmgr -show scsi

             SCSI              DEVICE    DEVICE  DRIVER  NUM  DEVICE FIRST
HWID:       DEVID   HOSTNAME    TYPE     SUBTYPE  OWNER  PATH  FILE   VALID PATH
-----       -----   --------    -------  -------  ------ ----  -----  ----------
   0:          0    sheridan    cdrom    none       0     1   (null)
  40:          1    sheridan    disk     none       2     1   dsk0   [2/0/0]
  41:          2    sheridan    disk     none       2     1   dsk1   [2/1/0]
  45:          3    sheridan    cdrom    none       0     1   cdrom0 [0/0/0]
  53:          4    sheridan    disk     none       0     1   dsk2   [3/0/0]
  54:          5    sheridan    disk     none       0     1   dsk3   [3/1/0]
  55:          6    sheridan    disk     none       0     1   dsk4   [3/2/0]
  56:          7    sheridan    disk     none       0     1   dsk5   [3/3/0]
  57:          8    sheridan    disk     none       0     1   dsk6   [3/4/0]
  58:          9    sheridan    disk     none       0     1   dsk7   [3/5/0]
```
```

+   - `dec_unid_db`

This database contains unique IDs. According to the Tru64 UNIX System Administration guide, “This is a binary database that stores the preceding highest hardware identifier (HWID) assigned to a hardware component. This database is used to generate the next HWID to be assigned to a newly-