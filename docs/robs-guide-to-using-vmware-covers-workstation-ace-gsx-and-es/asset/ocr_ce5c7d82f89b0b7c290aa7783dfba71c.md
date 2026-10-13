16. In the Advanced Selection screen, select the SCSI 1:0 location for your SCSI disk.

![](bbox=[0.13, 0.16, 0.8, 0.66])

Figure 26.11: Select SCSI bus 1 for the new disk.

It is common practice to add your shared disk to a separate SCSI bus channel and not on the SCSI 0 bus. That bus is commonly used for a SCSI boot disk and you do not want to accidentally share your server's system boot disk.

17. Click Finish and close the virtual machine settings' Control Panel.

18. At this point the .vmx file for both virtual machines should contain the following lines:

```
scsi1.present = "true"      (Added to create a second SCSI bus)
scsi1:0.present = "true"
scsi1:0.fileName = "C:\<pathtodisk>\shared.vmdk"
scsi1:0.deviceType = "plainDisk"
```