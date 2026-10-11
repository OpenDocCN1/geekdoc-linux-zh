TABLE 10-4 LAPTOP POWER MANAGEMENT TOOLS

| Utility | File | Description |
| :--- | :--- | :--- |
| Apm Daemon | apmd-2.4.tar.gz | Monitors battery status via Advanced Power Management |
| Apm X | apmx-0.00.tgz | Monitors battery power via percentage, charging, and battery off-line status |
| Tkbattery | tkbattery-1.0.tgz | X-based low-battery warning monitor |
| Xbatcheck | xbatcheck-1.2.tar.gz | X-based battery monitor with critical power alarm |
| X Battery Status Viewer | xbatstat-0.5.2.tar.gz | Monitoring Battery Status via /proc/apm that requires XFORMS-0.81 |
| Xbattery | xbattery-1.0.tar.gz | Monitors battery and AC-power status in an X window |

You have a variety of programs you can use for power management on laptops. These include *apmd*, which is a daemon for monitoring battery power. For monitoring it under X, you can use *apmx*. A highly configurable battery monitor is *tkbattery*, which uses APM like the previous two programs listed above. Additionally, there are three other tools that let you monitor your battery status and even your AC power in X. They are *xbatcheck*, *xbatstat*, and *xbattery*.

# # Rescue Disks

If you're playing around with your system, or your system happens to just crash for no apparent reason (this happens to all of us), you should have a rescue disk of some sort.

You can always use the command *make zdisk* from your kernel for a boot disk, but a rescue disk is always good to have handy. There are quite a few utilities available for download at http://sunsite.unc.edu/pub/Linux/system/recovery/, or you can use the *rawrite* command to the *rescue.gz* image onto a floppy disk as well. Table 10-5 gives you an overview of some utilities that increase your options for creating rescue disks.

In the *sunsite.unc.edu/pub/Linux/system/recovery/images/* directory, you can find *cramdisk* — which have both boot disk and RAM disk on one floppy — that provide rescue support for parallel-port Zip drives, PPP, Lynx, and other networking utilities. They can work with hosts that have at least 4MB of memory.