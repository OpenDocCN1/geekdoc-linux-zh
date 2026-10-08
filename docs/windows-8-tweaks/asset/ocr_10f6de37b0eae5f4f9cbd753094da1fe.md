an unpleasant surprise when your computer reboots and tells you that it cannot find any operating system. If you happen to get that message, don't worry; you did not just erase your operating system. Just reboot by pressing Ctrl+Alt+Delete at the same time, go back into the BIOS settings, and make sure that you select your hard drive as a boot device. After you have done that, your system will be back to normal.

Another possible issue that you might encounter is just a matter of inconvenience. After you change the boot order of the system devices so that the hard drive is listed first, you can no longer use system restore boot discs. If something has happened to your computer and you need to boot off of those drives to restore your system or run diagnostics, just go back to the system BIOS and lower or remove the hard disk from the first boot device and replace it with a CD as needed.

# ## Using the Quick Boot Feature of the BIOS

All systems initialize in more or less the same way. During the POST mentioned earlier, the BIOS checks the hardware devices and counts the system memory. Out of all the different types of system memory, the *random access memory*, better known as RAM, takes the longest to check. On a machine that has large amounts of RAM, this calculation can take several seconds. For example, a machine that has 4 GB of RAM may take up to three seconds just to check the memory. On top of the RAM counting, your computer needs to perform a few other tests to make sure that all the hardware is working properly.

The complete version of these tests is not needed every time you boot, and you can turn them off to save time. Most system BIOSs offer a feature called *Quick Boot*. This feature enables the user to turn off the full version of the test and sometimes enables you to run a shorter quick-check test instead. Other BIOSs allow you to turn off the Memory Check only, which still saves a lot of time.

To turn on the Quick Boot feature or to turn off the Memory Check, do the following:

+   1. Enter the system BIOS by pressing F1, F2, Delete, the Enter key, or the correct system setup key on the POST screen for your system.
2. After you are in the BIOS setup, locate the Quick Boot or Memory Check option, as shown in Figure 13-2. Navigate with the arrow keys until the option is highlighted.