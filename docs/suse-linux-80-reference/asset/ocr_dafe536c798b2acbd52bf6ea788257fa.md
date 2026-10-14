| Variable | Values / Meaning |
|---|---|
| `{addr}` | Address of the adapter, e.g. 0x300 |
| `{probing}` | `NoProbe` No adapter is probed  
`NoProbeISA` No ISA adapter is probed  
`NoProbePCI` No PCI adapter is probed  
`NoSortPCI` Order of multimaster adapter set by PCI BIOS  
`MultiMasterFirst` Multimaster before Flashpoint  
`FlashPointFirst` Flashpoint before Multimaster  
`InhibitTargetInquiry` For old devices that cause trouble with `scsi_luns > 0`  
`TraceProbe` outputs additional messages at initialization of the adapter  
`TraceHardwareReset` outputs additional messages at the adapter hardware reset  
`TraceConfiguration` outputs additional messages at the adapter configuration  
`TraceErrors` outputs error messages of the attached devices  
`Debug` outputs all |

This host adapter understands even more parameters. These are for fine tuning the adapter and are described in `/usr/src/linux/drivers/scsi/README.BusLogic`.

+   - *Future Domain TMC-16x0 SCSI host adapter*  
+     `fdomain={addr},{irq},{id}`

| Variable | Values / Meaning |
|---|---|
| `{id}` | SCSI ID of the host adapter `0...7` |

This driver also controls the Adaptec 2920.

*Example:* `fdomain=0x1400,11,7`

+   - *Future Domain TMC-885/950 host adapter*  
+     `tmc8xx={addr},{irq}`  
+     *Example:* `tmc8xx=0xca000,5`

+   - *NCR 5380 SCSI host adapter family*  
+     `ncr5380={addr},{irq},{dma}`