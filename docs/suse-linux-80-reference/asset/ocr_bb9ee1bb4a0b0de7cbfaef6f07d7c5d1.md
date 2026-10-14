![](bbox=[0.166, 0.089, 0.983, 0.382])

*Figure 11.1: System Information*

If you booted a kernel that already had a SCSI driver compiled, you do not need this SCSI driver as a module as well. Quite typical announcements when loading SCSI adaptors and connected devices might look like this:

```
scsi : 1 host.
Started kswapd v 1.4.2.2
scsi0 : SCSI host 0 accepting period 100ns offset 8 10.00MHz FAST SCSI-II
scsi0 : setting target 0 to period 100ns offset 8 10.00MHz FAST SCSI-II
  Vendor: QUANTUM  Model: VP3210S       Rev: 811H
  Type:   Direct-Access                    ANSI SCSI revision: 02
Detected scsi disk sda at scsi0, channel 0, id 0, lun 0
scsi0 : setting target 2 to period 248ns offset 8 4.03MHz synchronous SCSI
scsi0 : setting target 2 to period 248ns offset 8 4.03MHz synchronous SCSI
  Vendor: TOSHIBA  Model: CD-ROM XM-3401TA  Rev: 0283
  Type:   CD-ROM                         ANSI SCSI revision: 02
scsi2 : detected 1 SCSI disk total.
SCSI device sda: hdwr sector=512 bytes. Sectors=4308352 [2103 MB] [2.1 GB]
Partition check:
 sda: sda1 sda2 sda3 sda4 < sda5 sda6 sda7 sda8 >
```

# Loading Modules

Select which kinds of modules you need. If you booted via disk, the corresponding data must be read by linuxrc and displayed in a list.