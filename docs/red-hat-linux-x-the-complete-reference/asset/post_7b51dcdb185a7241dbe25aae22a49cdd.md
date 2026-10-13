
## GNOME Directories and Files

Red Hat installs GNOME binaries in the /usr/bin directory on your system. GNOME libraries are located in the /usr/lib directory. GNOME also has its own include directories with header files for use in compiling and developing GNOME applications, /usr/include/libgnome and /usr/include/libgnomeui (see Table 6-4). The directories located in /usr/share/gnome contain files used to configure your GNOME environment.

Table 6-4: GNOME Configuration Directories

| System GNOME Directories | Contents |
|---|---|
| /usr/bin | GNOME programs. |
| /usr/lib | GNOME libraries. |
| /usr/include/libgnome | Header files for use in compiling and developing GNOME applications. |
| /usr/include/libgnomeui | Header files for use in compiling and developing GNOME user interface components. |
| /usr/share/gnome/apps | Files used by GNOME applications. |
| /usr/share/gnome/help | Files used by the GNOME Help system. |
| /usr/share/doc/gnome* | Documentation for various GNOME packages, including libraries. |
| /etc/X11/gdm/gnomerc | GNOME configuration file invoked with the GNOME Display Manager (GDM). |
| /etc/gconf | GConf configuration files. |
| .gnome, .gnome2 | Hold configuration files for the user's GNOME desktop and GNOME applications. Includes configuration files for the panel, background, MIME types, and sessions. |
| .gnome-desktop | Directory where files, directories, and links you place on the desktop will reside. |
| .gnome2_private | The user's private GNOME directory. |
| .gtkrc | GTK+ configuration file. |
| .gconf | GConf configuration database. |
| .gconfd | GConf gconfd daemon management files. |
| .nautilus | Configuration files for the Nautilus file manager. |

### GNOME User Directories

GNOME sets up several hidden directories for each user in their home directory that begin with .gnome and include a preceding period in the name: .gnome and .gnome2 hold files used to configure a user's GNOME desktop and applications. Configuration files for the panel, MIME types, and sessions, among others, are located here. Configuration files for particular GNOME applications are kept in the subdirectory apps. The .gnome-desktop directory holds any files, folders, or links the user has dragged to the desktop. .gtkrc is the user configuration file for the GTK+ libraries, which contains current desktop configuration directives for resources such as key bindings, colors, and window styles.

### GConf

With GNOME 2.0, GNOME officially implements GConf to provide underlying configuration support. GConf corresponds to the Registry used on Windows system. It consists of a series of libraries used to implement a configuration database for a GNOME desktop. This standardized configuration database allows for consistent interactions between GNOME applications. GNOME applications that are built from a variety of other programs, as Nautilus is, can use GConf to configure all those programs according to a single standard, maintaining configurations in a single database. Currently the GConf database is implemented as XML files in the user's .gconf directory. Database interaction and access is carried out by the GConf daemon, gconfd.

## Chapter 7: The K Desktop Environment: KDE

### Overview

The K Desktop Environment (KDE) is a network-transparent desktop that includes the standard desktop features, such as a window manager and a file manager, as well as an extensive set of applications that cover most Linux tasks. KDE is an Internet-aware system that includes a full set of integrated network/Internet applications, including a mailer, a newsreader, and a Web browser. The file manager doubles as a Web and FTP client, enabling you to access Internet sites directly from your desktop. KDE aims to provide a level of desktop functionality and ease of use found in Mac OS and Windows systems, combined with the power and flexibility of the Unix operating system.

The KDE desktop is developed and distributed by the KDE Project, which is a large open group of hundreds of programmers around the world. KDE is entirely free and open software provided under a GNU Public License and is available free of charge along with its source code. KDE development is managed by a core group: the KDE Core Team. Anyone can apply, though membership is based on merit.

> Note KDE applications are developed using several supporting KDE technologies. These include KIO, which offers seamless and modular access of files and directories across a network. For interprocess communication, KDE uses the Desktop Communications Protocol (DCOP). KParts is the KDE component object model used to embed an application within another, such as a spreadsheet within a word processor. The XML GUI uses XML to generate and place GUI objects such as menus and toolbars. KHTML is an HTML rendering and drawing engine.

Numerous applications written specifically for KDE are easily accessible from the desktop. These include editors, photo and paint image applications, spreadsheets, and office applications. Such applications usually have the letter k as part of their name-for example, KWord or KMail. A variety of tools are provided with the KDE desktop. These include calculators, console windows, notepads, and even software package managers. On a system administration level, KDE provides several tools for configuring your system. With KUser, you can manage user accounts, adding new ones or removing old ones. Practically all your Linux tasks can be performed from the KDE desktop. KDE applications also feature a built-in Help application. Choosing the Contents entry in the Help menu starts the KDE Help viewer, which provides a Web page-like interface with links for navigating through the Help documents. KDE version 3.0 includes support for the office application suite KOffice, based on KDE's KParts technology. KOffice includes a presentation application, a spreadsheet, an illustrator, and a word processor, among other components (see Chapter 11 for more details). In addition, an integrated development environment (IDE), called KDevelop, is available to help programmers create KDE-based software.

> Note On Red Hat, KDE uses a Bluecurve theme to make it appear much the same as the Gnome desktop. However, on KDE, menus will show more KDE applications, including access to the KDE Control Center on the main menu.

KDE was initiated by Matthias Ettrich in October 1996, and it has an extensive list of sponsors, including SuSE, Red Hat, Mandrake, O'Reilly, and others. KDE is designed to run on any Unix implementation, including Linux, Solaris, HP-UX, and FreeBSD. The official KDE Web site is www.kde.org, which provides news updates, download links, and documentation. KDE software packages can be downloaded from the KDE FTP site at ftp.kde.org and its mirror sites. Several KDE mailing lists are available for users and developers, including announcements, administration, and other topics. See the KDE Web site to subscribe. A great many software applications are currently available for KDE at apps.kde.com. Development support and documentation can be obtained at developer.kde.org. Various KDE Web sites are listed in Table 7-1.

Table 7-1: KDE Web Sites

| Web Site | Description |
|---|---|
| www.kde.org | KDE Web site |
| ftp.kde.org | KDE FTP site |
| apps.kde.com | KDE software repository |
| developer.kde.org | KDE developer site |
| www.trolltech.com | Site for Qt libraries |
| www.koffice.org | KOffice office suite |
| themes.freshmeat.net | KDE desktop themes, select KDE entry |
| lists.kde.org | KDE mailing lists |

**Note** Currently, new versions of KDE are being released frequently, sometimes every few months. KDE releases are designed to enable users to upgrade their older versions easily. Normally, you can use the Red Hat Network update utility to automatically update KDE as updates become available. Alternatively, you can download new KDE packages from your distribution's FTP site and install them manually. Packages tailored for various distributions can be also downloaded through the KDE Web site at www.kde.org or directly from the KDE FTP site at ftp.kde.org and its mirror sites in the stable directory.
