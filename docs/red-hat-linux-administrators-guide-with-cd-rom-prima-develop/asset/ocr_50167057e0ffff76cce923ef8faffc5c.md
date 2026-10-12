the use of a GUI editor. Any changes made to the smb.conf file will not take effect until the SAMBA daemon is restarted.

Most Linux distributions have a version of SAMBA ready for installation. You can install this version either through the RPM version or through the source code release. The RPM version is by far the easier method to install. It places each of the several necessary files in their respective directories and makes it simple to start and stop the daemon.

The typical method of starting, stopping, or restarting SAMBA involves executing the standard command located in the run command directory. As you have seen as previously with the other daemons, you can send this daemon a restart signal:

```
# /etc/rc.d/init.d/smb restart
```

Such a command usually restarts two different services. SAMBA is actually composed of both the smbd daemon, which controls file and print services to the various Windows versions and to other Linux and UNIX clients, and nmbd, which provides NetBIOS name-serving and browsing support. RPM installations usually provide for both to be started at the same time, but both are equally customizable using the smb.conf file. The following is sample output from a restart command to the smb daemon:

```
# /etc/rc.d/init.d/smb restart
Shutting down SMB services:[ OK ]
Shutting down NMB services:[ OK ]
Starting SMB services:[ OK ]
Starting NMB services:[ OK ]
```

This service provides some useful functionality. For example, you can see Linux systems from within the Network Neighborhood icon of any Windows 95/98/2000 machine and subsequently access your own personal directory on that Linux box, if your login name and your Linux directory's name are the same. You can also share certain directories under SAMBA for others in your same workgroup to access, both for downloading and writing purposes.

# Configuring the smb.conf File

The key to making SAMBA work and giving other systems the correct permissions to access your Linux directories is to understand the /etc/smb.conf file. For most uses, editing only the first few lines of the smb.conf file is sufficient to get