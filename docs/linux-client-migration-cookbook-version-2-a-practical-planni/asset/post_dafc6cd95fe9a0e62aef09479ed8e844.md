
![](img/23b949da14ff7bab8762f0f0361af394_338_0.png)

Figure D-4 Desktop Multiplier using one X server for all client workstations

Figure D-4 shows a multi-station X implementation that uses a single X server to handle multiple sets of keyboard/mouse inputs and outputs one desktop for each user to use one or more associated monitors. This is how Desktop Multiplier operates.

And Figure D-5 on page 312 shows a multi-station X implementation in which one X server handles each set of keyboard/mouse inputs and outputs one desktop for each user to use one or more associated monitors. This is how "Ruby", also known as "Backstreet Ruby", operates. For more information, see:

```
http://www.tldp.org/HOWTO/XFree-Local-multi-user-HOWTO/about_rubry.html
```

![](img/23b949da14ff7bab8762f0f0361af394_339_0.png)

**D-5** Other multi-station approaches with separate X servers for each workstation

In a standard single user environment, the user runs a single instance of X on top of which rests the remainder of the GUI. In a multi-station environment, a single instance of X can be set up to handle multiple users (Desktop Multiplier) or multiple instances of X can be run (as in the case of Ruby).

![](img/23b949da14ff7bab8762f0f0361af394_340_0.png)

# Client personalization

This appendix compares the methods for storing client-side personalization data between Windows and Linux. Because this book focuses on migrating clients from Windows to Linux, migration of client-side personalization data could also be an important requirement for the planning and implementation phases of a project.

# Microsoft Windows client personalization

The primary container for personalization data in Windows is called the user’s profile. In Windows 2000 and Windows XP, profile data for the user "username" is typically stored in:

```
c:\documents\username
```

In Windows NT, profile data for the user "username" is typically stored in:

```
c:\profiles\username
```

Windows uses these locations to store various kinds of personalization data. For example:

- User documents
- Application data and settings
- Temporary Internet files
- Internet favorites

The profile directory name uses the user ID, but can also have a more detailed distinction, sometimes the computer name or the name of the domain is appended. This happens if a user exists already and a new one is created with the same name but integrated in the domain. So one username can exist several times on a machine, connected with the domain name or the local machine name or combinations. The consequence is that Windows has to distinguish between username.localcomputername and username.domainname.

Some settings are stored in folders of the user's profile. For instance, many settings are stored in a folder called "Application Data". However, the majority of settings are stored in the registry. The Windows registry contains two "hives". The "Local Machine" contains system-wide settings and hardware information. The "Current User" contains settings that are specific to a certain user. The registry has its own permissions layer, which is similar to file system permissions. The registry can only be accessed through APIs provided by Microsoft, because the binary file representation is too complex to manually edit. Because many settings are stored in the registry, this can lead to a single point of failure; a corrupted registry can render an entire profile unusable.

# Linux client personalization

Considering the modular structure of Linux, it becomes clear profiles must differ substantially from the Windows profiles. Because there is no registry in Linux, all settings must be saved in another way. System-wide settings in Linux are normally configured using readable text files in the /etc directory. These frequently have extensions such as .conf or .profile.

The file /etc/profile sets the system-wide environment and startup programs per user login. These system-wide defaults can be extended by profiles in the local or home directory of the user. The local .bash_profile (Bourne Again Shell) is one example on Red Hat Enterprise Linux; the .profile file on SUSE Linux is another example.

Structurally, Linux stores user profile data in a method somewhat similar to the Windows does. All individual user settings are stored inside the user's home directory, which is sometimes referenced as $HOME. The home directory for the user /username is usually found at:

```
/home/username
```

Linux does not implement a registry the Windows does. Instead, user profile information is stored in configuration files within the individual user home directories. These files are usually created by specific applications that need to store user personalization data required by that application.

One advantage of these files is that they are often plain text formatted files, and thus human readable. Another is that the content can be automatically manipulated by scripts if you want. Also, because each application stores data in separate files, a corrupted file affects that application. Because these files are standard files, the standard file permissions allow. By modifying these files, it is possible to prevent unintended changes by the user. This could have the effect of "looking down" certain aspects of the user's login environment.

Most applications create a hidden folder, beginning with a dot or period (.), in which configuration files for those applications are created and maintained. Frequently, these files are grouped together with similar applications, such as all Mozilla-based applications storing settings in $HOME/mozilla.

# Desktop personalization KDE Desktop

In KDE, desktop personalization is based on information found in a standard directory structure within the user's home directory. The contents of the desktop, including icons and other data, is usually found in:

```
/home/username/Desktop
```

Application data settings, such as e-mail, bookmarks, and other preferences, are usually stored in:

```
/home/username/.kde/share/config
```

When KDE looks up a setting, it first checks settings in the user's home directory. If the setting is not found, then it looks in the global configuration directory. Red Hat typically places the global configuration files in the

/usr/share/config directory. Other distributions might place these files in different locations. Because users start out with no customized settings in their home directory, any changes that are made to the global settings files are inherited by all new users created after making the changes.

KDE uses plain text files for all its configuration options. This makes it easy to configure KDE using scripts and editors. Three of the main files used to configure the desktop are:

- kdeglobals
- kdesktopoprc
- kickerrrc

The most recent versions of KDE ship with an application called KConfigEditor. KConfigEditor allows you to edit these files in a GUI. KConfigEditor can also be used to change some settings for GNOME applications as well. An example of the KConfigEditor interface is shown in Figure E-1.

![](img/23b949da14ff7bab8762f0f0361af394_343_0.png)

Figure E-1 KConfigEditor editing kdesktopoprc

# Desktop personalization GNOME Desktop

As with the KDE desktop, desktop personalization files in GNOME are stored in a directory structure within the user's home directory. Just like KDE, modern versions of GNOME store icons and other data in:

```
/home/username/Desktop
```

The task of making general configuration changes to the GNOME desktop is extremely different than for KDE. While KDE uses simple text files, the GNOME desktop uses a database called GConf to manage all of its settings. In order to make settings available from different applications and also from tools within the GNOME Desktop, there is a daemon running that notifies all involved applications when a value has changed and that manages all between applications and the configuration sources. This daemon is called gconfd-2 and runs in one instance for each user.
