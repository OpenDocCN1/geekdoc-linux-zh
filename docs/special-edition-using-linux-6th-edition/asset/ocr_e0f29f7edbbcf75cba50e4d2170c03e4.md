Thousands of developers around the world work on various aspects of the KDE system, including programming, documentation, translation, all kinds of testing, and packaging. The KDE Web site is located at http://www.kde.org.

This Web site contains many resources for both users and developers of KDE. For example, the Web site provides online documentation in many languages. Also, users can participate in mailing lists to receive or give assistance in working with KDE. For developers, application style guides, automated tools for constructing KDE applications, bug and feature wish lists, and more can be found here.

The KDE project is devoted to a philosophy of ease-of-use, consistency, and quality for graphical applications in the Linux world.

# INSTALLING KDE

Most major Linux distributions include KDE automatically when you install them. Debian is a major exception because of disagreements over licensing (though this may change in the next release). If you run Debian or another distribution that does not include KDE by default, or if you simply want to upgrade to a later version, installing the latest version is fairly easy. All the files you need are available at ftp://ftp.kde.org/pub/kde.

KDE is made up of various packages, which are listed in Table 3.1. This list of packages is consistent throughout the various distribution systems (such as RPM, deb, or tar).

**TABLE 3.1  KDE PACKAGES**

| Package | Use |
|---|---|
| `qt` | (required) The Qt toolkit from Trolltech. All of KDE is based on this windows toolkit. |
| `kdesupport` | (highly recommended) Non-KDE libraries that KDE relies on. |
| `kdelibs` | (required) KDE shared libraries. |
| `kdebase` | (required) Core KDE applications, such as the window manager, control center, terminal, and Web browser. |
| `kdeadmin` | (optional) System administration tools, such as the package manager, kpackage. |
| `kdegames` | (optional) Various games for KDE. |
| `kdegraphics` | (optional) Graphic viewers and manipulation programs. |
| `kdemultimedia` | (optional) Multimedia applications, such as the CD player. |
| `kdenetwork` | (optional) Network applications, such as the mail client and news reader. |
| `kdetoys` | (optional) Miscellaneous fun applications, such as kmoon, which shows you the current phase of the moon. |
| `kdeutils` | (optional) More useful utilities, such as the calculator and text editor. |
| `koffice` | (optional) The K Office Suite includes a powerful word processor, spreadsheet, and more. |