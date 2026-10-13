
## The /etc/rc.d/rc.sysinit script

As you already know, when a Red Hat Linux system boots, the kernel runs init, which in turn runs the /etc/rc.d/rc.sysinit script before processing any other scripts for the desired run level. The following line in the /etc/inittab file causes init to run this script before running anything else:

```
si::sysinit:/etc/rc.d/rc.sysinit
```

Notice that the run level field is empty, because init recognizes sysinit as a system initialization action. The rc.sysinit script does many things, including setting the host name, enabling the swap partition, checking the file systems, loading kernel modules, and more. Typically, you do not need to modify this script.

## The /etc/rc.d/init.d directory

The init.d subdirectory is used to store all the scripts needed for all the run levels. Keeping all the scripts in one location makes managing them easier. Each script is used to start/stop a particular service—Domain Name Service (DNS), Web service, or another such service. All of these scripts follow a special command-line argument syntax. For example, to start NFS (Network File System) service, you can run the following script:

/etc/rc.d/init.d/nfs start

To stop the same service, you can run the same script as follows:

/etc/rc.d/init.d/nfs stop

The nfs script takes start and stop as arguments. This is true for all the scripts in this directory, which are symbolically linked to the rc0.d through rc6.d directories, as needed.

## The /etc/rc.d/rc script

When init is told to change the run level to one of the seven possible run levels, it runs a script specified in one of the following lines in the /etc/inittab file:

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

As you can see, for each run level (0 through 6), a script called /etc/rc.d/rc is run, with the run level as the argument to the script. This script is responsible for starting and stopping all the services for the desired run level. For example, suppose that init is told to change the run level to 3. It will run the /etc/rc.d/rc script with an argument of 3 in a command line similar to this:

/etc/rc.d/rc 3

The /etc/rc.d/rc script is shown in Listing 2-2.

### Listing 2-2 The Script /etc/rc.d/rc

```
#!/bin/bash

# rc This file is responsible for starting/stopping
# services when the runlevel changes. It is also
# responsible for the very first setup of basic
# things, such as setting the hostname.

# Original Author: Miquel van Smoorenburg,
#                 <miquels@drinkel.nl.mugnet.org>
#

# Source function library.
. /etc/rc.d/init.d/functions

# Now find out what the current and what the previous
# runlevel are.
argvl="$1"
set `/sbin/runlevel`
runlevel=$2
previous=$1
export runlevel previous

# Get first argument. Set new runlevel to this argument.
[ "$1" != "" ] && runlevel="$argvl"

# Tell linuxconf what runlevel we are in
[ -d /var/run ] && echo "/etc/rc.d/rc$runlevel.d" > /var/run/runlevel.dir

# Is there an rc directory for this new runlevel?
if [ -d /etc/rc.d/rc$runlevel.d ]; then
# First, run the KILL scripts.
for i in /etc/rc.d/rc$runlevel.d/K*; do
# Check if the script is there.
[ ! -f $i ] && continue

# Don't run [KS]??foo.{rpmsave,rpmorig} scripts
[ "${i%.rpmsave}" != "${i}" ] && continue
[ "${i%.rpmorig}" != "${i}" ] && continue

# Check if the subsystem is already up.
subsys=$(/etc/rc.d/rc$runlevel.d/K??)
[ ! -f /var/lock/subsys/$subsys ] && \
[ ! -f /var/lock/subsys/${subsys}.init ] && continue

# Bring the subsystem down.
$i stop

done

# Now run the START scripts.
for i in /etc/rc.d/rc$runlevel.d/S*; do
# Check if the script is there.
[ ! -f $i ] && continue

# Don't run [KS]??foo.{rpmsave,rpmorig} scripts
[ "${i%.rpmsave}" != "${i}" ] && continue
[ "${i%.rpmorig}" != "${i}" ] && continue

# Check if the subsystem is already up.
subsys=$(if /etc/rc.d/rc$runlevel.d/S??)
[ -f /var/lock/subsys/$subsys ] || \
[ -f /var/lock/subsys/${subsys}.init ] && continue

# Bring the subsystem up.
$i start

done
fi
```

This script primarily does the following:

- Checks whether a subdirectory exists for the run level specified in the argument. In other words, if the script is run with an argument of 3, it checks to see whether or not the /etc/rc.d/rc3.d/ directory exists. If it exists, the script continues to the next step.
- Determines whether any of the programs (often called services) that are supposed to run in the new run level are already running. If a service is already running, the script kills the service so that it can restart it in the next step. To kill a running service, the script runs the necessary "K" script with the stop argument.
- Runs all the "S" scripts with the start argument.

