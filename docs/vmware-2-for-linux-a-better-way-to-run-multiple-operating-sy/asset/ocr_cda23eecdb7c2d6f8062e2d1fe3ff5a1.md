![](bbox=[0.25, 0.08, 0.68, 0.38])

# Figure 6.10

6. Seeing that you have an unformatted hard disk (never mind the fact that it’s really just a virtual disk), Windows Setup asks whether you want to configure the unallocated space. Let it do so.

> If you know you have special partitioning needs, instead of booting to Windows Setup, boot the PC with CD-ROM support and then run fdisk at the DOS prompt and create your own partitions on the virtual disk.

7. If you defined a hard drive larger than 512MB in size, Windows asks to turn on large disk support. You should enable this option unless you plan to do something elaborate such as create a dual-boot DOS partition that has access to all the Windows files.

8. Windows setup reboots the virtual machine. If you are prompted to insert the Windows 98 boot disk in drive A: ignore it. The same two text menus appear, and again tell it to boot from CD-ROM and start Windows setup from the CD-ROM. Setup then formats the virtual C: drive. See Figure 6.11 for proof.

9. Setup now performs the infamous Windows “routine check on your system”, shown in Figure 6.12. Nothing to worry about; Microsoft won’t be able to tell that you’re using VMware.

10. After the check, Windows finally starts the graphical portion of the installer, displayed in Figure 6.13. Click Continue.