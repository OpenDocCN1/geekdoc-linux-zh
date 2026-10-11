
## Figure C-12

| | Red Hat Enterprise Linux | SUSE Linux Enterprise Server |
| :--- | :--- | :--- |
| **Sysinit Scripts** | `/etc/rc.d/rc.sysinit` | `/etc/init.d/boot` |
| | `/etc/rc.d/rc.local` | `/etc/hot.d/boot.*` |
| | | `/etc/init.d/boot.local` |
| **Modules** | `/etc/modprobe.conf` only lists aliases for boot time load | `/etc/modprobe.conf` lists all modules that can be loaded |
| | | `/etc/modprobe.d/` (include directory for modprobe) |
| | `/etc/modprobe.conf.dist` lists all modules that can be loaded | `/etc/modprobe.conf.local` |

Note: SUSE Linux Enterprise Server uses `/filename.local` files for a lot of items. The use of a _local file ensures that when a security patch or fix for a bug comes out and the updated package is applied to the system, the _local file that matches up with the configuration file will not be touched; it is solely the realm of the system administrator.

## The SUSE Linux Enterprise Server Boot Process

SUSE Linux Enterprise Server uses a boot process that is similar to the process employed by Red Hat Enterprise Linux in many ways, but while Red Hat Enterprise Linux uses the kudzu tool, SUSE Linux Enterprise Server uses the linuxrc script to do the system initialization tasks.

The following list explains the SUSE Linux Enterprise Server boot process in detail:

1. Power-on self-tests
2. Initially detects and sets up hardware (such as PNP)
3. Locates the MBR on the bootable device
4. Reads the MBR from the bootable device
5. BIOS starts the boot manager
6. Boot Manager (such as GRUB) loads the Kernel and Initial (Initial RAM Disk)
7. Boot Manager starts the Kernel
8. Kernel decompresses itself and then takes control of the booting of the system
9. Note: if the initial root ext3 is used, it is mounted as the root of the system. The linuxrc script then loads the needed drivers to access the real system root and initrd is unmounted.
10. Kernel mounts the real system root
11. Kernel checks and sets up the console, reads RDS settings and initializes basic hardware interfaces
12. Drivers probe and initialize existing hardware
13. Kernel now controls the system, including hardware access and allocation of CPU time and memory
14. Kernel loads the init program, which becomes PID 1
15. Then init calls the `/etc/init.d/boot` to activate swap, disk quotas, logical volumes and software RAID and finally mount local file systems from the `/etc/fstab`
16. Next init calls the `/etc/init.d/rc` script, which switches the system to the default runlevel defined in the `/etc/inittab`
17. The runlevel scripts are initialized, and if the default runlevel includes multi-user characteristics, the Getty processes are initialized and users can then log in

## Init and Runlevels

This section provides a layout and comparison of the paths and methods that are different between Red Hat and SUSE boot processes and runlevels.

The way that Red Hat and SUSE Linux Enterprise Server store and manage their daemons are slightly different. The main path difference is that Red Hat uses and documents its service and runlevel root in the `/etc/rc.d` tree, while SUSE Linux Enterprise Server uses the more traditional `/etc/init.d` tree.

SUSE Linux Enterprise Server provides a symbolic link named `/etc/rc.d` that points to the `/etc/init.d` directory for Red Hat compatibility. You'll find upon inspection that Red Hat systems include a symlink named `/etc/init.d` that really points to the directory `/etc/rc.d/init.d`.

| | Red Hat Enterprise Linux | SUSE Linux Enterprise Server |
| :--- | :--- | :--- |
| Init files Root | `/etc/rc.d/init.d` | `/etc/init.d` |
| Runlevel Directories | `/etc/rc.d/rcXd` | `/etc/init.d/rcXd` |
| Service Scripts | `/etc/init.d/service start/stop` | `/etc/init.d/service start/stop` |
| | `service <name> start/stop` | `rc <name> start/stop` |
| | `(executes /sbin/service scripts)` | |
| Service Commands | `chkconfig <name> on/off` | `chkconfig <name> on/off` |
| | | `insserv <name>` |

## SUSE Linux Enterprise Server Boot Options

The intent of this section is to have a quick reference for the multitude of options that can be specified on the boot prompt for a SUSE Linux Enterprise Server system. In most cases the option text is followed by a " = " sign and then the value, such as `Language=en`.

