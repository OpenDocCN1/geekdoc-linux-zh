24. When prompted about DHCP, select Yes if you are using host-only networking or if your LAN uses DHCP (for bridged networking). You can always change the settings later.

25. Setup installs various drivers and then asks to start the network. If you plan to use Samba file sharing (either with your Linux PC over host-only networking or with a "real" Windows PC), ensure that the Workgroup field matches. (For host-only, WORKGROUP is the default setting. See Appendix B for more information.) Do not use the Domain setting unless you are using this virtual machine on a real Windows NT Server network, and you are very sure you know what you're doing. Click Next when done.

26. Click Finish to wrap up the installation. You are asked to set the date, time, and time zone.

27. The Display Properties window appears. Leave the default in place (640×480, 16 colors); you can improve your lot later by installing VMware Tools.

28. After a great deal of disk activity, setup asks you to remove the CD-ROM and click to restart the computer. Remember that you might need to disconnect the CD-ROM from VMware and manually unmount the CD in Linux before you can eject it. Be sure to re-attach the CD-ROM after you remove the CD so you can read other discs, and then click Restart.

29. When the NT boot menu appears, press Enter on the top (default) setting. After the NT splash screen appears, press Ctrl+Alt+Del to sign on, and then enter the administrator password you assigned during the setup process.

![](bbox=[0.27, 0.73, 0.68, 0.92])

Figure 11.14 Match the Workgroup setting with VMware's Samba server if you plan to use Samba over host-only networking.