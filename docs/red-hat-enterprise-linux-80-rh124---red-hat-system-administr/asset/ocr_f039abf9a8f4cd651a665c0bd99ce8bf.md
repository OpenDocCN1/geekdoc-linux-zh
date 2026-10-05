# CHAPTER 1 | Installing and Updating Software Packages

```
git-instaweb.x86_64 : Repository browser in gitweb
...output omitted...
```

+   * yum info PACKENAME returns detailed information about a package, including the disk space needed for installation.

Get information on the Apache HTTP Server:

```
[user@host ~]$ yum info httpd
Available Packages
Name            : httpd
Version         : 2.4.37
Release         : 7.module+el8+2443+605475b7
Arch            : x86_64
Size            : 1.4 M
Source          : httpd-2.4.37-7.module+el8+2443+605475b7.src.rpm
Repo            : rhel8-appstream
Summary         : Apache HTTP Server
URL             : https://http.apache.org/
License         : ASL 2.0
Description     : The Apache HTTP Server is a powerful, efficient, and extensible
                : web server.
```

+   * yum provides PATHNAME displays packages that match the path name specified (often include wildcard characters).

To find packages that provide the /var/www/html directory:

```
[user@host ~]$ yum provides /var/www/html
httpd-filesystem-2.4.37-7.module+el8+2443+605475b7.noarch : The basic directory
layout for the Apache HTTP server
Repo            : rhel8-appstream
Matched from:
Filename        : /var/www/html
```

# Installing and removing software with yum

+   * yum install PACKENAME obtains and installs a software package, including any dependencies.

```
[user@host ~]$ yum install httpd
Dependencies===================================================================
Package        Arch            Version             Repository        Size
===================================================================
Installing:
httpd           x86_64          2.4.37-7.module...  rhel8-appstream   1.4 M
Installing dependencies:
apr             x86_64          1.6.3-8.el8         rhel8-appstream   125 k
apr-util        x86_64          1.6.1-6.el8         rhel8-appstream   105 k
...output omitted...
Transaction Summary
====================================================================
```

RH124-RHEL8.0-en-1-20190507

491