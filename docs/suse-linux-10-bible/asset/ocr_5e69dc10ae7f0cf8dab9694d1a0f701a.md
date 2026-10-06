# 710 Part V ◆ SUSE Linux in the Enterprise

| The Virtual Machine Options |
| --- |
| Options How much memory will be used by the virtual machine.
The virtual machine can be started automatically on boot or manually when needed.
Boot Options are used as extra arguments for the kernel.
| Machine Name domain1 |
| Boot Options |
| Memory Size in MB 256 |
| Activation Manually |
| Cancel | Accept |

**Figure 28-8:** Setting virtual machine options in YaST

You may need to adjust the amount of memory allocated to your main Xen domain in /boot/grub/menu.1 and reboot in order to make sure that free memory is available to you to create additional Xen domains.

+   3. Click the Dis heading to adjust the size and name of the virtual disk image that is being created. The screen shown in Figure 28-9. Click Edit to modify the default entry or click to specify a new one. I intend to use 4 GB (4096 MB) as the size of disk images for Xen domains, as this provides to add applications, collect data from long-running applications, and so on. Click Accept to continue.

+   4. If you do not already have a network installation source defined, Click Source to define one. YaST's Virtual machine Installation module requires the use of a networked install source as FTP, HTTP, SMB, or NFS. This displays the standard YaST Installation Source dialog box. After defining a networked install source, that YaST module closes and the Virtual Machine Installation dialog box redisplays.

+   5. Click Network to customize the setting of the network interface used by the Xen domain that you are creating. It is rarely necessary to modify this.