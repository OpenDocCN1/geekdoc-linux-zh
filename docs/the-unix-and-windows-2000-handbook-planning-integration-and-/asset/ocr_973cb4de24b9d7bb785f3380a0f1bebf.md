```
AUTO_HOME = $(YPSRCDIR)/auto.home
```

```
YPSERVERS = $(YPDDIR)/ypservers # List of all NIS servers for a domain
```

# rpc.yppasswdd

Users must be able to change their passwords on any NIS client. The master NIS server must be running the rpc.yppasswdd daemon to allow users to change their passwords. This daemon accepts command-line options that allow you to specify the location of the passwd file and to execute the make command in the /var/yp directory. The format for passing options to rpc.yppasswdd is different for the different versions of UNIX and should be confirmed by examining the man pages. Table 7.3 contains the locations of the scripts to update to specify the location of the passwd file (/var/yp/files, in our example) for the rpc.yppasswdd daemon.

# Startup Scripts

Each version of UNIX has a different startup script file. Table 7.4 contains startup files to edit for the domain name, ypserv, and ypbind daemons. We will use a Red Hat Linux 6.1 system to examine the startup scripts to ensure the start of NIS services at boot.

+   1. Change directory (cd) to /etc/rc.d/init.d and do a directory listing (ls), as shown in Figure 7.1.
+   2. Confirm that a startup script exists for ypserv, ypbind, and yppasswd. If a script is missing you will have to reinstall the module with RPM.
+   3. cd to /etc/rc.d/rc.3 and do an ls (Figure 7.2). This directory contains scripts for services that must be started for full multi-user

| Table 7.3 | Startup Scripts for rpc.yppasswdd |
|---|---|
| Version | File |
| AIX | /etc/rc.nfs |
| HPUX | /etc/rc.config.d/namesrvs |
| Linux | /etc/rc.d/init.d/yppasswdd |
| Solaris | /etc/init.d/rpc |