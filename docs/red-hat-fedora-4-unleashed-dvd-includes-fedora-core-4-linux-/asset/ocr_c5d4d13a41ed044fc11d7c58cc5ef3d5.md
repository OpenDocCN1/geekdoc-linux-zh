+   • initab—The system initialization table defines the default runlevel, also known as run-control level or system state. Changes to this file can determine whether your system boots to a graphical or text login, as well as whether dial-up remote access is enabled. (You learn about default runlevels in the section “System Services and Runlevels” located in Chapter 14, “Automating Tasks.” See the section “Starting X” located in Chapter 6 to learn more about changing initab to boot to a graphical interface. Chapter 18, “Internet Connectivity,” in the section “Configuring a Dial-In PPP Server” discusses editing initab to enable dial-up remote access).

+   • modprobe.conf—This configuration file contains directions and options used when loading kernel modules to enable various types of hardware, such as sound, USB, networking, and so on (discussed in the section “Managing Modules” in Chapter 38). The contents of this file are used during boot time, and the file can be manually edited or automatically updated by Red Hat’s kudz u hardware management server (if enabled, as you learn later in this section).

+   • passwd—The list of users for the system, along with user account information. The contents of this file can be changed by various programs, such as useradd or csh.

+   • printcap—The system’s printer capabilities database (discussed in the section “Overview of Fedora Linux Printing” in Chapter 11, “Printing with Fedora”).

+   • shells—A list of approved shells (command-line interfaces).

One of the most important directories under /etc for Fedora is sysconfig. This directory contains network activation scripts and hardware- and software-related information:

```
$ tree -afx /etc/sysconfig
/etc/sysconfig
|-- /etc/sysconfig/amd
|-- /etc/sysconfig/apm-scripts
|   |-- /etc/sysconfig/apm-scripts/apmscript
|-- /etc/sysconfig/apmd
...
|-- /etc/sysconfig/clock
|-- /etc/sysconfig/console
...
|-- /etc/sysconfig/dhcpd
|-- /etc/sysconfig/dhcrelay
...
|-- /etc/sysconfig/grub
|-- /etc/sysconfig/harddisks
|-- /etc/sysconfig/hidd
|-- /etc/sysconfig/httpd
|-- /etc/sysconfig/hwconf
...
|-- /etc/sysconfig/init
...
```