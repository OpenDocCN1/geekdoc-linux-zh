+   - **Fast SCSI (SCSI-2)** Fast SCSI allows faster timing on the bus; 10MHz instead of 5MHz. On an 8-bit SCSI bus, this increases the maximum speed from 5MBps to 10MBps.
- **Ultra SCSI** Allows up to 20MHz signals on the bus to achieve speeds of up to 20MBps.
- **Wide SCSI (SCSI-3)** Uses an extra cable (or 68-pin P cable) to send the data 16 or 32 bits wide. This allows for double or quadruple speed over the SCSI-1 bus. Currently, no single drive reaches these speeds, but groups of several drives can.

Following is a visual guide for SCSI connectors.

Most SCSI Slow (5MBps) computers and host adapters use the Centronics-type 50-pin connector shown in Figure C-1.

![](bbox=[0.14, 0.37, 0.7, 0.45])

Many 8-bit SCSI Fast (up to 10MBps) computers and host adapters use the 50-pin high-density connector shown in Figure C-2.

![](bbox=[0.14, 0.57, 0.6, 0.65])

All Fast or Wide (16-bit) SCSI-3 computers and host adapters, as well as old DEC single-ended SCSI s, use the 68-pin high-density connector shown in Figure C-3.

![](bbox=[0.14, 0.77, 0.7, 0.85])

A less common SCSI connector, the New SCA 80-pin connector is shown in Figure C-4.

![](bbox=[0.14, 0.91, 0.7, 0.95])

As when adding any other peripheral or equipment to your system, consult with the manufacturer first. When adding equipment to your Sun system, first call Sun and make sure the equipment is supported under Solaris and that you can obtain instructions for connecting the equipment. Again, a few minutes of planning will save hours of grief and downtime. Most system administrators are more comfortable having their hardware maintenance person install the equipment.