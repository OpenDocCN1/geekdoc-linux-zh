space. During the RHEL 9 installation process, this can be achieved by selecting the Installation Destination option on the Installation Summary screen and ensuring that the Automatic storage configuration option is selected. This will automatically install RHEL 9 into the unallocated space created when the Windows partition was reduced in size.

Once installation of RHEL onto the disk is complete and the system has restarted, the standard RHEL boot menu will appear, including an additional option to boot the Windows system:

![](bbox=[0.28, 0.21, 0.74, 0.48])

Figure 4-4

# 4.2 Changing the Default Boot Option

When the system starts, the boot options screen will appear, and wait 5 seconds for the user to choose an operating system. If no selection has been made before the timeout elapses, the default operating system will be started. The default operating system will be the standard (non-rescue) RHEL 9 image on a newly configured system. This default can, however, be changed from within RHEL.

A range of boot configuration options (including the 5-second timeout and the boot RHGB settings outlined in “Installing RHEL 9 on a Clean Disk Drive”) are declared in the /etc/default/grub file, which reads as follows on a new installation:

```
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=1G-4G:192M,4G-64G:256M,64G-:512M resume=/dev/mapper/rhel-swap rd.lvm.lv=rhel/root rd.lvm.lv=rhel/swap rhgb quiet"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

The first step in changing the default boot system is to declare the GRUB_SAVEDEFAULT setting