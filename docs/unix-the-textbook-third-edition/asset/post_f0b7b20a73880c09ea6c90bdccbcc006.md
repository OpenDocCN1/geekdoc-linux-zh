
groups are you going to establish at installation, and how are you going to manage groups in a post installation environment?

4. Who will be responsible for the nine systems administration tasks listed previously? For example, this will influence your disk management tasks concerning file systems for users and projects, according to the data storage model you employ.

5. What kind of software tools do you want to include for the kinds of tasks you and your user base will be doing? For example, during installation, you are able to add packages on top of the default package installation to help accomplish those tasks. How are the user groups established in item 3 going to have access privileges to this software? What are your policies with respect to group access to software tools, and how do you enforce this policy?

6. What kind of GUI windowing system do you want to install with the system? You have a choice at installation of KDE4, Gnome, and others, and your previous experience and preferences with a particular style of desktop environment can be implemented at installation. Will you be doing a server install, based on your use case? A server install, and the management of a server system, involves another whole universe of considerations and design decisions.

## EXERCISE 23.1

Make a detailed listing on paper of your answers to these six questions before you begin to install your operating system. Then, read through the following sections showing the procedures for actual installation, and for each of your answers, determine ahead of time how you will proceed. This exercise is meant to serve as a "dry run" through any particular path you might take through the installation process.

## 23.2.2 GUI Install of PC-BSD

The most efficient, and patented, way to install PC-BSD on your computer is to follow the installation instructions in the PC-BSD handbook for the release of the software you want to install. Practically speaking, you can proceed through the installation from start to finish in a very intuitive manner, without using the handbook. Then, once the system is installed, you can consult the handbook, which is opened via clicking on an icon on the KDE4 desktop, for further detailed descriptions of the GUI installation process. In addition, versions of the PC-BSD handbook are available online for earlier releases of the software, and the general process of doing a GUI installation has not changed considerably since the earlier releases. This may change somewhat in later releases of the software, but certainly will not detrimentally affect using a purely intuitive initial installation scenario.

## EXERCISE 23.2

Why would it be dangerous to do a full disk install of a new installation on a disk that has legacy archived user data on it?

6. Begin the installation by clicking on the Install Solaris icon. The Welcome screen will open.

The list on the left side of the window lists the following steps that you will follow to configure the system before installing the OS:

- a. Configure the root disk where the OS will be installed (sometimes called the boot disk)
- b. Set the time zone
- c. Create a user login account
- d. Begin the installation

7. Click on the Next button and the Disk Discovery window will appear. Select whether you will be installing the OS onto a local disk (internal or external disk) or an Internet Small Computer System Interface (iSCSI) disk accessible over the network using the iSCSI protocol. Select Local Disks.

8. Click on the Next button and the Disk Selection window will appear. You will be using the whole disk for the Solaris OS, so make that selection and click Next.

> Note: This procedure will erase everything on the disk.

9. The Time Zone screen appears. Select the correct region, location, time zone, date, and time, then click Next.

10. The Users screen will appear. On this screen, you will create a user account and enter a computer name for this system. When installing the OS using the Live Media installer, you must create a user account. This will be your login account. After the installation, you will not be allowed to log in directly as root.

When creating a user account, follow these rules:

- The username cannot be root.
- The username must start with a letter.
- The username may contain alphabetical characters, numbers, underscores ( _ ), periods ( . ), or hyphens ( - ).

After the installation using Live Media is complete and the system has been rebooted, the default behavior is to not allow root to log in from the login screen. You will first log in using the user account that was created during installation, and then, if desired, switch to the root account when root privileges are required. See Chapter 2, Figures 2.2 and 2.3, to see the appearance of the login screen dialog boxes.
