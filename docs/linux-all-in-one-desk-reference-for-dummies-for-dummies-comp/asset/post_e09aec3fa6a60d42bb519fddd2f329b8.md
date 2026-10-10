
## 102 Setting Up Printers

2. **Select the type of printer — Local Printer or Network Printer — and click Next.**

The wizard prompts for more information about the printer's connection.

3. **Provide information about the printer's connection and click Next.**

For example, for a local printer, specify whether it's a parallel or USB printer. The wizard displays a screen from which you can select the printer's make, model, and a driver.

4. **Select your printer's make, model, and driver, as shown in Figure 3-17. Click Next.**

![](img/11709a8f88c8cd03868a929dc94c0e2b_127_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_127_1.png)

The wizard gives you the option of printing a test page and completing the printer configuration.

5. Click Finish to complete printer configuration.

After finishing printer configuration, the First Run Wizard continues with other configuration tasks.

## Managing DVDs and CD-ROMs

The GUI desktop makes using DVDs and CD-ROMs in Linux easy. Just place a DVD or a CD-ROM in the drive, and an icon appears on the desktop.

You can then access the CD or DVD by double-clicking the icon on the desktop.

To access the files and folders, you simply double-click the icons that appear in a GUI file manager window. In some Linux distributions, the GUI automatically opens the contents of a CD or DVD in a file manager window soon after you insert the CD or DVD in the drive.

If you see a DVD/CD-ROM icon, right-click that icon for a context menu. From that menu, you can eject the CD or DVD when you are done.

![](img/11709a8f88c8cd03868a929dc94c0e2b_128_0.png)

The Knoppix and MEPIS desktops show icons for each detected drive. To open a CD or DVD, simply click the icon for that drive. In SUSE, click the My Computer icon, and click the icon for the DVD/CD drive. Ubuntu opens the CD/DVD in a Nautilus window and also places an icon on the desktop. Xandros Desktop opens the CD/DVD in a Xandros File Manager window.

## Installing Other Software

The exact steps for installing software depend on the type of package in which the software is distributed. Most Linux software comes in either an RPM file or a Debian package file. The RPM files have an .rpm extension, and the Debian packages have a .deb extension.

Most distributions provide GUI installers to ease the process of installing new software packages. In this section, I provide a quick overview of adding software in Debian, Fedora Core, SUSE, and Xandros. You typically do not add software to Knoppix (or any other Live CD distribution) because Live CD distributions run CD-ROM.

![](img/11709a8f88c8cd03868a929dc94c0e2b_129_0.png)

Fedora Core and SUSE use RPM packages. Debian, MEPIS, Ubuntu, and Xandros are all Debian-based distributions, and as expected, they typically use Debian packages (also called DEB). However, both RPM and DEB packages can be installed in any Linux distribution.

### Installing software in Debian, MEPIS, and Ubuntu

The best way to manage software packages in Debian and Debian-based distributions such as MEPIS and Ubuntu is to use APT — the Advanced Packaging Tool — that you usually control through the `apt-get` command.

When you install Debian, one of the last steps is to configure the sources for APT. The *APT sources* are the Internet servers (both FTP and Web) where APT looks for software packages to download and install on your system. Assuming that APT is properly configured and that your system has a high-speed Internet connection, you can begin installing any package by typing the following command in a terminal window:

```
apt-get install pkgname
```

where *pkgname* is the name of the package that you want to install. If you do not know the package name, start by typing the following command in the terminal window:

```
apt-cache search keyword
```

where *keyword* is related to the package you want to install. For example, to search for a package that has the word *screenshot* in its description and also contains the word *KDE*, I would type the following. (I use *grep* to search the output for occurrences of the text *KDE*.)

```
apt-cache search screenshot | grep KDE
```

This command then prints the following line as the result:

```
ksnapshot - Screenshot application for KDE
```

This shows that the *ksnapshot* package is what I need. If this package was not yet installed, I could then install it by typing the following command:

```
apt-get install ksnapshot
```

That, in a nutshell, is how you can use the command-line tools to look for and install packages in Debian.

### Installing Other Software

![](img/11709a8f88c8cd03868a929dc94c0e2b_130_0.png)

Debian, MEPIS, and Ubuntu also come with a GUI package installer for APT called Synaptic Package Manager, which is quite intuitive to use. To try it, choose Applications->System Tools-> Synaptic Package Manager from the GNOME desktop in Debian. In MEPIS, choose Main Menu->System-> Synaptic Package Manager. In Ubuntu, choose Select System->Administration-> Synaptic Package Manager. (In Ubuntu, when prompted for a password, enter your normal user password because there is no root user in Ubuntu.)

After Synaptic Package Manager starts, it displays a Quick Introduction dialog box that tells you, briefly, how to mark packages for installation, upgrade, or removal, and how to get to the menu to perform these actions. After reading the Introduction, click Close to get rid of that dialog box.

If your package information is older than 48 hours, another dialog box prompts you to update the package information. Click Reload in that dialog box. Synaptic Package Manager then downloads the latest package information, closes the dialog box, and displays information about the packages in the main window, as shown in Figure 3-18.

![](img/11709a8f88c8cd03868a929dc94c0e2b_130_1.png)

> **Figure 3-18:** You can install and remove packages by using Synaptic Package Manager.

By clicking the categories on the left side of the Synaptic Package Manager window you can view lists of various categories of packages on the right side of the window. A box to the left of each package indicates whether the package is installed or not. If you click on the package name, Synaptic Package Manager displays information about the selected package in the lower-right side of the window.

To select a package for installation or removal, click the box to the left of its name and pick Mark for Installation or Mark for Removal from the pop-up menu that appears. If selecting a package for installation requires other packages, Synaptic Package Manager displays a dialog box with that information, and you can click Mark to install the required packages also. Mark as many packages as you want and click Apply on the toolbar to perform all marked actions.

### Installing software in Fedora Core

Most Fedora Core software comes in the form of RPM files. *An RPM file is basically a single package that contains everything — all the files and configuration information — needed to install a software product.*

From the GNOME desktop, use the Add or Remove Packages utility — a graphical utility for installing and uninstalling RPMs. Follow these steps:

1. **Choose System** *Applications* **Add/Remove Software.**
    - If you’re not logged in as *root*, a dialog box prompts you for the *root* password. The Add or Remove Packages utility starts and gathers information about the status of packages installed on your system. After it sorts through the information about all the installed packages, the utility displays the Package Management dialog box, which contains a list of all the packages. (See Figure 3-19.)

![](img/11709a8f88c8cd03868a929dc94c0e2b_131_0.png)

2. To install an uninstalled package group, select the check box to the left of that package group’s name. For partially uninstalled package groups, click the Details hyperlink that appears in a column to the right of the package name.
    - A dialog box appears with details of the packages in the package group.
3. In the dialog box, select the packages that you want to install or remove by clicking the names, and click Close to exit the dialog box.
    - You return to the Package Management dialog box, and if you added or removed any package, the Update button becomes active.
4. Click the Update button to update the packages based on any additions or removals you made in the lists of packages.

### Installing software in SUSE

In SUSE, follow these steps to install or remove software:

1. Choose **Main Menu**: YaST** to start the YaST Control Center shown in Figure 3-20.
    - The YaST Control Center displays categories of tasks on the left side and specific tasks for that category on the right side.
2. Click the Software category on the left side so that the right side shows the options for Software.
3. Click the Software Management icon on the right side (refer to Figure 3-20).
    - YaST displays a new window where you can search for software packages.

![](img/11709a8f88c8cd03868a929dc94c0e2b_132_0.png)
