# Administration and configuration

You enter the administration part of vast via the SYSTEM ADMINISTRATION command in the main menu. The following list provides an overview of further alternatives:

# INTEGRATE HARDWARE INTO SYSTEM

Here you can change the settings of your mouse, modem, CD-ROM drives, printers, ISDN hardware, scanner, and network cards.

# KERNEL AND BOOT CONFIGURATION

Here you can select a new boot kernel (which in normal operation occurs rather infrequently), create a boot diskette, and configure LILO.

# NETWORK CONFIGURATION

Via submenu entries you can modify various aspects of the network connection, such as host name, name server, sendmail, network printers, ISDN, and PPP.

# CONFIGURE LIVE-SYSTEM

This command allows you to mount the Live file system of the last CD-ROM distribution into your system. This way you can try out a large part of the SUSE packages without installing them onto your (always too small) hard disk. Disadvantage: the CD-ROM is blocked by the Live system and start-up takes somewhat longer.

# LOGIN CONFIGURATION

Here you can set up your system in such a way that after system start-up a graphical login (either xdm or kdm) appears. However, please change the login only if both the base system and X are working reliably!

# SETTINGS OF SEUSEWM

In this dialog you can set the default window manager for the entire system (that is, for all users). GNOME, however, is not among the alternatives presented in this dialog – more about the use of GNOME can be found on page 747.

Obviously the window manager can also be set individually for each user, by modifying the \.xinitrc or the environment variable WINDOWMANAGER.

The usewm package is responsible for the fact that X window managers are available with which you can start (nearly) all installed programs. (In contrast to other distributions, these are not dummy menus of whose entries lead to nothing the programs are not installed.) These menus need to be updated at each software installation or uninstallation. The responsibility of the SuSEConfig program. Since updating these menus takes some time, it can be completely switched off in the settings dialog, or at least restricted to a small number of window managers.

# USER ADMINISTRATION AND GROUP ADMINISTRATION

These dialog help with creation and assignment of new users and groups.

# CREATE BACKUPS

This menu item hosts a small backup program (see page 745).