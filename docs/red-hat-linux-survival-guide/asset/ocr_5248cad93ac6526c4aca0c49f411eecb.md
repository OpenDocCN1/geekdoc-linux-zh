installation phase, you can install the RPM version of the software. For example, to install the 9.1.0-10 version of BIND software for the Intel x86 platform, I located the bind-9.1.0-10.i386.rpm package in the Red Hat Linux CD-ROM's RPMS directory and ran the following command:

```
rpm -ivh bind-9.1.0-10.i386.rpm
```

The RPM package of the BIND software just described comes with three programs: /usr/sbin/named (the name server itself), /usr/sbin/named-xfer (the accessory program for the name server), /usr/sbin/ndc (a program to control the name server), and /usr/doc/bind-8.2.2/named-bootconf.pl (an accessory Perl script to convert older configuration files to the new format). After you've installed the BIND software, you're ready to configure DNS.

# Understanding the Basics of DNS Configuration

The primary configuration file for the BIND domain name server daemon, named, is /etc/named.conf. At startup, the named server reads this configuration file to determine how it should function.

# The /etc/named.conf file

This file consists of comments, statements, and blank lines, as described in the following sections.

# Comments

A comment line can be a single line that starts with two forward slash characters. For example:

```
// This is a comment line in named.conf
```

Or it can be a line that starts with a # character as follows:

```
# This is a comment line in named.conf
```