
yast --mask install --autoexit
This will automatically open the installation main menu and return to the command line on exit.

| Installation | YaST Version 1.07 -- (c) 1994-2000 SuSE GmbH |
|---|---|
| Logfile: | Load configuration |
| Save configuration |
| Change/create configuration |
| Check dependencies of packages |
| What if? |
| Start installation |
| Index of all series and packages |
| Package information |
| Install packages |
| Delete packages |
| Main menu | |

Figure 85. YaST: package installation main menu

SuSE Linux offers a choice of software configurations. These contain a list of
selected software packages to fit a certain need. Select Load configuration
to load a predefined configuration.

80 Linux System Administration and Backup for IBM @server xSeries and Netfinity

# Installation YaST Version 1.07 -- (c) 1994-2000 SuSE GmbH

| | | | |
|---|---|---|---|
| [ ] SuSE Almost everything. | 1859 - 7.25 G |
| [ ] SuSE Development system. | 452 - 1.98 G |
| [ ] SuSE D2 base system | 93 - 202.7 M |
| [ ] SuSE Games | 519 - 1.82 G |
| [ ] SuSE Gnome system. | 425 - 1.61 G |
| [ ] SuSE KDE system. | 683 - 1.61 G |
| [ ] SuSE Minimum system. | 359 - 1.47 G |
| [ ] * SuSE Multimedia system. | 87 - 158.7 M |
| [ ] SuSE Network oriented system. | 464 - 1.6 G |

| F1=Help | | F2=Description | | F9=Floppy |
|---|---|---|---||
| < Add | | Replace | | Abort |

![](img/4e6a76e57a4105be55d8a1cc0750b023_92_0.png)

You can now add the files from your current configuration, or you can replace it with one of these configurations. If you replace a configuration, all currently installed packages that are not part of the selected configuration will be marked for deletion! Press Esc to return to the main menu.

To add packages to or remove packages from your current configuration, select Change / create configuration. This will open the Series window in Figure 87.

# Series selection YaST Version 1.07 -- (c) 1994-2000 SuSE GmbH

| Series | | |
|---|---|---|
| Documentation | [ 144.7 M ] |
| Emacs | [ 31.7 M ] |
| Emulators | [ 0 B ] |
| Games and more | [ 1.9 M ] |
| GNOME - GNU Object Model Environment | [ 0 B ] |
| All Graphics | [ 59.9 M ] |
| Amateur Radio (AX.25, CW, Logs, etc.) | [ 0 B ] |
| KDE - K Desktop Environment (version 2) | [ 0 B ] |
| K Desktop Environment | [ 76.8 M ] |
| KWP Applications | [ 6.5 M ] |
| Network-Support (TCP/IP, UUCP, Mail, News) | [ 355.3 M ] |

| device-name partition | total | used | free | free% | mount-point |
|---|---|---|---|---|---||
| /dev/sda6 | Linux | 1.85 G | 1.12 G | 753.3 M | 39% | / |
| /dev/sda5 | Linux | 5.5 M | 325.0 K | 5.2 M | 94% | /boot |

| F1:Help | F4:Resorting | F5:Dependencies | F10=Esc-Exit |

All software packages are categorized into different series. Choose your category and press Enter to see all packages belonging to this series.

# Package selection - Series n YaST Version 1.07 -- (c) 1994-2000 SuSE GmbH

| | | | |
|---|---|---|---||
| [ ] acmnrp | NNTP Proxy in Java | <F3>=200 |
| [ ] amanda | Network Disk Archiver | Mount point |
| [ ] apache | The Apache Web Server | Free |
| [ ] archive | Where do I find what? | 812.0 M |
| [ ] authd | The Apache auth_ldap Module | /boot |
| [ ] autofs | A kernel-based automounter | 3.4 M |
| [ ] backend | Load balancing for the Apache web server | .../adm |
| [ ] bind | Name Server Utilities (old version) | 0 B |
| [ ] bind9 | BIND9 (new version) | | |
| [ ] bindutil | Utilities to query and test DNS | | |
| [ ] bing | Point-to-point bandwidth measurement tool | | |
| [ ] bitchx | An IRC client | | |
| [ ] bookmail | Bukmail | | |

