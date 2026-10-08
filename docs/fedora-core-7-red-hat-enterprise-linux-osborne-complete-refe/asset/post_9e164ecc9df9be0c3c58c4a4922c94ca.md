
check box for gFTP. In multimedia (Applications | Sound and Video) the popular K3b CD/DVD burning application also is not selected. This is just one of the popular applications you will have to select in the Multimedia optional panel. Other packages you may want to include are Thunderbird (Applications | Graphical Internet) and Samba configuration (Servers | Windows File Server).

You can no longer just install everything or even everything in a category. Users are becoming more and more specialized in their tasks, and there is no sense in installing software they will never need. The initial install becomes more like a base collection that users can then add to as they want. This reflects the massive expansion of Linux software packages now available. The Fedora Extras repository along with additional repositories like freshrpms.net now provide far more software than could possibly be included in a few disks.

Many software packages require that other software packages also be installed. This is called a dependency. If you don't have these already selected for installation, they will be selected for you.

After selecting your software, the next screen lets you start the installation. This is your last chance to back out of the installation. You can press the Back button to reselect packages, or simply press your system's reset button to end the install process, leaving your original system untouched. Once you click the Next button, if you chose to format partitions, they will be formatted.

The packages are then installed, showing each package as it is installed and the progress of the installation. (For the Fedora DVD-ROM, the install program detects all packages as residing on the single DVD-ROM. If you are using CD-ROMs instead, you will be prompted when to install the next CD-ROM. The current one will automatically be ejected for you.) When the installation finishes, a postinstall process will complete. You are then usually given the option to create a boot disk. You can use this disk to access your Linux system should your hard disk boot somehow fail.

## Finishing Installation

Once your installation is finished, you can click the Reboot button to reboot. Be sure to remove the install or boot DVD/CD-ROM. If you booted from a CD, your CD will be ejected before rebooting. If you booted directly from the CD-ROM, you may want to change your boot sequence in your BIOS back to your original settings.

## GRUB on Restart

When you reboot, a GRUB boot loader menu will be displayed listing Linux and other operating systems you specified, such as Windows. Use the arrow keys to move to the Linux entry; if it is not already highlighted, and press ENTER. The screen will appear for a few seconds and then run the default operating system. If you want to remain at the menu display until you specifically choose a system, you can press any key when GRUB starts up.

For graphical installations, some displays may have difficulty running the graphical start up display known as the red hat graphical boot tool, rhgb. If you have this problem, you can edit your Linux GRUB entry and remove the rhgb quiet terms at the end of the Grub start up line. Press the e key to edit a Grub entry. Your system will start up initially using text display for all the start up tasks, then shift to the graphical login. The Linux GRUB line will look something like this.

```
kernel /vmlinuz-2.6.20-1.3094.fc7 ro root=/dev/fedora7/fedora70 rhgb quiet
```

### Setup

The first time you start up Fedora, the Setup Agent is run. This agent will help you perform basic configuration of your system, letting you set the date and time, configure your display (graphics card and monitor), and configure your sound card, as well as set up user accounts. The different steps will be listed on a side pane, with an arrow progressing through each one as you complete a task. For Fedora, you will be initially asked to approve the GNU General Public License for this distribution. The steps are listed here:

- License Agreement
- Firewall
- SELinux
- Date and Time
- Hardware Profile
- Create User
- Sound Card
- Finish Setup

### Firewall and SELinux

The Firewall Configuration screen then lets you create basic default levels of network security. A pop-up menu lets you enable or disable the firewall (it is enabled by default). You can also specify services you may be running that permit others to access to your system, such as Web or FTP services. One service you may want to include is Samba to allow browsing of your Samba shares. The Other Ports entry expands to a panel where you can add ports that should be allowed access, like ports you want to use for bittorrent.

The next screen lets you configure Security-Enhanced Linux (SELinux). SELinux provides a very high level of security administration. You have three settings: enforcing, permissive, and disable. Enforcing is the default, but Permissive may be the better choice until you are sure how you want SELinux configured in detail. The Enforcing setting will deny access by unauthorized users to files and applications. If your security policy is not accurately configured, access could be denied to valid users. At the Permissive level you can see how SELinux performs and adjust its configuration appropriately. SELinux may not be fully compatible with older software.

### Date and Time

The Date And Time Configuration panel will automatically probe for the date and time, displaying the date on a calendar and the time in hours, minutes, and seconds. You can easily change any entry with the click of a button. You can also choose to use the Network Time Protocol, which will obtain the time automatically from a time server on the Internet, making sure your time is always correct. You can choose from server pools listed, for instance, **0.fedora.pool.ntp.org**. The advanced options let you synchronize before using a service or use a local time source.

> **Tip**
> The display is automatically detected during installation. You can later configure it after the install process is completed. Should you have an ATI or Nvidia graphics card on your system, you can later download and install its Linux driver from rpm.livna.org (see Chapter 4).

#### Hardware Profile Reporting

The Smolt hardware profile screen lets you allow your hardware configuration to be registered with the Fedora project, so statistics on hardware compatibility can be compiled directly from users. See *fedoraproject.org/wiki/Releases/Smolt* for more information.

#### Create User

The Create User panel then lets you create a normal user account. You should have at least one, other than root. A dialog box is displayed with entries for the username, the user’s full name, the password, and the password confirmation. Once you have entered the information and clicked **Next**, the new user will be created.

You can also select LDAP, Windbind, Hesiod, or NIS to configure a user’s network login process. Click the Use Network Login button. Here you can configure the servers. This starts up system-config-authentication. Use this also if your network supports the authentication server. Three panels are displayed: User Information, Authentication, and Options. On the User Information panel, you can configure LDAP, Kerberos, Windbind, and SMB (Samba) authentication. On the Authentication panel, you can enable and configure support for each, specifying NIS, LDAP, Kerberos, or SMB servers that your network may use. The options panel lists support for password authentication.

#### Sound Configuration

On the Sound panel, your sound card will be automatically detected and configured. You can click a button to test the sound. You also have mixer options for dynamic keys and to disable software mixing. If you have more than one device, they will all be displayed with their own panels.
Click the **Finish** button to finish your setup.

### Login and Logout

The Setup Agent then concludes and the login prompt or the login screen will appear. A graphical install will use the login screen. You can then log in to your Linux system using a login name and a password for any of the users you have set up. An entry box will be displayed in the middle of the screen and labeled User. Just type in your user name and press **ENTER**. The label of the box will then change to password and the box will clear. Then enter your password and press **ENTER**.

If you log in as the root user, you can perform administrative operations, such as installing new software or creating more users. To log in as the root user, enter **root** at the entry box and the root user password in the entry box when the password label appears.
