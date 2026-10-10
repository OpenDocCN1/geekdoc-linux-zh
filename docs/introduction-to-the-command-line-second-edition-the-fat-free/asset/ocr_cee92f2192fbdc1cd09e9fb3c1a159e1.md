# ioscan

**Purpose:** List hardware on HP-UX systems.

**Usage syntax:** `ioscan [OPTIONS]`

```
```
# ioscan
H/W Path  Class         Description
=======    ===         ==========
      0
            bc           I/O Adapter
8/0        ext_bus      GSC add-on Fast/Wide SCSI Interface
8/0.5      target
8/0.5.0    disk         SEAGATE  ST34371W
8/0.7      target
8/0.7.0    cti          Initiator
8/0.8      target
8/0.8.0    disk         SEAGATE  ST318436LC
8/4        ba           PCI Bus Bridge - GSCtoPCI
8/4/1/0    lan          HP  J3515A  HSC 10/100Base-TX D-Class
1 port     Core I/O Adapter
8/16       ba           Initiator
8/16/0     ext_bus      Built-in Parallel Interface
8/16/4     tty          Built-in RS-232C
8/16/5     ext_bus      Built-in SCSI
8/16/5.0   target
8/16/5.0.0 tape         HP  C1537A
8/16/5.2   target
8/16/5.2.0 disk         SONY   CD-ROM CDU-76S
8/16/5.7   target
8/16/5.7.0 cti          Initiator
8/16/6     lan          Built-in LAN
8/16/7     ps2          Built-in Keyboard/Mouse
8/20       ba           Core I/O Adapter
8/20/2     tty          Built-in RS-232C
...
         
            Listing devices with ioscan on HP-UX
```
```

**ioscan** displays information about hardware installed on HP-UX systems. The above example displays the typical output of this command which shows information about the system’s hardware profile.

**Common usage examples:**
`ioscan`  | Display a simple hardware listing
`ioscan -f` | Display a detailed hardware listing