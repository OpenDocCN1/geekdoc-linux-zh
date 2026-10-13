Only packages in the mandatory and default categories are installed. In most cases, that's not a problem. But the RHCE objectives related to web servers suggest the need to "deploy a basic CGI application." And the CGI-related packages are listed as optional. While there are ways to set up the installation of optional packages with the groupinstall switch, it's easier for our purposes to just install needed packages separately by name. For web servers, the appropriate package for handling CGI scripts is covered in Chapter 14.

In a similar fashion, you can install the Samba File Server covered in Chapter 15 with the following command:

```
# yum groupinstall "CIFS file server"
```

There's actually just one package in this group, samba. For that reason, the following command would work equally well:

```
# yum install samba
```

For Chapter 17, the Network Infrastructure Server package group includes packages associated with logging and DNS. However, as all packages in this group are optional, the yum groupinstall command would not install any packages from that group. Fortunately, the rsyslog package is already installed by default, even in a minimal RHEL 6 installation. But you will want to install DNS to address one of the RHCE objectives. One way to set up the DNS service for Chapter 17 is with the following command:

```
# yum install bind
```

For a number of server services, you should make sure that appropriate client packages are installed. The Network file system client package group can help in that respect; the following command would install clients for the automounter, Samba, and NFS:

```
# yum groupinstall "Network file system client"
```

A different kind of network server relates to iSCSI storage. There are two package groups of interest: the Network Storage Server and the iSCSI Storage Client. They each are associated with a single package, which will be discussed in Chapter 12.

Finally, there are a couple of packages of interest that are not included in standard package groups. They set up the NTP server and authentication to remote databases. If not already installed, you'll need to install them. One method is with the following command:

```
# yum install ntp sssd
```