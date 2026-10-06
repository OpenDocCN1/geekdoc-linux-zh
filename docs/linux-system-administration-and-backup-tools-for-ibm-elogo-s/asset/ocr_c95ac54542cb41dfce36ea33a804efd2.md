# SELECTION OF NETWORK

The base configuration of your network devices is set here. Press F6 to assign an IP address to a network device. Use F7 to configure your hardware; this is only necessary with ISDN and PLIP networks. The ISDN parameters may be configured by pressing F8.

![](bbox=[0.166, 0.14, 0.833, 0.339])

Figure 10. YaST: enter another network device

You can add multiple IP addresses to one Ethernet card, by configuring it using eth0:9; eth0:1 and so (IP aliasing support must be activated in the Linux kernel; the default SuSE kernel has been compiled with IP aliasing support).

After you have finished the network configuration, press F10 to save the current setup. YaST will now create the respective entries in /etc/rc.config and the network setup will be applied after the next reboot or after restarting the network and routing scripts.

# 4.6 Changing the configuration file with YaST

SuSE Linux utilizes a central file /etc/rc.config to store most of the system configuration information. The contents of this file will be used by the init scripts on boot, as well as for creating configuration files for the different services.

The format of this file is plain ASCII text. The configuration is stored in the form VARIABLE=value. Additional comments are marked with a "#" at the beginning of the line. Since rc.config contains most of the configuration information, you do not need to edit the original configuration files for most services. It is sufficient to make the change in this single file; YaST (in combination with the SuSEconfig collection) will take care of the correct creation of these files. However, if you are used to modifying the