
| User GNOME Directories | Contents |
|---|---|
| .gnome, .gnome2 | Hold configuration files for the user's GNOME desktop and GNOME applications. Includes configuration files for the panel, background, MIME types, and sessions. |
| .gnome-desktop | Directory where files, directories, and links you place on the desktop will reside. |
| .gnome2_private | The user's private GNOME directory. |
| .gtkrc | GTK+ configuration file. |
| .gconf | GConf configuration database. |
| .gconfd | GConf gconfd daemon management files. |
| .nautilus | Configuration files for the Nautilus file manager. |

## TABLE 8-4 GNOME Configuration Directories (continued)

## GNOME User Directories

GNOME sets up several hidden directories for each user in their home directory that begin with .gnome and include a preceding period in the name. .gnome and .gnome2 hold files used to configure a user's GNOME desktop and applications. Configuration files for the panel, MIME types, and sessions, among others, are located here. Configuration files for particular GNOME applications are kept in the subdirectory apps. The .gnome-desktop directory holds any files, folders, or links the user has dragged to the desktop. .gtkrc is the user configuration file for the GTK+ libraries, which contains current desktop configuration directives for resources such as key bindings, colors, and window styles.

## GConf

With GNOME 2.0, GNOME officially implements GConf to provide underlying configuration support. GConf corresponds to the Registry used on Windows system. It consists of a series of libraries used to implement a configuration database for a GNOME desktop. This standardized configuration database allows for consistent interactions between GNOME applications. GNOME applications that are built from a variety of other programs, as Nautilus is, can use GConf to configure all those programs according to a single standard, maintaining configurations in a single database. Currently the GConf database is implemented as XML files in the user's .gconf directory. Database interaction and access is carried out by the GConf daemon, gconfd.

## CHAPTER

## The K Desktop Environment: KDE

The K Desktop Environment (KDE) is a network-transparent desktop that includes the standard desktop features, such as a window manager and a file manager, as well as an extensive set of applications that cover most Linux tasks. KDE is an Internet-aware system that includes a full set of integrated network/Internet applications, including a mailer, a newsreader, and a Web browser. The file manager doubles as a Web and FTP client, enabling you to access Internet sites directly from your desktop. KDE aims to provide a level of desktop functionality and ease of use found in MAC/OS and Windows systems, combined with the power and flexibility of the Unix operating system.

The KDE desktop is developed and distributed by the KDE Project, which is a large open group of hundreds of programmers around the world. KDE is entirely free and open software provided under a GNU Public License and is available free of charge along with its source code. KDE development is managed by a core group: the KDE Core Team. Anyone can apply, though membership is based on merit.

> NOTE KDE applications are developed using several supporting KDE technologies. These include KIO, which offers seamless and modular access of files and directories across a network. For interprocess communication, KDE uses the Desktop Communications Protocol (DCOP). KParts is the KDE component object model used to embed an application within another, such as a spreadsheet within a word processor. The XML GUI uses XML to generate and place GUI objects such as menus and toolbars. KHTML is an HTML rendering and drawing engine.

Numerous applications written specifically for KDE are easily accessible from the desktop. These include editors, photo and paint image applications, spreadsheets, and office applications. Such applications usually have the letter k as part of their name—for example, KWord or KMail. A variety of tools are provided with the KDE desktop. These include calculators, console windows, notepads, and even software package managers. On a system administration level, KDE provides several tools for configuring your system. With KUser, you can manage user accounts, adding new ones or removing old ones. Practically all your Linux tasks can be performed from the KDE desktop. KDE applications also feature
