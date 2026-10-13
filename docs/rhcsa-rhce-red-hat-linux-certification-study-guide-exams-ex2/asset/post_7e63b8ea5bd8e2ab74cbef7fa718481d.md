
> exam watch The Linux Loader (LILO) hasn't been supported by Red Hat for nearly a decade. In addition, while GRUB 2.0 is available, it is also not supported for RHEL 6, at least as of the initial release.

- The Install Boot Loader On /dev/sda option would install the bootloader on the master boot record of the noted hard drive. Unless another bootloader is installed, that is appropriate.
- The Use A Boot Loader Password can help secure the system. As you'll see in Chapter 5, without a bootloader password, anyone with access to the boot menu can access Linux with full administrative privileges just by booting into runlevel 1.
- The Boot Loader Operating System List specifies a list of detected operating systems. While you might see a second entry for an operating system such as Microsoft Windows in real life, RHEL 6 should be the only operating system installed here for the Red Hat exams.

While it's possible to add an entry from this menu for other operating systems, it won't work for other Linux installations on the same system. For that purpose, it's more effective to modify the GRUB bootloader configuration file directly after installation is complete.

While you may choose to set up a bootloader password, the defaults should be acceptable on any system where RHEL 6 is the only operating system installed on the local machine. Make any appropriate changes and click Next to continue.

## Wow, Look at All That Software!

There are over 2500 packages available just from the RHEL 6 installation DVD. That number does not include a number of packages available only through the Red Hat Network. With so many packages, it's important to organize them into groups. After configuring the GRUB bootloader, you'll see the options shown in Figure 1-13, which allows you to configure the local system to a desired functionality. The selection depends on your objective. If you're installing on a physical system to set up KVM-based virtualization, select Virtual Host. If you're setting up virtual guests (or other dedicated servers), select Basic Server. During a Red Hat exam, you'll be installing most additional software after basic operating system installation is complete. Other options are listed in Table 1-3. Depending on the rebuild distribution, the options may vary significantly.

## FIGURE 1-13

Functional installation options

![](img/9139201cfcaf4292284a0eed074928e5_40_0.png)

## TABLE 1-3 Installation Software Categories

| Category | Description |
|---|---|
| Basic Server | Installs basic packages for Red Hat as a server |
| Database Server | Includes MySQL and PostgreSQL database packages |
| Web Server | Sets up a system with the Apache Web server |
| Virtual Host | Configures a system with the KVM VM system |
| Desktop | Includes desktop productivity software |
| Software Development Workstation | Adds tools to modify and compile software |
| Minimal | Includes a minimal list of packages for the operating system |

![](img/9139201cfcaf4292284a0eed074928e5_41_0.png)

For a truly secure baseline in a production environment, consider the minimal installation. Fewer packages means fewer vulnerabilities. You can then add just the packages needed for the desired functionality. Any software that isn't installed can't be exploited by a cracker.

> In the world of Linux, the term "hacker" refers to good people who want to create better software. The term "cracker" refers to people who want to break into other systems with evil intent.

The repositories listed can be useful for additional server functionality. As suggested by their names, the unselected repositories shown in Figure 1-13 support the installation of software in a number of categories, including storage clusters, systems that require high availability, and systems that balance the load for high-traffic services. As these are Red Hat repositories, maintained by Red Hat, some third-party repositories may not duplicate the availability or functionality of some of the repositories shown in the figure.

If you want to redirect systems to local or internal repositories, to control the packages others install on their systems, click Modify Repository. That allows you to specify where the local system looks for new packages and updates.

![](img/9139201cfcaf4292284a0eed074928e5_41_1.png)

> Some groups of developers enable the installation of software not supported by Red Hat. Two examples can be found at http://atrpms.net and http://rpmrepo.org.

For the purpose of this chapter, retain the default Red Hat Enterprise Linux repository (or the defaults for a rebuild distribution such as CentOS/Scientific Linux). Make sure to select Customize Now; otherwise, you won't be able to follow along with the next section. Click Next to continue.

## Baseline Packages

In this section, you'll get a basic overview of what's available during the RHEL 6 installation process. During the exams, you may refer to one of these package groups with the Red Hat Add/Remove Software tool. You can also find a list of available package groups with the `yum grouplist` command. More information is available in Chapter 7.

Red Hat package groups are organized logically; for example, packages associated with a specific language can be found in the Languages package group. It's important to choose only the package groups you need. Fewer installed packages means more room for personal files, as well as the log files needed to monitor systems.

## Package Groups

This section includes the briefest possible overview of each of the package groups available during the RHEL installation process. As you can see from Figure 1-14, there are high-level groups in the left-hand pane, such as Desktops, and regular package groups in the right-hand pane, such as the X Window System. The details of the RPMs associated with each package group are stored in an XML file. To review that file, go to the RHEL installation DVD and read the compressed `*-comps-rhel6-Server.xml.gz` file in the `/repodata` directory.

For an example of the details within a package group, select Desktop and click Optional Packages. This opens the Packages In Desktop window shown in Figure 1-15. Compare this list to the aforementioned XML file. Mandatory packages aren't shown in the associated window, as their installation is required for the package group. As the XML labels suggest, default packages are selected by default; optional packages are not selected.

![](img/9139201cfcaf4292284a0eed074928e5_42_0.png)

## FIGURE 1-15

Red Hat Enterprise Linux Desktop package group details

![](img/9139201cfcaf4292284a0eed074928e5_43_0.png)

Take some time studying this screen. Examine the packages within each package group. You'll learn about the kinds of packages that are installed by default. If you don't add them during the installation process, it isn't the end of the world. You can still add them with the `rpm` and `yum` commands or the Add/Remove Packages tool described in Chapter 7.

If the XML file is too confusing, just make a note of the name of a package group. From that name, you can find a list of associated packages after installation is complete. For example, the following command identifies mandatory, default, and optional packages for the base package group:

```bash
$ yum groupinfo base
```

For the purpose of this book, I've created two different baseline installations. One baseline is suited as a host system for VMs; the other is suited to be installed in a VM. Both include a relatively minimal GUI installation, as most Linux administrators appreciate the convenience of multiple open command line consoles, side by side. To that end, I selected the following package groups during the installation process.

- Desktops – Desktop: Includes the basic GNOME Desktop Environment.
- Desktops – Fonts: Installs fonts that improve system readability in the GUI.
- Desktops – X Window System: Adds the server packages associated with the GUI.
- Applications – Internet Browser: Includes the Firefox Web browser.

The package groups fall into different categories; for example, to select the X Window System package group, I first highlighted the Desktops category in the left-hand pane. I could then select the X Window System package group in the right-hand pane.

In addition, for the physical host system configured for KVM-based VMs, I made sure the Virtualization package groups were included. They should be automatically included if you selected the Virtual Host system category earlier in the installation process.

Once desired packages are selected, click Next. Anaconda then proceeds to the installation process. When the process is complete, you'll see a final screen that confirms the installation, along with an option to reboot the system.

On the system used to write this book, I also installed the OpenOffice.org suite and The GIMP (The GNU Image Manipulation Program).

## On Reboot

When installation is complete, you'll see a final message to that effect, with an option to reboot the system. If you've installed RHEL 6 on a physical system, don't forget to eject or remove the boot disk and/or the installation DVD.

For RHEL 6 installed in a KVM-based VM, you'll need to change the boot device. If it isn't already open, click Applications | System Tools | Virtual Machine Manager. Enter the root administrative password if prompted, and double-click on the desired VM. Then change the boot device with the following steps:

1. In the window associated with the VM, click View | Details.
2. In the window that appears, shown in Figure 1-16, click Boot Options.
