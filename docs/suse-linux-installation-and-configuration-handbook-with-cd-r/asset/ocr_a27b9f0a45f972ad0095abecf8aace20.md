# Table 6.1 Important System Directories

| Directory | Description |
|---|---|
| /etc/ | The systemwide configuration directory. It contains all the important settings. This directory is a must-have when backing up. |
| /opt/kde/share/config | The default configurations for KDE. The per-user .kde directory is more important than this one. |
| ~/.kde | The per-user .kde configuration directory. If you use KDE as your main desktop environment, you should back up this directory to save your settings. |
| ~/.gnome | The per-user GNOME configuration directory. If your main desktop environment is GNOME, you should back up this directory. |
| /opt/www | You should back up this directory if your SuSE Linux is a Web server. |
| /usr/src/linux/.config | This file contains your SuSE Linux kernel configuration. You should back up this file only if you have applied special settings to your kernel and recompiled it. It will save you a lot of time reading the kernel options help. |
| /usr/share/ | Many packages have their configuration files in this directory. This is where you should look for the packages with settings that need to be backed up. |
| /usr/X11/share | Some X-related packages keep their configuration files in this directory. |
| /usr/X11/lib/X11/app-defaults | Default interface settings for many X applications are kept in this directory. |
| /usr/local/etc | Although the default SuSE Linux installation does not use this directory to keep configuration settings, programs specific to this server might be installed in /usr/local and thus keep their configuration files in /usr/local/etc. |

# Planning a Backup Strategy

When planning a backup strategy you must consider how important your data or your users' data is to you. In fact, the efficiency of a backup can be measured by two factors:

+   - Availability of the system—It is important that you restore the system to what it was as quickly as you can. A good system configuration backup should do this in almost no time.