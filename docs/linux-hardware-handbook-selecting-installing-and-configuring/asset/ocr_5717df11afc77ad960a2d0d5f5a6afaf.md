this from the Old CD-ROM drivers (not SCSt, not IDE) configuration menu shown in Figure 7.4. You must select `Y` under the first option, Support non-SCSI/IDE/ATAPI CDROM drives, and select at least one drive type using a `Y` or `M` compilation option. Unlike with the SCSI and EIDE/ATAPI configuration, it's necessary for you to specify the exact model of CD-ROM drive you have. In some cases, you might need to specify additional options to help the driver locate the hardware.

![](bbox=[0.31, 0.28, 0.77, 0.56])

# Figure 7.4

*Linux includes support for many older proprietary CD-ROM interfaces.*

Most Linux distributions ship with support for all proprietary CD-ROM drives enabled as modules. If you're not certain what model you've got, but you know it's an older proprietary device, you might want to do the same when you compile your kernel.

# Parallel-Port Interfaces

A few CD-ROM drives use the parallell port. These devices are typically marketed for older portable computers that lack CD-ROM drives, and they're quite rare. In most cases, they use a parallel-to-IDE converter, and are handled in the same way as parallel-port removable media drives, described in the section “Parallell Port Interfaces” in Chapter 6.

As a general rule, I don't recommend using parallell-port CD-ROM drives, because they're not as reliable as their counterparts that use other interfaces. The parallell port also isn't capable of handling today's fast CD-ROM drives, although it's adequate for older drives.