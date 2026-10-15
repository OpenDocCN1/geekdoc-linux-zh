15. This brings you to the "Bootselection menu items" screen. Here, you can change the simple menu entries for matching partition entries that are displayed when the system boots. Also, you can specify the timeout (in seconds) and the default action to be taken (if no selection is made in the bootmenu). By default, the Boot menu timeout is set to 10 seconds, which I change to 100 seconds. The default boot menu action is set to "Boot off partition 0".

16. Then edit menu entries 0 and 1, to label "Windows" and "NetBSD" respectively. Then exit.

17. Next appears the NetBSD Disklabel screen. Here you are expected to set up your NetBSD disklabel. Four options are mentioned: Standard, Standard with X, Custom and Use existing.

18. I choose the installation type: "Standard with X" which requires about 450.00 MB HDD space.

19. Next screen exhibits the BSD–disklabel partitions. Since for most people in most situations this suits the best, keep the changes as it is and select "Partitions are OK" and press enter.

20. A name is prompted for your NetBSD disk, I entered "ghosh" and continue.

21. /sbin/newfs runs to create the new filesystems.

22. In the next screen you are prompted to install either normal set of bootblocks or serial bootblocks. Since we are using the BIOS console device as the console, you must select "Use normal bootblocks" and press enter.

23. This completes the first part of the NetBSD installation procedure. Sysinst has written a disklabel to the target disk, and newfs'ed and fsck'ed the new partition on the disk. The next step is to fetch and unpack the distribution filesystems.

24. I chose "Custom Installation" of NetBSD distribution sets.

25. In the next screen, choose all that you would like to install and press "Exit".

26. Enter the type of installing media. Select "cdrom" and device::cd0 and directory:/i386/binary/sets and continue.

27. The following .tgz files gets untarred and installed onto your hard disk: base.tgz, etc.tgz, comp.tgz, games.tgz, man.tgz, misc.tgz, text.tgz, xbase.tgz, xfont.tgz, xserver.tgz, xcomp.tgz and xcontrib.tgz.

28. A message appears as "All selected distribution sets unpacked successfully". Next, device files are made automatically, and you are prompted for a few necessary post–installation configuration steps.

29. You need to set timezone, I choose "Europe/Moscow".

30. Next, to choose the password cipher. The options available are: DES or MD5. I prefer MD5 to DES.

31. I set the root password and then finally a message appears on your screen telling you that NetBSD 1.6.1 operating system has been successfully installed on your computer. Reboot your computer to boot from hard disk.

32. When I reboot for the first time, I get the following prompt on the screen: F1 Windows, F2 NetBSD each in one line. I press the F1 functional key to boot into Windows 98 (SE) and check whether everything is working perfectly or not. As it so happens, it does! Then I reboot and this time, I press F2, which logs me into NetBSD 1.6.1.

33. Depending on the configuration of your computer, you will receive bootup messages on your screen when you boot into NetBSD for the first time. Though the messages scroll off the screen rather fast for you to read anything productive, you can always read it later by using the "/sbin/dmesg | more" command. Finally, you will arrive at the login prompt. Login using the username/password you set during installation. Check if everything is in place or not and try exploring the new system.