The following is an example session that achieves the preceding processes. Note that it does not include modifying the pf.conf file:

```
bob@solaris11beta:~$ su
Password: xxx
root@solaris11beta:~# pkg install firewall
    Packages to install:     1
    Services to change:      1
    Create boot environment: No
    Create backup boot environment: Yes
DOWNLOAD          PKGS      FILES   XFER (MB)   SPEED
Completed         1/1       30/30   0.3/0.3     145k/s
PHASE             ITEMS
Installing new actions            87/87
Updating package state database   Done
Updating package cache            0/0
Updating image state              Done
Creating fast lookup database     Done
Updating package cache            1/1
root@solaris11beta:~# svcadm disable network/ipfilter
root@solaris11beta:~# svcadm enable network/firewall
root@solaris11beta:~#
```

# 23.10 VIRTUALIZATION METHODOLOGIES

A virtual environment for a computer program, and for an operating system, can be defined as a shell within which the program functions autonomously. In Chapter 25 we show three popular and important facilities for creating a virtual operating system environment within a UNIX host environment: PC-BSD Jails implemented and controlled by the iocage program, Solaris 11 Zones, and VirtualBox VMs. These facilities provide extensions of some of the topics we covered in this chapter.

What differentiates these three facilities is that, for the first two, all virtual environments are running under the same kernel on one host machine. In the third one, any number of different kernels can be running simultaneously on one host machine. That means that for Jails you can be running many versions of only PC-BSD at the same time on one machine. And for Zones you can only be running multiple versions of Solaris 11 at the same time on one machine. With VirtualBox, you can be running PC-BSD, Solaris 11, and any number of other operating systems at the same time on one machine.

The important application of these methodologies in the context of system administration is to provide a measure of system security. For example, it is possible with all three facilities to isolate a system service or application program in a guest operating environment, completely autonomous from the host operating system. A service like an ftp server can be run inside of a PC-BSD Jail or Solaris 11 Zone, and anything that intrudes upon that server and its system space does not intrude upon the host operating system space.