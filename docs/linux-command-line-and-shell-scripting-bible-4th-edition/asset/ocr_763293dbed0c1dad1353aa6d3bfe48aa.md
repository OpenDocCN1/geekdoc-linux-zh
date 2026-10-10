```
```
r    rm -f /usr/local/share/man/man8/sa1.8*
    install -m 644 -g man man/sa1.8 /usr/local/share/man/man8
    rm -f /usr/local/share/man/man8/sa2.8*
    install -m 644 -g man man/sa2.8 /usr/local/share/man/man8
    rm -f /usr/local/share/man/man8/sadc.8*
    ...
    install -m 644 -g man man/sadc.8 /usr/local/share/man/man8
    install -m 644 FAQ /usr/local/share/doc/sysstat-12.3.3
    install -m 644 *.1sm /usr/local/share/doc/sysstat-12.3.3
#
```
```

Now the sysstat package is installed on the system! Though not quite as easy as installing a software package via a package management system, installing software using tarballs is not that difficult.

# ## Summary

This chapter discussed how to work with a software package management system to install, update, or remove software from the command line. Most of the Linux distributions use fancy GUI tools for software package management, but you can also perform package management from the command line.

The Debian-based Linux distributions use the `dpkg` utility to interface with the package management system from the command line, and the `apt-cache` and `apt-get` utilities to interface with a common repository to easily download and install new software. A front end to these utilities is `apt`. It provides simple command-line options for working with software packages in the `dpkg` format.

The Red Hat-based Linux distributions are based on the `rpm` utility but use different front-end tools at the command line. Red Hat, CentOS, and Fedora use `dnf` for installing and managing software packages. The openSUSE distribution uses `zypper` for managing software.

Application containers are a relatively new player in software package management. An application container bundles all the files necessary for an application to run in one installable package. This means the application doesn't rely on any external dependencies such as library files, and the container bundle can be installed in any Linux