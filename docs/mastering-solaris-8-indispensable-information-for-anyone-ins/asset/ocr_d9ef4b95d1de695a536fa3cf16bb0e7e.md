subsystem and block aggregation layer to the storage device. The file subsystems provide access methods and packaging (naming and space allocation) as well as caching for performance and coherency in distributed systems. Most of the model is devoted to block aggregation, and this model is not device centric. That is, you don't see network-attached storage (NAS) devices, Storage Area Networks (SANs), switches, and other devices indicated as you might on a topology map.

# FIGURE 9.5
The SNIA Shared
Storage Network
Model

![](bbox=[0.28, 0.27, 0.87, 0.58])

In the block subsystem are the storage devices: disks, tape drives, and solid-state devices that store data. At that level there are space management, block aggregation, striping, and redundancy (mirroring) features and address mapping. For SANs, *aggregation* means virtualization through slicing and concatenation. That includes features such as RAID, mirroring, and so forth, managed by volume managers and disk array logical unit numbers (LUNs). The block level also includes a caching function. The block subsystem determines where operations take place: on a host (logical volume, HBA, or device driver), on a storage device (array controller or disk controller), or over the SAN using an HBA or a specialized appliance. Data is moved in and out of the block system as a vector of blocks.

All of the pieces of the services subsystem remain to be more fully described and worked into this model. In truth, many of the principles of discovery and monitoring, for example, are yet to be fully worked out in the industry. Another important thing to note is that anywhere you see an interface, you are looking at the most dynamic areas of development and the places in which competing standards tend to make life difficult for storage value-added resellers (VARs) and integrators.