## The /etc/rc.d/rc0.d through rc6.d directories

The rc0.d to rc6.d subdirectories are used for run levels 0 to 6. These directories contain symbolic links to scripts in the /etc/rc.d/init.d directory.

Take a look at the rc.d directory in an example Red Hat Linux 6.1 system. This directory lists the symbolic links shown in Listing 2-3.

### Listing 2-3 A Directory Listing of /etc/rc.d/rc3.d

```
lrwxrwxrwx root root 14 K05innd -> ../init.d/innd
lrwxrwxrwx root root 15 K10xntpd -> ../init.d/xntpd
lrwxrwxrwx root root 13 K15gpm -> ../init.d/gpm
lrwxrwxrwx root root 15 K15httpd -> ../init.d/httpd
lrwxrwxrwx root root 20 K15postgresql -> ../init.d/postgresql
lrwxrwxrwx root root 20 K20bootparamd -> ../init.d/bootparamd
lrwxrwxrwx root root 17 K20usersd -> ../init.d/usersd
lrwxrwxrwx root root 16 K20rwalld -> ../init.d/rwalld
lrwxrwxrwx root root 15 K20rwhod -> ../init.d/rwhod
lrwxrwxrwx root root 15 K25squid -> ../init.d/squid
lrwxrwxrwx root root 19 K34ypasswdd -> ../init.d/ypasswdd
lrwxrwxrwx root root 15 K35dhcpd -> ../init.d/dhcpd
lrwxrwxrwx root root 16 K35ypserv -> ../init.d/ypserv
lrwxrwxrwx root root 18 K45arpwatch -> ../init.d/arpwatch
lrwxrwxrwx root root 15 K50snmpd -> ../init.d/snmpd
lrwxrwxrwx root root 16 K55routed -> ../init.d/routed
lrwxrwxrwx root root 17 K75gated -> ../init.d/gated
lrwxrwxrwx root root 16 K87ypbind -> ../init.d/ypbind
lrwxrwxrwx root root 16 K96pcmcia -> ../init.d/pcmcia

lrwxrwxrwx root root 17 S01kerneld -> ../init.d/kerneld
lrwxrwxrwx root root 17 S10network -> ../init.d/network
lrwxrwxrwx root root 17 S11portmap -> ../init.d/portmap
lrwxrwxrwx root root 15 S15nfsfs -> ../init.d/nfsfs
lrwxrwxrwx root root 16 S20random -> ../init.d/random
lrwxrwxrwx root root 16 S30syslog -> ../init.d/syslog
lrwxrwxrwx root root 13 S40atd -> ../init.d/atd
lrwxrwxrwx root root 15 S40crond -> ../init.d/crond
lrwxrwxrwx root root 14 S50inet -> ../init.d/inet
lrwxrwxrwx root root 15 S55named -> ../init.d/named
lrwxrwxrwx root root 13 S60lpd -> ../init.d/lpd
lrwxrwxrwx root root 13 S60nfs -> ../init.d/nfs
lrwxrwxrwx root root 18 S75keytable -> ../init.d/keytable
lrwxrwxrwx root root 18 S80sendmail -> ../init.d/sendmail
lrwxrwxrwx root root 13 S91samba -> ../init.d/smb
lrwxrwxrwx root root 19 S99linuxconf -> ../init.d/linuxconf
lrwxrwxrwx root root 11 S99local -> ../rc.local
```

Notice that scripts from the /etc/rc.d/init.d directory are linked in two different ways. Some scripts are linked as follows:

```
K{two-digit number}{script name}
```

Other scripts are linked as shown here:

```
S{two-digit number}{script name}
```

All the scripts that are prefixed with K are run with the stop argument, and all the scripts that are prefixed with S are run with the start argument. The two-digit number is used to set the execution order. Thus, a script called S01foo will be run before S10bar. These S and K scripts are run by /etc/rc.d/rc script.

After the rc script is finished, the processing done by init also finishes, and the system becomes available in the new run level.

## The /etc/rc.d/rc.local script

The rc.local script typically is run once at the end of run levels 2, 3, and 5. You can add anything that needs to be run once per boot in this file.

## The /etc/rc.d/rc.serial script

The rc.serial script typically is run once at the end of run level 1 or 3 to initialize serial ports.
