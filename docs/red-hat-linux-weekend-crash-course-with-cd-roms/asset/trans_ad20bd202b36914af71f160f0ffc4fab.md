
others cannot guess easily. Typically, make the password at least eight characters long, include a mix of letters and numbers, and (for good measure) throw in some special characters such as + or *. Remember the password is also case sensitive.

Type the password on the first line and then reenter the password on the next line. Each character in the password appears as an asterisk (*) on the screen. Both entries must match before the installation program accepts the password. The installation program displays a message when it accepts the root password. After you type the root password twice, you might also want to add one or more user accounts.

To add a user account, fill in the Account Name, Password, and Full Name fields and then click the Add button. The new account information then appears in the table underneath the Add button. You do not have to add all the user accounts at this time. Later on, you can use the Linuxconf tool (which comes with Red Hat) to add more user accounts.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_61_0.png)

You must enter the root password before you can proceed with the rest of the installation. After you do so and add any other user accounts you need, click the Next button to continue with the installation.

## Configure password authentication

The installation program displays a screen from which you can configure the password authentication options. There are several options that you can enable or disable. Of these, the first two are already selected:

- **Enable MD5 passwords:** Select this option to enable users to use long passwords of up to 256 characters instead of the standard password that can be, at most, eight characters long. Note that MD5 refers to Message Digest 5, an algorithm developed by RSA, Inc. to compute the digest of the entire data of a message. Essentially, MD5 reduces a message to a digest consisting of four 32-bit numbers.
- **Enable shadow passwords:** This option causes the /etc/passwd file to be replaced by /etc/shadow, which only the super user (root) can read. This provides an added level of security.

You should use these default settings for increased system security. Click the Next button to proceed to the next configuration step.

## Selecting the Package Groups to Install

After you complete the key configuration steps, the installation program displays a screen from which you can select the Red Hat Linux package groups that you want to install. After you select the package groups, you can take a coffee break and the Red Hat installation program can format the disk partitions and copy all selected files to those partitions.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_62_0.png)

Red Hat uses special files called *packages* to bundle a number of files that make up specific software. For example, all configuration files, documentation, and binary files for the Perl programming language come in a Red Hat package. You use a special program called *Red Hat Package Manager (RPM)* to install, uninstall, and get information about packages. Session 23 shows you how to use RPM. For now, just remember that a package group is made up of several Red Hat packages.

Figure 3-5 shows the Package Group Selection screen with the list of package groups that you can elect to install. An icon, a descriptive label, and a button prefix identify each package group.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_62_1.png)

Figure 3-5
GUI screen from which you select the components to install

Some of the components are already selected, as indicated by the pressed-in buttons. These are the minimal set of packages that Red Hat recommends for installation for the class of installation (Workstation, Server, or Custom) you have chosen. You can, however, choose to install any or all of the components. Use the mouse to move up and down in the scrolling list and click the mouse on an entry to select or deselect that package group.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_63_0.png)

In an actual Red Hat Linux installation, you install exactly those package groups that you need. However, for the purpose of this crash course, choose many different package groups because you need them to go through all the sessions. Each package group requires specific packages to run. The Red Hat installation program automatically checks for any package dependencies and shows you a list of packages that are required but that you have not selected. In this case, you should install the required packages.

Because each package group is a collection of many different Red Hat packages, the installation program also gives you the option to select individual packages. If you select the item labeled Select individual packages that appears below the list in Figure 3-5 and then click the Next button, the installation program takes you to other screens where you can select individual packages. If you are installing Red Hat Linux for the first time, you really do not need to go down to this level of detail to install specific packages. Simply pick the components that you think you need from the screen shown in Figure 3-5. After you select the components you want, click the Next button to continue with the rest of the installation.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_63_1.png)

You can always install additional packages later on with the RPM utility program, described in Session 23.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_63_2.png)

## Completing the Installation

After you complete the key configuration steps and select the components to install, the installation program configures the X Window System. The installation program uses an X server with minimal capability that can work on all video cards. In this step, the installation program prepares the configuration file that the X server uses when your system reboots.

The installation program tries to detect the monitor and displays the X Configuration screen (see Figure 3-6) with the result, whether or not it succeeds.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_64_0.png)

### Figure 3-6

Result of detecting the monitor displayed in the X Configuration screen

If the installation program displays a wrong monitor or a generic one as the choice, you should enter a range of values for the two parameters that appear along the bottom of the screen:

- **Horizontal Sync** — the number of times per second that the monitor can display a horizontal raster line, in kilohertz (kHz). A typical range might be 30–64 kilohertz (kHz).
- **Vertical Sync** — how many times a second the monitor can display the entire screen, in Hertz (Hz). Also known as *vertical refresh rate*, the typical range is 50–90 Hertz (Hz).

Typically, the monitor’s documentation includes all this information. Other places to get information about your monitor include: your Microsoft Windows setup, your system’s Windows driver, your computer vendor’s Web site, or the Norton System Information tool.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_64_1.png)

Do not specify a horizontal synchronization range that is beyond the capabilities of your monitor. A wrong value can damage the monitor.

After selecting the monitor, the installation program tries to detect the video card and displays the result in a screen. The detected card appears as the selected item in a long list of video cards. If you know the exact name of the video card or the name of the video chipset used in the video card, select that item from the list.

On the same screen where you view and select the video card, you should also turn on the graphical login by clicking the button labeled Use Graphical Login. Then you get a graphical login screen when you reboot the system.

After you finish selecting X configuration options, click the Next button. The installation program displays an informative message telling you that a log of the installation is in the /tmp/install.log file. That file essentially lists all the Red Hat packages that are installed in your system. You can review the install log later on and keep the file for future reference. The content of the install log depends on the exact packages you choose to install.

Click the Next button to proceed with the installation. The Red Hat installation program formats the disk partitions and then installs the packages. As it installs packages, the installation program displays a status screen showing the progress of the installation with information such as the total number of packages to install, the number installed so far, an estimated amount of disk space needed, and an estimated time remaining to install. Formatting and installation both take a while.

After all the packages are installed, the installation program displays a screen that prompts you to insert a blank floppy into your PC's A: drive. This floppy is the emergency boot disk that you can use to start Red Hat Linux if something happens to the hard disk or you do not install the LILO.

Insert a blank floppy into your PC's A: drive and click the Next button. The installation program copies the Linux kernel and some other files to the floppy. After preparing the boot disk, the installation program displays a message informing you that installation is complete.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_65_0.png)

**When you insert a blank floppy into your PC's A: drive, this destroys all data on the floppy.**

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_65_1.png)

The message goes on to remind you to remove the floppy from drive A: before exiting the installation program. Do so, label the floppy appropriately, and save it for future use. Then click the Exit button to reboot your PC. When it finishes rebooting, you should get the Red Hat Linux graphical login screen. You are now all set to explore and learn Red Hat Linux.

