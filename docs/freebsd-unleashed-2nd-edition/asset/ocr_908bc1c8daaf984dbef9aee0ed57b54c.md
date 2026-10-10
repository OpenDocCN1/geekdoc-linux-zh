> **CAUTION**
> 
> Up to this point, no changes have actually been made to your hard disk. This is your last chance to back out of the installation. After you select *Yes*, the partitions you created will be formatted and the installation will begin. Any existing data on the partitions you selected to use will be lost!

Assuming you are happy with the installation choices you made, select *Yes*. The system then prints a message telling you it is starting an emergency holographic shell on tty4. It then proceeds to format the partitions. After partition formatting is done, Sysinstall will begin copying files to your hard disk(s).

# # Post-installation Configuration and Customization

When the file-copying process is complete, you will see a screen that congratulates you for making it to this point. The screen also informs you that Sysinstall will now move on to the final configuration questions. In addition to configuring the network in this post-installation phase, you will set the time; configure the mouse; choose the desktop, software packages, and users you want to assign to your system; and set the root password. Select *OK* to continue.

# ## Configuring the Network

Next, you are asked if you want to configure any Ethernet or SLIP/PPP network devices. If you have the values from your system administrator, you can go ahead and set these up now. If you don't have the values available or if you are setting up a new network and are unfamiliar with networking, you can always re-enter this utility later after you have read the chapters on networking.

> **CAUTION**
> 
> If you are on a network and you do not configure the network device(s) now, be aware that when the system reboots, you cannot access the network until you configure the network devices to work with your network. With that said, if you don't have a network or you don't know what values should go in the fields for the network configuration, go ahead and skip this section and come back to it later after you have read the networking chapters.

If you don't want to configure any network devices now, simply select *No* and move on to the next section of this chapter. If you do want to configure network devices at this time, select *Yes*. You should now see a screen like the one shown in Figure 2.6.

Select the network device you wish to configure from the list and then press *Enter*. Note that depending on the make and model of your Ethernet adapter, it may have various names. It will usually have the number zero, though, if it is the first Ethernet adapter in the system.