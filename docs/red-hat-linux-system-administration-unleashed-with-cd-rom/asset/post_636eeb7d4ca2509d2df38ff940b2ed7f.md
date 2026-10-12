
allows you to use any of the installation methods supported by Red Hat, but not have to answer all of the questions. The primary difference between this method and the homegrown approach just described is that even with kickstart files, there is no installation method available from Red Hat that uses a network push model.

## A Template-Based Approach

The methods described thus far are useful if your machines are all basically the same, but if your network is composed of several classes of machines, it might be useful to consider the following approach to managing system installations. This approach relies on the fact that at some level, all systems must have a common core of software in order to function on the network. This core becomes your base template, which you can install to all machines as a first step to bringing a new machine online. For purposes of this discussion, we will assume that your network is divided into two parts. The first part is your administrative network, which is where the day-to-day work of the company is performed and where machines fall into four base categories. These are a development workstation, a development server, an administrative server, and an administrative workstation. The second part of the network is the production network, which consists of Web servers, database servers, and mail servers.

## Establishing an Install Template

Based on the network described in the preceding section, you will begin by creating an install template. There will be two flavors of install templates—one minimalist template for the production network, and a second more featureful template for your administrative network. Let's start with a discussion of the production template.

## The Production Template

Since the production servers are not intended for interactive use, the install template for them will not include several items that you might normally find on a Red Hat system. Some of the items that will be specifically excluded from the production template include the following:

- X Windows software
- Compilers
- Personal productivity software
- Office applications
- Documentation
- Games
- Word publishing software

In fact, the production template will include the bare minimum of software required to accomplish the following tasks:

- Boot the system
- Connect to the network
- Run scripts and programs

The first task is accomplished by installing the base Linux utilities found in /bin and /sbin along with the devices support in the /dev directory and configuration data found in /etc and /var. There is no need for most of the software normally found in /usr, with the exception of some of the utilities found in /usr/bin and support files in /usr/share and /usr/lib. An exact list of these files is not presented here because it would take up several pages, but a good starting point for determining which files are required can be found in the Filesystem Hierarchy Standard, which is described in Chapter 4, "Where Do I Find...?"

Next, you add the network connectivity support. These files are primarily the clients found in /usr/bin and the daemons found in /usr/sbin. This includes such items as the telnet daemons and clients, the daemons to support the remote commands such as rcp, rsh, and rlogin, and other network related files, such as /etc/services, /etc/protocols, and /etc/inetd.conf. It would also include those files required to protect your system, such as tcpd, ipchains, and proxy software if desired. The minimal set of files needed to establish network connectivity is the same as described in the discussion of creating boot floppies found earlier in this chapter.

Finally, there are the files required for program runtime support, such as shared libraries and files needed to support any scripting languages you will be using on the system, such as perl or tcl and their supporting files.

All of these files can be obtained from the Red Hat installation media, and with careful pruning can be made to fit in under 200 megabytes of disk space with some space for growth. This would naturally not include space for growth filesystems like /var or /tmp, but with judicious planning, you can have a thin server system base that you can customize to serve whatever purpose you like. Listing 3.4 specifies a list of packages that I use to meet the criteria specified here. This set of packages requires approximately 175 megabytes of hard drive space, but could be trimmed even further by the elimination of manual pages, info files, and other data not essential to the operation of a system.

## LISTING 3.4 List of Packages for Thin Server Installation

- setup
- filesystem
- basesystem
- ldconfig
- glibc
- chkconfig
- mktemp
- termcap
- libtermcap
- bash
- apmd
- ncurses
- info
- fileutils
- grep
- ash
- at
- authconfig
- bash2
- bc
- bdflush
- bind
- bind-utils
- binutils
- bzip2
- caching-nameserver
- sed
- console-tools
- e2fsprogs
- rmt
- cpio
- cracklib
- cracklib-dicts
- crontabs
- textutils
- shadow-utils
- dev
- diffutils
- ed
- eject
- emacs
- emacs-nox

## LISTING 3.4 continued

- etcskel
- file
- findutils
- ftp
- gawk
- gd
- gdb
- gdbm
- getty_ps
- glib
- gmp
- gpm
- groff
- gzip
- hdparm
- initscripts
- ipchains
- isapnptools
- ispell
- joe
- kbdconfig
- kernel
- kernel-pcmcia-cs
- kernel-smp
- ld.so
- losetup
- libc
- libstdc++
- lilo
- pwdb
- pam
- sh-utils
- redhat-release
- linuxconf
- logrotate
- losetup
- lsof
- ltrace
- mailcap
- mailx
- make
- MAKEDEV

## LISTING 3.4 continued

- man
- man-pages
- mingetty
- mkbootdisk
- mkinitrd
- #mk kickstart
- modutils
- mount
- mouseconfig
- mt-st
- mtools
- nc
- ncompress
- net-tools
- netkit-base
- newt
- ntsysv
- passwd
- perl
- portmap
- procmail
- procps
- psmisc
- pump
- quota
- raidtools
- rdist
- readline
- redhat-logos
- rhs-hwdiag
- rootfiles
- rpm
- rsh
- rsync
- sash
- screen
- sendmail
- sendmail-cf
- setconsole
- setserial
- setuptool
- slang

## LISTING 3.4 continued

- slocate
- ssh
- ssh-clients
- ssh-extras
- ssh-server
- stat
- strace
- sudo
- syslogd
- SysVinit
- tar
- tcp_wrappers
- tcpdump
- tcsh
- telnet
- time
- timeconfig
- tmpwatch
- traceroute
- ucd-snmp
- ucd-snmp-utils
- unzip
- utempter
- util-linux
- vim-common
- vim-minimal
- vixie-cron
- wget
- which
- words
- wu-ftpd
- XFree86-libs
- xntp3
- zip
- zlib

## The Administrative Template

The requirements for the administrative template differ in several important ways. In a normal administrative network, you will usually have shared resources that you make available to all systems connected to your network via the network filesystem or NFS. In addition, these systems are used for interactive work on a daily basis and therefore require software to make time spent on the systems as productive as possible. To reduce the amount of work required to maintain these systems, it is often desirable to have software that requires frequent updates on shared filesystems. In this manner, you can install a package once and have it immediately available to all users of the network. Examples of software that you might want to install in this fashion include the X Windows software, TeX, compilers, graphical user interfaces like KDE or Gnome, and office suites. The base requirements for the administrative template build on those of the production template to include the following additional features:

- Software to access shared filesystems
- Personal productivity software
- Documentation
- Word publishing software

The shared resources on the network would likely include software to support the different functions of the four types of systems found there. For example, the administrative workstations would access network-capable versions of office suites and other software from the administrative servers. The development workstations and servers would share software such as compilers and interpreters. The primary difference between the workstations and servers in both cases is the computing power of the servers and the availability of resource-intensive applications, such as databases.

## Class-Based Customization

The most difficult part of this installation strategy is developing the system by which machines are customized based on the class of machine to which they belong. In our example network, we have already identified four classes of systems on the administrative network and three on the production network. A method of achieving the customization required to make a generic system into one of the specific classes of systems is to maintain a class template, which can be installed on top of the base operating system. In addition, you could also have a function-based template, so that each function is a package that can be installed on top of the base system to add specific functionality. Let's take a look at each class and discuss how to convert a system containing the base template into a system capable of performing a specific function, starting with the administrative network.
