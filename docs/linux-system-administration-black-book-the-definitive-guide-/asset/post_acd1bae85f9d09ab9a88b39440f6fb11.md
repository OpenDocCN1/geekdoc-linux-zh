
## Upgrade Option

The Upgrade option is not actually an installation class. It is an option that allows you to upgrade a current installation instead of installing a new version of the operating system and its associated packages. However, this option is not always the smoothest way to update a system. Sometimes it is better to use the RPMs (Red Hat Package Manager formatted files, as discussed in Chapter 4) provided by Red Hat and upgrade the system manually.

## GNOME Vs. KDE

Red Hat 6.2 and later versions offer the option of installing either the GNOME (GNU Network Object Model Environment) or KDE (K Desktop Environment) GUI early on in the installation process if you use a Workstation class. If you use the Custom class, choosing which GUI involves looking at the list of overall packages available for installation. GNOME is the GUI selected by default. If you want to use KDE, deselect GNOME and select KDE. You also have the option of installing both GUIs.

Both desktop environments are open source and freely available for use. They both come with suites of applications designed to automate everyday end-user and system-administration tasks. There is a slight difference in how the organizations behind these two environments deal with software developers, so be sure to read their Web sites thoroughly if you intend to develop tools or applications for GNOME (www.gnome.org) or KDE (www.kde.org).

> Choosing which GUI to use often involves several questions:

- Which look and feel most appeals to you?
- Which desktop environment’s **philosophy** do you prefer?
- Are specific tools you want or need available in only one of the environments?

For more information about Linux and GUIs, see Chapter 6.

## Other Distributions

There are many Linux distributions available in addition to Red Hat. This book focuses on Red Hat-specific items, but most of the content will work with any Linux flavor. Only small adjustments in file locations or tools may be necessary. In fact, a number of distributions are built on top of Red Hat. A list of some of these is outlined in Table 1.4.

Red Hat is, of course, not the only Linux distribution out there. There are new Linux distributions being introduced on a regular basis all over the world. Table 1.5 lists a number of the available distributions and where you can find out more about them.

### Table 1.4 Popular Linux distributions based on Red Hat Linux.

| Name | Home Page | Architectures |
|---|---|---|
| DLD | www.delix.de | Intel x86 and compatible |
| LinuxPPC | www.linuxppc.org | PPC (Power PC) machines (see Web site for full listing) |
| Mandrake | www.linux-mandrake.com | Intel x86 and compatible |

### Table 1.5 Other popular Linux distributions.

| Name | Home Page | Architectures |
|---|---|---|
| Caldera | www.caldera.com | Intel x86 and compatible |
| Debian | www.debian.org | DEC Alpha, Intel x86 and compatible, Motorola 680x0, SPARC |
| LinuxPPC | www.linuxppc.org | PPC (Power PC) machines (see Web site for full listing) |
| Mandrake | www.linux-mandrake.com | Intel x86 and compatible |
| Slackware | www.slackware.com | Intel x86 and compatible |
| SuSE | www.suse.com | Intel x86 and compatible, DEC Alpha |
| TurboLinux | www.turbolinux.com | Intel x86 and compatible |

# Immediate Solutions

## Getting New Versions Of Red Hat Linux

You can always find out what the latest and greatest of Red Hat’s releases are by going to **www.redhat.com**. The boxed set is available for purchase through them as well as in stores that carry computer software. You can also download the contents of the installation CD and/or source CD from **ftp://ftp.redhat.com** if you have a sufficiently large bandwidth to make it worthwhile. For inexpensive Red Hat CDs that come with user manuals in digital form (without technical support), visit:

- www.cheapbytes.com
- www.linixmall.com

## Updating Your System Through Red Hat

Red Hat continuously makes updates available for its distribution. Some of these updates come from teams working on packages not written by Red Hat. Once the patches or new programs arrive at Red Hat, the programming team tests them and compiles RPMs that will add the new functionalities smoothly to the user’s systems. Important updates include security fixes as holes are discovered. Keeping abreast of security issues is covered in detail in Chapter 9.

One way to keep up to date with Red Hat updates is to join the Red Hat Announce mailing list. To join this list, do the following:

1. Open a blank email.
2. Address it to **redhat-announce-list-request@redhat.com**.
3. Put the word “subscribe” in the subject line.
4. Leave the body blank.
5. Send the email.
6. Respond to the email as required, confirming that you want the subscription.

It is not necessary, however, to join the mailing list. All updates are posted to the FTP server (**ftp://ftp.redhat.com**) and its mirrors. The directory name is based on the version number and architecture. For example, if the version is Red Hat Linux 6.2 and the architecture is Intel x86 and equivalent, the directory is /pub/redhat/updates/6.2/i386. In Chapter 20, you will learn how to write a shell script that automatically checks for and fetches new updates, and notifies you that they have arrived.

> **TIP:** Updates are also made available at the home sites for most of the tools you use in Linux, such as GNOME. Utilizing these requires you to be a little more careful of dependencies and other such issues, but many system administrators like to use items directly from the source when they want to keep up with the latest versions.

# Navigating GNOME

If you chose the GNOME GUI during the installation process, once you log in you are faced with a screen containing a number of windows that open automatically. Clear these windows out of the way for now by either clicking on OK in the dialog boxes, or by clicking on File Close or File Exit.

Once the initial items are cleared off the screen, GNOME initially looks like what is shown in Figure 1.1.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_38_0.png)

Figure 1.1 The initial GNOME screen.

## Configuring The GUI

To configure the GNOME GUI, do the following:

1. Boot the machine.
2. Log into the account containing the GUI settings you want to configure.
3. If the Linux box does not automatically go into the GUI, type “startx” to start it.
4. Look at the taskbar on the bottom of the screen and locate the toolbox icon shown in Figure 1.1.
5. Click on the toolbox icon to open the Control Center, as shown in Figure 1.2.
6. Click on the menu item corresponding to the aspect you want to configure. For example, to configure the environment’s background, click on the Background option under the Desktop menu (see Figure 1.3).
7. Choose the settings as you see fit.
8. The set of buttons (Try, Revert, OK, Cancel, and Help) at the bottom of the screen in Figure 1.3 are at the bottom of every Control Center option. When you have selected the new settings that you want to use, click on the Try button.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_39_0.png)

Figure 1.2 The GNOME Control Center.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_40_0.png)

Figure 1.3 The GNOME Control Center Background configuration option.

9. If the settings are acceptable, click on OK to close the dialog box or proceed to the next Control Center option. Otherwise, click on Revert to return to the previous settings.

| Related solutions: | Found on page: |
|---|---|
| Finding GUI Components Online | 162 |
| Adding A Window Manager | 162 |
| Adding A Theme | 164 |
| Changing Desktop Environments | 167 |

## Opening Programs

To open the file system navigator used in the GNOME GUI, do the following:

1. Boot the machine.
2. Log into the account containing the GUI settings you want to configure.
3. If the Linux box does not automatically go into the GUI, type “startx” to start it.
4. Look at the taskbar on the bottom of the screen and locate the footprint icon shown earlier in Figure 1.1.
5. Click on the footprint icon to pull up the GNOME menu shown in Figure 1.4.
