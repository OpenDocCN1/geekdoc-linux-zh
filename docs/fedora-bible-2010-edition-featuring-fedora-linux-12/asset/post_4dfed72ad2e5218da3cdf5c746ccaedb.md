
## Office and Productivity
- **Office and Productivity** — Installs software appropriate for a home or office personal computer or laptop computer. This includes the GNOME desktop (no KDE) and various desktop-related tools (word processors, Internet tools, and so on). Server tools, software development tools, and many system administration tools are not installed.
- **Software Development** — Similar to Office and Productivity installation but adds tools for system administration and software development. (Server software is not installed.)
- **Web Server** — Installs the software packages that you would typically need for a Linux Web server (in particular, Apache Web server and print server). It does not include many other server types by default (FTP, DNS, DHCP, mail, SQL, or news servers). The default server install also includes a GUI (GNOME only).

> NOTE: Unlike earlier versions, recent versions of Fedora no longer offer an Everything install type or a Minimal install type.

A recent feature in Fedora lets you select software repositories outside of Fedora, from which you can select packages to install during the initial Fedora installation. Use the check box to be able to install from other software repositories. Select Add additional software repositories to add other repositories (such as RPMfusion.org, described in Chapter 5). Then, select the Customize Now button if you want to further specifically select which packages in the selected tasks are installed. This lets you see which categories from each task and which packages within those categories are selected to be installed. It also lets you add or remove package selections. Note that packages from multiple repositories can appear in the same category (for example, you would see games from both Fedora and RPMFusion packages appearing in the Games category if the RPMFusion repository were enabled).

Select the install classes you want, and then choose Customize Now to see the packages to be installed (based on install categories and package groups). Unselecting the major categories can get you a pretty good minimal install if you like to build from a bare-bones install. In the following step, the procedure will continue as though you had chosen Customize Now.

13. **Customize categories.** If you selected Customize Now, you are presented with categories of software on the left side of the screen and package groups on the right side. Select a category to see which groups it contains. Select a group and click the Optional packages to see which optional packages are available in that group and which are selected to be installed. Categories include:
    - **Desktop Environments** — The GNOME desktop environment is selected by default. KDE is the other main choice. While not on the install DVD, SUGAR and XFCE are the other available desktop environments. (Desktop environments are described in Chapter 3.)
    - *Applications* — This category includes packages of office applications, games, sound and video players, Internet tools, and other applications. (Many of these applications are described in Chapters 5 through 8.)
    - *Development* — General and specialized software development tools are included in packages in this category.
    - *Servers* — Packages in this category are for Web, mail, FTP, database, and a variety of other network server types.
    - *Base System* — Contains basic system administration tools, many common utilities, and support for basic system features (such as X Window System, Java, and Legacy software support).
    - *Languages* — Packages containing support for multiple languages are contained in this category.

After you have chosen the packages you want to install, select Next to continue. The installer will take some time to check for dependencies among the packages you selected.

14. **Installation.** A screen tells you that Fedora is being installed. Now the packages are installed. This typically takes from 20 to 60 minutes to complete, although it can take much longer on older computers.

For live CD installation, the live CD image is simply copied to your hard disk.

15. **Finish installing.** When you see the Congratulations screen, you are done. Eject the DVD or CD and click Reboot.

Your computer will restart. If you installed GRUB, you will see a graphical boot screen that gives you several seconds to press a key to view and/or change the bootable partitions. After that, your Fedora installation should boot.

The first time your system boots after installation, Fedora Firstboot runs to do some initial configuration of your system. The next section explains how Fedora Firstboot works.

## Running Fedora Firstboot

The first time you boot Fedora, after it is installed, Fedora Firstboot runs to configure some initial settings for your computer.

> NOTE: Firstboot runs automatically only if you have configured Fedora to boot to a graphical login prompt. To start it from a text login, log in as root and type the following from a Terminal window:
>
> # rm /etc/sysconfig/firstboot
> # /usr/sbin/firstboot

The first screen you see is the Welcome screen. Click Forward to step through each procedure as follows:

- *License Information* — Read the Fedora License information about the GPL.
- *Create User* — For your daily use of Fedora, you should have your own user account. You should typically log in with this user name (of your choosing) and use only the root user to perform administrative tasks. In the first of the four text boxes on the screen, type a user name (something such as jparker or alanb). Next, type your full name (such as John W. Parker or Alan Bourne). Then type your password in the Password text box and again in the Confirm Password text box. Click Forward. Firstboot will warn you if your password is considered too weak and therefore easier to break.
  - If some form of network authentication is used, such as LDAP, Kerberos, or SMB authentication, you can click the Use Network Login button. See the “Enabling Authentication” sidebar for information on choosing different authentication types.
- *Date and Time* — Set the date and time, or click to synchronize date and time over the network to enable the network time protocol to keep your system clock properly set. Click Forward.
- *Hardware Profile* — The Smolt hardware profiler runs to gather and display all kinds of information about your hardware. Select Send Profile if you agree to have this information sent to the Fedora Project. Firstboot is complete. Click Finish to continue. You may need to reboot. See Chapter 3 for a description of how to log in to Fedora and start learning how to use Linux.

When Fedora starts up the next time, it will boot up normally to a login prompt. A graphical boot screen is displayed (instead of a scrolling list of services starting up).

## Enabling Authentication

In most situations, you will enable shadow passwords and SHA512 passwords (as selected by default) to authenticate users who log in to your computer from local passwd and shadow password files. To change that behavior, you can select the Use Network Login button during the Create User setup during Firstboot.

The shadow password file prevents access to encrypted passwords. SHA512 is an algorithm used to encrypt passwords in Linux and other UNIX systems. It replaces an algorithm called crypt, which was used with early UNIX systems. When you enable SHA512 passwords, your users can have longer passwords that are harder to break than those encrypted with crypt. You can also use MD5 or SHA256 for encrypting passwords, although these methods are less secure.

If you are on a network that supports one of several different forms of network-wide authentication, you may choose one of the following features (on the Authentication tab):

- *Enable Kerberos Support* — Tick this check box to enable network authentication services available through Kerberos. After enabling Kerberos, you can add information about a Kerberos Realm (a group of Kerberos servers and clients), KDC (a computer that issues Kerberos tickets), and Admin server (a
