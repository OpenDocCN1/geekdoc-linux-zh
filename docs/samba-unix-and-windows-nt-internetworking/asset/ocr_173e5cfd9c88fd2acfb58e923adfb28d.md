and get right to the point of the matter. Time to roll up our sleeves and install Samba.

# Install or Upgrade

The first task is to determine whether this will be a new installation or an upgrade to an existing Samba environment. If this is a new install, then go ahead and skip to the next section on Samba distribution. If you're taking the upgrade route, begin by determining the software version of your running Samba service. You may be able to verify the version number quickly by referring to the distribution directory used initially to install the software. Usually the directory name will indicate the version and release numbers. If it does not, then check the whatsnew.txt file in the top level of the distribution tree. If there is any question whether the running system corresponds to what you believe to be the distribution source, validate the version of the running system by invoking either the smbstatus or the smbclient command (Example 5.1).

# Example 5.1 smbstatus and smbclient version display

```
$ smbstatus -d
Samba version 2.0.5a
Service   uid   gid   pid   machine
----------------------------------------
No locked files
Share mode memory usage (bytes):
1048464(99%) free + 56(0%) used + 56(0%) overhead = 1048576(100%)
total
$ smbclient -L localhost
...
password:
Domain=[EYRIE] OS=[Unix] Server=[Samba 2.0.5a]
...
```

The version number will allow you to gauge differences between your current Samba environment and the new features and modifications available in the latest release. In most cases you will want to upgrade to the latest and greatest version of Samba. This will put you in the best position regarding support and problem fixes. Some sites may prefer to lag a release or two behind the current version, not wanting to be too near the bleeding edge. There might also be operating system or hardware dependencies that mandate remaining at an older release.

Next make note of any local customizations or changes that differ from the default Samba distribution. Examples include alternate directory paths for commands, libraries, and log files, and any modifications or patches to the source code. Save a copy of the Samba configuration file, smb.conf, and the password file, smbpasswd, somewhere safe, far away from the installation process. It's always a good idea to play it safe by taking a full backup of your system before making any major changes to services or configuration. The same advice of taking a system backup also applies once the installation has been completed. This will give you a reference point should you later need to restart from a clean installation base.

# Distribution

# Where Can I Get the Latest Stuff?