Version: 8.2.3
Package Size: installed 2.9 M (compressed 998.0 K)
The new named author examples. The support utilities nslookup, dig,
dnsquery and host are found in the package bindutils. Documentation on setting
a name server can be found in /usr/share/doc/SuSE/packages/bind

```
F1=Help F2=Description F5=Dependencies F18=Ok Fsc=Abort
```

Figure 88. YaST: To select a package for installation/update, press the Spacebar or Enter. This will toggle the status of the selected package. The indicator in the first column displays the current status:

| Indicator | Package status |
|---|---|
| [ ] | Package is not installed and not selected for installation |
| [X] | Package is marked for installation |
| [i] | Package is already installed |
| [R] | Package is installed and will be replaced / reinstalled |
| [D] | Package is installed and marked for deletion |

If you want to change the package status of multiple packages at once, press Shift+A (see Figure 89).

Chapter 4. SuSE Linux basic system administration 83

![](img/4e6a76e57a4105be55d8a1cc0750b023_95_0.png)

After you have made your choice, press F10 to return to the series selection.
You can now select or remove packages from other series, or press F10 once more to return to the software configuration main menu. If you made any modifications to your current software configuration, you can start the actual installation or removal of packages by selecting Start Installation. If you want to verify which packages will be installed, removed or replaced, select
What if...

![](img/4e6a76e57a4105be55d8a1cc0750b023_95_1.png)

84 Linux System Administration and Backup for IBM @server xSeries and Netfinity

Click Continue to return to the main menu. If you are satisfied with your selection, select Start installation. YaST will now check on which CD the necessary packages are located and prompt you for the respective CD. After the packages have been installed, you will return to the main menu shown on page 85. You can now add or remove packages. If you want to save configuration to floppy or hard disk, depending on your needs, return to the YaST main menu by selecting Selection.

## 4.2 Package management using RPM

Package management can also be done with the Red Hat package manager (RPM). The following table shows some of the frequently used commands.

| Command | Description |
|---|---|
| rpm -q <package> | If installed, check version and build number |
| rpm -qi <package> | Obtain some more information about installed package |
| rpm -qa | List all installed packages |
| rpm -qf <filename> | Determine the package that <filename> belongs to |
| rpm -Uv <package>.rpm | Update/Install the package.rpm showing a progress bar |
| rpm -F -v *.rpm | Update all installed packages using the files in the current directory |
| rpm --help | Get some help about the different options |

> > Note
run SuSEconfig afterwards! Some packages require post-installation maintenance. More information and options about RPM can be found in the manual page (man rpm), the RPM how-to
(less /usr/share/doc/howto/en/RPM-HOWTO.gz) and on the RPM Web site at http://www.rpm.org. You can also display a short overview by running
rpm --help.

## 4.3 User and group administration using YaST

Linux is a multi-user operating system. To differentiate between the various users, each user has to log in with a unique user name and password. Each user belongs to a primary user group, but they can also be a member of other groups (up to 16). Each user is named with a user ID (UID), which is also unique throughout the system. The same applies to user group names and IDs (GIDs).

Usually each user has a personal home directory. This is space on the file system (usually a directory below /home/username) that belongs to a person and where the person can store their personal files. Other users generally have no access to the files stored in another user's home directory.

You should carefully consider adding groups before adding users. Sometimes there are concerns about restricting access to some parts of the user system. You can do this by creating separate groups to control access to various files and filesystems. Also if you are going to be a system with many users, you should create separate groups divided by what they are on the system.

Another concern in setting up users and groups is that you may want to share files with other systems. This can be done by CD-ROM, tape, diskette or similar device. You can use the network to share information with NFS,
