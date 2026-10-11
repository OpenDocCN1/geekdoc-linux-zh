+   • **Low command latency** Because of the simplicity of the EIDE interface, EIDE drives respond quickly to commands. The result is that EIDE drives can sometimes return the first data packet more quickly than can equivalent SCSI models. This characteristic is due to the difference between EIDE and SCSI, but it’s generally swamped by other performance factors.

+   • **Low capacity** At any given moment in time, EIDE hard disks cover a lower range in capacities than SCSI hard drives. For example, Figure 5.3 represents the capacities advertised at a major Internet computer retailer in February of 2000. Note that there’s considerable overlap in available capacities for both EIDE and SCSI, but the EIDE range is lower than that of SCSI devices.

![](bbox=[0.35, 0.4, 0.6, 0.48])

# **Figure 5.3**
EIDE hard disks aren’t available in capacities as high as those for SCSI hard disks.

+   • **CHS or LBA modes** IDE hard disks have traditionally used a three-number identifying code for each sector on the disk. Known as cylinder/head/sector (CHS) addressing, this code is a remnant from the days when hard disks had almost no onboard electronics. More recently, EIDE drives have added logical (or linear by some definitions) block addressing (LBA) mode, in which a single number is used to identify a sector on the hard disk.

In addition to these characteristics of EIDE drives, the EIDE interface itself possesses several characteristics of interest to this discussion:

+   • **Two-device limit** Each EIDE chain (that is, devices attached to a single port) is limited to just two devices. Most motherboards include only two EIDE ports, so the total number of EIDE devices supported per motherboard is just four. This isn’t many on modern systems sporting devices like hard disks, CD-ROM drives, CD-R burners, and LS-120 or zip drives.

+   • **Non-concurrent communication** The two devices on each chain can’t communicate simultaneously; one or the other monopolizes the EIDE bus.

+   • **Interrupt consumption** Each EIDE chain requires the use of one interrupt (IRQ). Because IRQs are a very limited resource on modern PCs, the use of one IRQ per two devices can be a very serious problem, particularly if you exceed the four devices supported by modern motherboards.