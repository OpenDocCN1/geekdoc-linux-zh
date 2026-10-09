![](bbox=[0.3, 0.09, 0.88, 0.32])

Figure 2-1 LVM: Logical Volume Manager

reset the computer. The computer boots and displays the Install Image Boot menu (Figure 3-4, page 61).

+   2. You can make a selection from the Install Image Boot menu, press the TAB key to display the boot command line (which you can modify), and begin installing Fedora/RHEL when you are ready. One of the menu items checks the installation medium. If you do nothing, Anaconda starts installing the system after 60 seconds.

+   3. As part of the process of bringing up a live session or installing Fedora/RHEL, Anaconda creates RAM disks (page 1269) that it uses in place of the hard disk used for a normal boot operation. Anaconda copies tools required for the installation or to bring up a system from a Live or Install Image to the RAM disks. The use of RAM disks allows the installation process to run through the specification and design phases without writing to the hard disk and enables you to opt out of the installation at any point before the last step of the installation. If you opt out before this point, the system is left in its original state. The RAM disks also allow a live session to leave the hard disk untouched.

+   4. You give Anaconda information about how you want to configure the system.

+   5. When Anaconda is finished collecting information, it writes the operating system files to the hard disk.

+   6. When you reboot the system, gnome-initial-setup asks questions that are required to set up the first user (page 68).

+   7. The system is ready for you to log in and use.