# 2.7.9 Device Request Dispatcher

The Device Request Dispatcher (DRD) accepts requests for data from the physical file systems and sends the request to the appropriate serving member. Note that the CFS is organized as client-server as is the DRD in some cases. The DRD is at a lower level than the CFS and does not concern itself with file system specifics. It dispatches the requests for data to be retrieved from the devices (thus the name).

The DRD provides cluster-wide access to disk storage regardless of whether the disk storage is accessible locally. The DRD will use the ICS and ultimately the CI to send its requests for data to the appropriate serving member. Note that DRD is not limited to providing access to disks. It also provides access to tape drives, floppy drives, CD-ROM, and DVD-ROM devices.

Be aware that prior to V5.0, DRD stood for Distributed Raw Disk. After V5.0, the Device Request Dispatcher provides access to raw disks and other block devices. Thus the change in the acronym was made.

Figure 2-14 includes the DRD handling requests for device access.

![](bbox=[0.22, 0.68, 0.78, 0.94])

Figure 2-14: DRD Subsystem Relationships