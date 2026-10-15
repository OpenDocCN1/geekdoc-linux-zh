6. VMware now asks whether you want to create a new virtual disk or use an existing physical disk. The default option is to use a new virtual disk, which you should accept unless you have familiarized yourself with the concepts of raw and plain disks in Appendix A, “Advanced VMware Configuration.” Click Next.

7. Enter the size, in megabytes, for the virtual disk when asked by the window shown in Figure 13.2. (2,000 is the default.) Keep in mind that virtual disks grow as you add data, but once created, the maximum size is fixed. Click Next to proceed.

8. VMware should detect your CD-ROM at this stage. Leave the default settings alone, and click Next to continue.

9. VMware now asks the same question about floppy access. Unless you have a compelling reason to disable the floppy, leave this setting alone as well. Click Next.

> Contemporary CD-ROM distributions of FreeBSD are bootable, so you do not need a boot floppy. Still, if you have a floppy drive available, it’s safest to let VMware use it.

10. You can configure the virtual machine for networking on this step, shown in Figure 13.3. No networking keeps the FreeBSD VM isolated. Bridged networking configures a virtual Ethernet card that can communicate with your LAN and the outside world, and Host-only networking enables file sharing and communication between your virtual machine, the host PC, and any other virtual machines with host-only networking enabled. If you plan to use host-only networking, it is best to let VMware install its own Samba and DHCP server (as advised in Chapter 4, “Installing VMware for Linux”). If you have a LAN, use Bridged for now. If you do not, use Host-only or None. Click Next to reach the final step.

![](bbox=[0.22, 0.8, 0.48, 0.97])

Figure 13.2