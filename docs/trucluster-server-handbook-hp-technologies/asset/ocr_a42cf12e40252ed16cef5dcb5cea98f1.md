After all the installed software subsets are configured, a new UNIX kernel is built for the new cluster member. This new kernel is then copied into place.

```
*** KERNEL CONFIGURATION AND BUILD PROCEDURE ***
*** PERFORMING KERNEL BUILD ***

A log file listing special device files is located in /dev/MAKEDEV.log
Working...Wed Mar 27 16:35:42 PST 2002

The new kernel is /sys/SHERIDAN/vmunix
Copying new kernel to /vmunix ...
```

As soon as this is done, the new cluster member continues to boot to multi-user mode.

# 11.4 Configuring the New Cluster Member

Once in multi-user mode, the configuration of the new cluster member continues with the setup of the system default network interface. The first prompt asks if we are prepared to add the network interface configuration for the new cluster member. We can opt to do this later using the "sysman net_wizard" command or the clu_netsetup(8) command or we can choose to configure the network interface now. For our cluster, we choose to configure the interface now.

```
clu_add_member was unable to determine the network configuration for the interface associated with this system's hostname. You may configure this interface using the clu_netsetup by answering 'yes' to the following question. If you decide not to run clu_netsetup, then the time it takes the system to boot will be considerably longer.
Would you like to run clu_netsetup at this time? [yes]: yes
**** TruClusters Add Member Network Interface Configuration ****

1 Configure Interface

2 Exit

Enter the number for your choice: 1
**** CONFIGURE/DELETE NETWORK INTERFACES ****

You can configure or delete network interfaces. Configuration information is updated in /etc/rc.config and /etc/hosts. Choose "configure" or "delete" at the prompt.

Enter whether you want to "(c)onfigure" or "(d)elete" network interfaces. If you are finished, press the RETURN key: c
```

Next, we are asked to select the network interface we want to configure. In our case, we select the "ee0" device. Your configuration will most likely be different, so plan which devices you want to use for your network interface.