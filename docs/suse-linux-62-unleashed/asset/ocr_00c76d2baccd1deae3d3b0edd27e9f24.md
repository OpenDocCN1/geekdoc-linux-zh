# The BRU-2000-PE software is installed using the rpm command.

To do a full or incremental backup of your system, you must run BRU-2000 as the root operator. To use the graphical interface version, start the program by typing xbru at the command line of an X11 terminal window to see the main dialog box shown in Figure 20.3.

**Figure 20.3**nThe BRU-2000 program is a commercial backup and restore program for nearly 20 operating systems, including Linux.

![](bbox=[0.215, 0.245, 0.685, 0.495])

> Note
Updated software of the X11 BRU-2000 interface is available at ftp://ftp.estinc.com/pub/X11 or through http://www.scriptics.com.

The program first checks the status of the default backup device, but you can configure the program to use one of more than 37 different devices for backup. You can also define new devices, such as Iomega Zip drives, for storing tape archives. To configure BRU-2000 to use a Zip disk as a backup device, select the Configure BRU menu item from the File menu. A new dialog box appears, as shown in Figure 20.4.

> Note
If you have an older version of BRU-2000, check http://www.estinc.com/brutabs.html for important updated device table files as jazz.fix and zip.bt. You'll need to use them on an Omega Zip or Jaz disk with BRU-2000. First, you should add the following lines to the /usr/lib/bru/unmountape.tcl file :