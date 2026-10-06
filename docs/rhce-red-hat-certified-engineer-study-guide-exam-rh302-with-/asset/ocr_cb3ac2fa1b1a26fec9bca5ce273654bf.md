288 Chapter 12 • Using RPM Packages

```
gnome-linuxconf
####################################
```

One of the advantages of the -vh is that it is very clear what packages have actually been installed. An annoying shortcoming of RPM is that it will exit with an error if a package is already installed. Without the -vh, it is some-times difficult to tell which packages in a list of packages were installed before RPM aborted.

Another handy RPM feature is support for files stored on FTP servers. Rather than downloading the package file and installing the package, you can install directly from the FTP server by issuing a command that has this form:

```
ftp://server/path
```

where server is the host or IP address of the anonymous FTP server and path specifies the path to the package file. For example, the following command installs a package that resides on Red Hat's anonymous FTP server:

```
rpm -ivh ftp://contrib.redhat.com/i386/RedHat/RPMS/
gnorpm-0.9-10.i386.rpm
```

If you need to access the FTP server by means of a particular account, issue a command that has the form

```
ftp://user:pass@server/path
```

where user and pass specify the user ID and password and the remaining tokens having the name given previously. If the server listens on a non-standard port, you can use this command form:

```
ftp://user:pass@server:port/path
```

where port is the number of the port on which the server listens. Red Hat Linux 6.2 and later versions of RPM support filename globbing, lets you include wildcard characters. For example, the RPM command to install gnorpm could be written

```
rpm -ivh ftp://contrib.redhat.com/i386/RedHat/RPMS/
gnorpm*
```

One more handy RPM feature is that you don't need to specify the pack-ages in any particular order, even if one or more of the specified packages depends on the capabilities of another. The rpm detects any depen-dencies and installs the packages in an appropriate order.

Copyright©2000 SYBEX, Inc., Alameda, CA www.sybex.com