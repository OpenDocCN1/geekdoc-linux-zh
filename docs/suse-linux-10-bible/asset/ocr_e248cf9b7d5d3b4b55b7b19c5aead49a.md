# Chapter 8 ♦ The X Window System 219

After you have created this file, exit the text editor and log out. This should display the standard SUSE graphical login screen. Log back in, and the system will execute the .xinitrc file in your home directory to start xterm and the Fluxbox window manager.

When you are running Fluxbox, click the right mouse button to display its application and configuration menu.

The contents of this menu are determined by the file ~/.Fluxbox/menu, which is a text file that is located in your home directory. To add other commands to this menu, simply edit the file and add those commands to the menu. To switch between different Fluxbox themes, select Fluxbox menu: System styles from the main Fluxbox menu and select any of the other styles that are listed on menu.

If, experimenting with Fluxbox, you decide that you prefer the desktop environment or window manager that you were previously using, simply remove the .xinitrc file from your home directory and your system will return to using its previous graphical defaults.

![](bbox=[0.181, 0.488, 0.815, 0.843])

Figure 8-9: The Fluxbox application and configuration menu