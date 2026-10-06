
## GNOME System Settings Window (Continued)

| Standard/Graphical greeter | Specifies the characteristics of these greeters. The Standard chooser **Show chooser images (face browser)** allows the display of images (presumably of users) in the Login window (Figure 2-3, page 32). Each user can click his/her picture to enter his/her name in the login text box. After that the login proceeds as usual. |
| Security | These options control local, remote, and timed logins by **root** and other. **Show system menu** displays the System menu on the Login window. This menu includes the shutdown, reboot, and configuration choices. The Retry delay is the number of seconds that user must wait to log in after providing incorrect name/password information. |
| XDMCP | Controls the X Display Manager Control Protocol, which allows you to configure remote non-GUI/Linux systems with X Windows. Refer to the *Linux XDMCP HOWTO* for more information. |
| Mail Transport Agent Switched | Changes the system's mail transport agent. You can choose between *sendmail* and postfix. |
| Mouse | Selects the type of mouse attached to the system and allows you to specify simultaneously pressing the two buttons on a two-button mouse emulates pressing the middle button on a three-button mouse (Emulate 3 button click). |
| Network | Runs neat, a network configuration tool. |
| Active Profile | Network configuration profiles enable you to name profiles so that you can easily switch profiles as needed. This feature is useful on laptops that frequently change environments. This frame selects, renames, and creates new profiles |
| Add | Displays the Add new Device Type window (refer to “Internet Configuration Wizard” page 1023). In most situations you do not have to use this tab as the system sets up a network-hardware device when you install the hardware. |
| Edit | Displays the configuration window appropriate to the hardware that is highlighted so that you can make changes. |
| Copy | Copies the highlighted device and gives it a nickname that ends in **Copy0**, **Copy1**, and so on. |
| Delete | Deletes the highlighted device. You must deactivate the device before you can delete it. |
| Activate | Activates the highlighted device. |
| Deactivate | Deactivates the highlighted device. |
| Hardware | |
| Add | Displays the Choose Hardware Type window. When you select a hardware type (Ethernet, Modem, ISDN, Token Ring) from the combo box, it displays the configuration window appropriate to the type of hardware. In most situations, you do not have to use this tab as the system sets up a network hardware device when it first sees it. | Edit | Displays the configuration window appropriate to the hardware that is highlighted so that you can make changes. | Delete | Deletes the highlighted hardware. |
| Hosts | |
| Hosts | Edits the /etc/hosts file (page 1017). |
| DNS | Edits the /etc/resol.conf file; refer to "DNS: Domain Name Service" text box with your system's hostname. Fill in the three DNS text boxes with the name servers that your system uses. You do not need three, but it is a good idea to have at least two. Next is the DNS Search Path field: Specify the domain names of systems you want in your search domain—a search list for host-name lookup that defaults to the local domain name. |
| Packages | Refer to "redhat-config-packages: Adds and Removes Software Packages" on page 926. |
| Printing | Refer to "printconfig-gui: Configures and Manages LPRng Printers" on page 1006. |
| Root Password | Runs redhat-config-password, a utility that allows you to choose a new root password. |
| Security Level | Refer to "redhat-config-security: Sets up a Firewall" on page 924. |
| Soundcard Detection | Runs redhat-config-soundcard, which displays sound card information and allows you to test the sound system. |
| Users and Groups | Refer to "redhat-config-users: Manages User Accounts" on page 993. |

## KDE Control Center: System Module

Select this module from K menu: Control Center⇔System; you can select the individual functions from K menu: Preferences⇔System.

When you are not running as root, many of the items in the System section of the Control Center are gray out, indicating that you cannot modify or use them. In each of the windows that contains grayed-out sections, clicking the Administrator Mode at the lower-right corner of the window allows you to supply the root password to bring all the items in the window to life so that you can modify/use them (Table 17-10).

## KDE Control Center: System Module

| table 17-10 | |
| --- | --- |
| Alarm Daemon | Configures kalarm, the alarm daemon, which monitors the kalarm, korganizer, and other applications' calendar files. |
| Boot Manager (LILO) | Sets up and modifies lilo. Click the Expert to display the /etc/lilo.conf file. Refer to lilo: The Linux Loader on page 1040. |
| Linux Kernel Configurator | Refer to "The KDE Linux Kernel Configurator" on page 1035. |
| Login Manager | Controls the appearance and functionality of the GUI login window. |
| Appearance | |
| Appearance Greeting | The message you see on the GUI login window. |
| Logo area | Determines what appears in the logo area of the GUI Login window. You can display nothing, a clock, or an image of your choice. |
| Logo | With Show logo selected in the Logo area, displays the logo that will be displayed. Double-click the logo to select a different logo. |
| Position | Specifies the location of the GUI login window on the screen. Choose Centered, or click Specify and enter the X and Y coordinates in pixels. |
| GUI Style | Specifies the GUI style that the Login Manager will use. |
| Echo mode | Specifies what KDE displays as you enter your password. |
| Locale, Language | The language KDE uses for titles, prompts, labels, and so forth. For more information, refer to "locale" on page 1477. |

## KDE Control Center: System Module (Continued)

| Font | Specifies the fonts used in the GUI Login window. Select *Greeting*, *Fail*, or *Standard* from the drop-down list, and specify the font you want to use by clicking *Change font*. The *Example* frame displays the font you choose. You can specify *antialiasing* (page 1454) if you like. |
| Background | These apply to the background while the login window is displayed. |
| Background | Choose a **Mode** of *Flat* for a single-color background; **Background Program** to run a program, in *Setup*, to generate the background; or one of the selections for a two-color background. Click *Color 1* or *Color 2* to select the Color window. View the effect of your choice in the picture of a monitor near the top of the window. |
| Wallpaper | Choose a wallpaper from the Wallpaper drop-down list or by clicking the **Browse** button. Specify how you want the wallpaper displayed from the **Mode** drop-down list. |
| Sessions | |
| Allow shutdown | After you click **Shutdown** on the Login window, you are given the choice of shutting the system or rebooting it. |
| Console | Specifies which users can shut down the system when they are logged in on the console. |
| Remote | Specifies which users can shut down the system when they are logged in remotely. |
| Commands | Specifies which commands are used to halt and reboot the system when a user chooses *Power off* or *Restart Computer* in the login window (Figure 2-3, page 32). |
| Lilo | Displays boot options when the user reboots from the Login window. |
| Show boot options | Displays the options for the **lilo** boot manager when you reboot/reboot the system. Each of the following text boxes must be correct for this feature to work. |
| Lilo command | The command that runs **lilo**. |
| Lilo map file | The name of the **lilo**-maintained file that contains the name and location of the kernel(s) that lilo boots. |
| Session types | Defines which session types are available from the GUI Login window. |
