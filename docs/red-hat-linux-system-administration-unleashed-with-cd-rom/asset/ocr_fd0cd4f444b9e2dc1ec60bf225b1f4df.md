SCSI bus lengths for different SCSI technologies in Table 8.6 show how the decision of which type of terminator to use affects the capabilities of the chain. Some devices may provide internal auto-termination capabilities, eliminating the need for external termination. Because this auto-termination varies from device to device, and may not be fully compatible with all SCSI host adapters, check your owner's manuals before enabling this feature.

Once the cabling requirements have been determined, the drives need to be connected to one another and to the host adapter to form the SCSI chain. Internal devices (devices within the main server cabinet) are generally connected with a long SCSI ribbon-cable with a terminator on one end and the host adapter on the other (refer to Figure 8.2). External devices may be a bit more confusing because they are generally connected in a daisy-chain fashion and terminated at the last SCSI device chassis (see Figure 8.3). Note that large-capacity SCSI device cabinets, especially hardware RAID cabinets, are generally terminated internally and do not require additional termination. Check your device cabinet owner's manual for the specific requirements of your hardware.

Figure 8.3
Daisy-chaining of external SCSI devices.

![](bbox=[0.27, 0.55, 0.6, 0.88])

# SCSI Device Naming

SCSI disk devices are named using a similar naming scheme to that of IDE disks. All SCSI disk devices begin with the prefix sd (SCSI disk) and are stored in the /dev directory.