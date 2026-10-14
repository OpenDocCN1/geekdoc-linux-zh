# Configure GRUB with YaST

Although you can use YaST (Boot Loader Configuration module) to simplify the configuration of the boot loader, you should not experiment with this module unless you understand the concepts behind it.

To start the YaST Boot Loader module, start YaST, enter the root password, and then select **System > Boot Loader**, or start the Boot Loader module directly from a terminal window by logging in as root and entering `yast2 bootloader`.

Figure 11-2 shows what appears.

![](bbox=[0.023, 0.246, 0.94, 0.762])

**Figure 11-2**

Select the Section Management tab to see the current GRUB settings for your system. The **Def (Default)** column indicates which entry is selected as the default when booting the system.