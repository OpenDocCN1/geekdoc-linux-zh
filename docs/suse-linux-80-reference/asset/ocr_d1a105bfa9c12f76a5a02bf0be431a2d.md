# Configuring the Boot Mechanism with loadlin

loadlin will be introduced in the following sections as another method of booting SuSE Linux. loadlin is a DOS application capable of booting a Linux kernel stored in a DOS directory. loadlin can be seamlessly integrated into an already existing DOS/Windows 9x environment and easily started with the help of Windows boot manager. As there is no entry in the MBR, Windows will not know that Linux is installed, but only “see” one or more partitions possessing IDs Windows does not recognize. Undesired side effects that could result from Linux coexisting on your Windows system are minimized that way.

The procedure described here works for Windows 95 and Windows 98. The configuration files shown below were developed for Windows 95. Therefore, the following only directly refers to Windows 95.

You will have to make some preparations before you can use loadlin to boot Linux. Depending on your system environment, you will also have to modify certain boot files.

loadlin can be activated in two ways: by selecting from several configurations in the boot menu or by starting loadlin from a running system state switching to Linux. Both methods have their advantages and disadvantages:

+   - Using the boot menu, avoid starting Linux from within another operating system.
+   - You can integrate other configurations into a boot menu.
+   - However, you must modify the boot files to set up a boot menu. You might have to try out different options. Some helpful tips can be obtained in the DOS help files after typing `help menu`.
+   - Switching to Linux at the DOS prompt is quite simple.
+   - The Linux boot can be nicely built into the graphical user interface of Windows 95. Switch to Linux by double-clicking an icon. You can also set up a boot menu in Windows 95 (Windows 95 runs on DOS 7.0).

> **Tip**
> 
> If possible, use a boot menu if you want to boot Linux as soon as you switch on the computer. The DOS prompt or the double-click method can additionally be used to switch to Linux from DOS/Windows 95. Only a summary of using Windows boot menus is included here.