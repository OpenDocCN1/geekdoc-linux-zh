# Using RPM for Software Management

# rpm -Uvh pine-4.44-7.i386.rpm
Preparing...
#################################### [100%]
########################################################### [100%]
1:pine

Note that it wasn't necessary to remove the currently installed software package—the upgrade option (saving the old configuration files), and then automatically installs the new software.

You can also upgrade your system software by using the rpm command -F or "freshen" option, which will fetch a designated package from a remote FTP or HTTP server. For example, to upgrade the fetchmail-conf package, use rpm like this (the FTP URL has shortened in this example):

```
# rpm -Fv http://ftp.tux.org/linux/redhat/updates/7.3/en/i386/
fetchmailconf-5.9.0-11.i386.rpm
```

Retrieving http://ftp.tux.org/linux/redhat/updates/7.3/en/i386/
fetchmailconf-5.9.0-11.i386.rpm

Preparing packages for installation...
fetchmailconf-5.9.0-11

If you have broadband access, you can upgrade a system in place quickly without taking it to runlevel 1 (see Chapter 7, "Managing System Services"). This is a primary feature of Xim's version of GNOME, http://www.xim.com/. The rpm command will retrieve the designated package, and then upgrade the software on your system. You use the -e option, along with the name of a software package, to remove or erase software from your system with rpm. For example, to remove the pine email package, use the rpm command like this:

```
# rpm -e pine
```

Note that if the operation succeeds, no messages will be displayed on your system. You can quickly search for the names of installed packages by piping the output of rpm -qa through the grep and sort commands (see Chapter 5, "First Steps with Linux"), for additional information on grep and sort); here's how to search:

```
$ rpm -qa | grep mail | sort
fetchmailconf-5.9.0-5
fetchmailconf-5.9.0-11
kmail-3.0.0-4
mailcap-2.1.9-2
mailman-2.0.9-1
mailx-8.1.1-22
metamail-2.7-28
procmail-3.22-5
redhat-switchmail-0.5.1-1
```