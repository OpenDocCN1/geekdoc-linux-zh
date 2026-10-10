# Chapter 7: Home sweet /home

```
[root@jupiter root]# rpm -e totem
[root@jupiter root]#
```

Note that uninstalling is not that verbose by default, it is normal that you don't see much happening. When in doubt, use `rpm -qa` again to verify that the package has been removed.

RPM can do much more than the couple of basic functions we discussed in this introduction; the RPM HOWTO <http://www.tldp.org/HOWTO/RPM-HOWTO/index.html> contains further references.

# ### 7.5.2.2. DEB (.deb) packages

# #### 7.5.2.2.1 What are Debian packages?

This package format is the default on Debian GNU/Linux, where `dselect`, and, nowadays more common, `aptitude`, is the standard tool for managing the packages. It is used to select packages that you want to install or upgrade, but it will also run during the installation of a Debian system and help you to define the access method to use, to list available packages and to configure packages.

The Debian web site <http://debian.org/> contains all information you need, including a "dselect Documentation for Beginners".

According to the latest news, the Debian package format is becoming more and more popular. At the time of this writing, 5 of the top-10 distributions use it. Also `apt-get` (see Section 7.5.3.2) is becoming extremely popular, also on non-DEB systems.

# #### 7.5.2.2.2 Examples with DEB tools

Checking whether a package is installed is done using the `dpkg` command. For instance, if you want to know which version of the Gallery software is installed on your machine:

```
nightwish@goferst:~$ dpkg -l *gallery*
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Installed/Config-Files/Unpacked/Failed-Config/Half-installed
|/ Err?=none/Hold/Reinst-r-quired/X=both-problems (Status,Err: uppercase=bad)
||/ Name Version Description
+++=-==================================================================
ii gallery 1.5-1sarge2 a web-based photo album written in php
```

The "ii" prefix means the package is installed. Should you see "un" as a prefix, that means that the package is known in the list that your computer keeps, but that it is not installed.