| Option name | Description | Example |
| :--- | :--- | :--- |
| Language | Set the language | `de_DE` |
| Keyboard | Load this keyboard | `de-latin1` |
| Display | Set the menu color scheme | `Color/Mode/Alt` |
| Install | URL to installation source media | `http://Server/path/to/source` |
| Instmode | Install mode | `cd/dnf/dns/nbd/http/https` |
| HostIP | Client IP address | 10.0.0.1 |
| Netmask | Client netmask | 255.0.0.0 |
| Gateway | Client gateway | 10.0.0.254 |
| Server | Installation server address (deprecated, use install- instead) | 10.0.0.2 |
| Nameserver | DNS server | 10.0.0.3 |
| Proxy | FTP or HTTP proxy server | 10.0.0.4 |
| Proxy port | Proxy server port | 8000 |
| Partition | Path to local install source | /Partitions=hda1 |
| Server dir | Path relative to “Server” param (deprecated, use install- instead) | /path/to/source |
| Netdevice | Network interface to use during install | eth0 |
| BOOTPWait | Sleep x seconds between network activation and starting bootp | 5 |
| BOOTPTimeout | x second time-out for BOOTP requests | 10 |
| DHCPTimeout | x second time-out for DHCP requests | 60 |
| TFTPTimeout | x second time-out for TFTP connection | 10 |
| ForceRootImage | Load the installation system into RAM disk | 0 or 1 |
| Textmode | Start YaST in text mode (for VMware, older monitors etc) | 0 or 1 |
| Username | Username for install server (i.e tftp) | User |
| Password | Password for install server (e.g., TFTP) | Password=newell |
| WorkDomain | Domain/workgroup name for Samba install | Workgroup=TUMNET |
| ForceInismod | For inismod to run with -f | 0 or 1 |
| DHCP | Start DHCP daemon now, but use UseDHCP | 0 or 1 |
| UseDHCP | Use DHCP instead of BOOTP (DHCP is default) | 0 or 1 |
| MemLimit | Ask for swap if free memory drops below xxx kB | 1000 |
| Manual | Start Isuarc in manual mode | 0 or 1 |
| NoPCIModule | Don’t start PCMCIA | 0 or 1 |
| AutoYaST | Path to AY control file | autoyast=http://server/control.xml |
| Vnc | Install over VNC instead of local console | 0 or 1 |
| vnc_password | Set VNC password (min. 5 chars) | vnc_password=novell |
| UseSSH | Install over SSH instead of local console | 0 or 1 |
| SSHPassword | Set SSH password | SSHPassword=novell |
| insmod | Load xz2 kernel mod | insmod=pcent32 |
| brokenmodules | Modules to ignore or not load | brokenmodules=agp |
| acpi | Turn on/off ACPI Options | acpi=off |
| apic | Clustering Mode support for i64 | apic=noapic |
| apm | Advanced Power Management | apm=off |
| barrier | Journaling File System Support for transactional writes | barrier=flush (for reiserfs) <br> barrier=1 (for ext3) |
| netwait | Causes the network to wait N seconds (for other modules) | netwait=10 |
| LogHost | Log install messages to a remote syslog server in addition to /var/log/YaST2/y2log | LogHost=10.0.0.1 (IP address of logging server) |

## SERVICES AND DAEMONS

Although not all-inclusive, the following table contains the majority of the situations in which Red Hat and SUSE Linux Enterprise Server differ.

| | Red Hat Enterprise Linux | SUSE Linux Enterprise Server |
| :--- | :--- | :--- |
| Apache | | |
| Configuration Files | /etc/httpd/conf/httpd.conf | /etc/apache2/httpd.conf |
| Include Files and/or Directories | /etc/httpd/conf.d/*<br>... | /etc/apache2/conf.d<br>/etc/apache2/sysconfig.d<br>/etc/apache2/vhosts.d |
| Log Files | /var/log/httpd/* | /var/log/apache2 |
| WebRoot | /var/www/html | /srv/www/htdocs |
| CGI-BIN Directory | /var/www/cgi-bin | /srv/www/cgi-bin |
| Commands | /etc/init.d/httpd | /etc/init.d/apache2 |
