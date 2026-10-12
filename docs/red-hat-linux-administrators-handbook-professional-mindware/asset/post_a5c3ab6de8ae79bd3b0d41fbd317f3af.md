
As you can see, for each run level (0 through 6), a script called `/etc/rc.d/rc` is run, with the run level as the argument to the script. This script is responsible for starting and stopping all the services for the desired run level. For example, suppose that init is told to change the run level to 3. It will run the `/etc/rc.d/rc` script with an argument of 3 in a command line similar to this:

```
/etc/rc.d/rc 3
```

The `/etc/rc.d/rc` script is shown in Listing 2-2.

### Listing 2-2 The script /etc/rc.d/rc

```bash
#!/bin/bash
#
# rc This file is responsible for starting/stopping
# services when the runlevel changes. It is also
# responsible for the very first setup of basic
# things, such as setting the hostname.
#
# Original Author:
# Miquel van Smoorenburg, <miquels@drinkel.nl.mgn.net.org>
#
# Source function library.
. /etc/init.d/functions

# Now find out what the current and what the previous
# runlevel are.
argv1=$1
set `/sbin/runlevel`
runlevel=$2
previous=$1
export runlevel previous

# See if we want to be in user confirmation mode
if [ "$previous" = "N" ]; then
    if grep -i confirm /proc/cmdline >/dev/null || [ -f /var/run/confirm ]; then
        rm -f /var/run/confirm
        CONFIRM=yes
        echo "Entering interactive startup"
    else
        CONFIRM=
        echo "Entering non-interactive startup"
    fi
fi

# Get first argument. Set new runlevel to this argument.
[ -n "$argv1" ] && runlevel="$argv1"

# Tell linuxconf what runlevel we are in
[ -d /var/run ] && echo "/etc/rc$runlevel.d" > /var/run/runlevel.dir

# Is there an rc directory for this new runlevel?
if [ -d /etc/rc$runlevel.d ]; then
    # First, run the KILL scripts.
    for i in /etc/rc$runlevel.d/K*; do
        # Check if the script is there.
        [ ! -f $i ] && continue

        # Don't run [KS]??foo.{rpmsave,rpmorig}
        [ "$${i%.rpmsave}" = "$${i}" ] && continue
        [ "$${i%.rpmorig}" = "$${i}" ] && continue
        [ "$${i%.rpmnew}" = "$${i}" ] && continue

        # Check if the subsystem is already up.
        subsys=${i#/etc/rc$runlevel.d/K??}
        [ ! -f /var/lock/subsys/$subsys ] && \
        [ ! -f /var/lock/subsys/$( $subsys ).init ] && continue

        # Bring the subsystem down.
        if egrep -q "(killproc | action )" $i ;
        then
            $i stop
        else
            action "$subsys: " $i stop
        fi
    done

    # Now run the START scripts.
    for i in /etc/rc$runlevel.d/S*; do
        # Check if the script is there.
        [ ! -f $i ] && continue

        # Don't run [KS]??foo.{rpmsave,rpmorig}
        [ "$${i%.rpmsave}" = "$${i}" ] && continue
        [ "$${i%.rpmorig}" = "$${i}" ] && continue
        [ "$${i%.rpmnew}" = "$${i}" ] && continue

        # Check if the subsystem is already up.
        subsys=${i#/etc/rc$runlevel.d/S??}
        [ -f /var/lock/subsys/$subsys ] || \
        [ -f /var/lock/subsys/$( $subsys ).init ] && continue

        # If we're in confirmation mode, get user confirmation
        [ -n "$CONFIRM" ] && {
            confirm $subsys
            case $? in
                0)
                    :
                    ;;
                1)
                    CONFIRM=
                    ;;
                2)
                    continue
                    ;;
            esac
        }

        # Bring the subsystem up.
        if egrep -q "(daemon | action )" $i ; then
            $i start
        else
            if [ "$subsys" = "halt" -o \
                 "$subsys" = "reboot" -o \
                 "$subsys" = "single" -o \
                 "$subsys" = "local" ]; then
                $i start
            else
                action "Starting $subsys: " $i start
            fi
        fi
    done
fi
```

This script primarily does the following:

- Checks whether a subdirectory exists for the run level specified in the argument. In other words, if the script is run with an argument of 3, it checks to see whether or not the `/etc/rc.d/rc3.d/` directory exists. If it exists, the script continues to the next step.
- Determines whether any of the programs (often called services) that are supposed to run in the new run level are already running. If a service is already running, the script kills the service so you can restart it in the next step. To kill a running service, the script runs the necessary K script with the stop argument.
- Runs all the S scripts with the start argument.

## The /etc/rc0.d through rc6.d directories

The rc0.d to rc6.d subdirectories are used for run levels 0 to 6. These directories contain symbolic links to scripts in the `/etc/init.d` directory. Take a look at the rc3.d directory in an example Red Hat Linux 7.0 system. This directory lists the symbolic links shown in Listing 2-3.

### Listing 2-3 A directory listing of /etc/rc.d/rc3.d

```
lrwxrwxrwx 1 root root  14 Mar  3  2001 K05innd -> ../init.d/innd
lrwxrwxrwx 1 root root  15 Mar  3  2001 K10xntpd -> ../init.d/xntpd
lrwxrwxrwx 1 root root  13 Mar  3  2001 K15gpm -> ../init.d/gpm
lrwxrwxrwx 1 root root  15 Mar  3  2001 K15httpd -> ../init.d/httpd
lrwxrwxrwx 1 root root  20 Mar  3  2001 K15postgresql -> ../init.d/postgresql
lrwxrwxrwx 1 root root  20 Mar  3  2001 K20bootparam -> ../init.d/bootparam
lrwxrwxrwx 1 root root  17 Mar  3  2001 K20ruserd -> ../init.d/ruserd
lrwxrwxrwx 1 root root  16 Mar  3  2001 K20rwhod -> ../init.d/rwhod
lrwxrwxrwx 1 root root  15 Mar  3  2001 K25squid -> ../init.d/squid
lrwxrwxrwx 1 root root  15 Mar  3  2001 K34ypasswdd -> ../init.d/ypasswdd
lrwxrwxrwx 1 root root  15 Mar  3  2001 K35chcpd -> ../init.d/chcpd
lrwxrwxrwx 1 root root  16 Mar  3  2001 K35yppasswdd -> ../init.d/yppasswdd
lrwxrwxrwx 1 root root  14 Mar  3  2001 K45arpwatch -> ../init.d/arpwatch
lrwxrwxrwx 1 root root  15 Mar  3  2001 K50snmpd -> ../init.d/snmpd
lrwxrwxrwx 1 root root  15 Mar  3  2001 K55routed -> ../init.d/routed
lrwxrwxrwx 1 root root  15 Mar  3  2001 K75gated -> ../init.d/gated
lrwxrwxrwx 1 root root  16 Mar  3  2001 K87ypbind -> ../init.d/ypbind
lrwxrwxrwx 1 root root  16 Mar  3  2001 K96pcmcia -> ../init.d/pcmcia
lrwxrwxrwx 1 root root  17 Mar  3  2001 S01kernel -> ../init.d/kernel
lrwxrwxrwx 1 root root  17 Mar  3  2001 S10network -> ../init.d/network
lrwxrwxrwx 1 root root  17 Mar  3  2001 S10portmap -> ../init.d/portmap
lrwxrwxrwx 1 root root  15 Mar  3  2001 S10nfsfs -> ../init.d/nfsfs
lrwxrwxrwx 1 root root  16 Mar  3  2001 S20random -> ../init.d/random
lrwxrwxrwx 1 root root  16 Mar  3  2001 S30syslog -> ../init.d/syslog
lrwxrwxrwx 1 root root  13 Mar  3  2001 S40atd -> ../init.d/atd
lrwxrwxrwx 1 root root  15 Mar  3  2001 S40crond -> ../init.d/crond
lrwxrwxrwx 1 root root  14 Mar  3  2001 S50inet -> ../init.d/inet
lrwxrwxrwx 1 root root  15 Mar  3  2001 S55named -> ../init.d/named
lrwxrwxrwx 1 root root  13 Mar  3  2001 S60lpd -> ../init.d/lpd
lrwxrwxrwx 1 root root  13 Mar  3  2001 S60nfs -> ../init.d/nfs
lrwxrwxrwx 1 root root  18 Mar  3  2001 S75keytable -> ../init.d/keytable
lrwxrwxrwx 1 root root  18 Mar  3  2001 S80sendmail -> ../init.d/sendmail
lrwxrwxrwx 1 root root  13 Mar  3  2001 S91smb -> ../init.d/smb
lrwxrwxrwx 1 root root  19 Mar  3  2001 S99linuxconf -> ../init.d/linuxconf
lrwxrwxrwx 1 root root  11 Mar  3  2001 S99local -> ../rc.local
```

Notice that scripts from the `/etc/init.d` directory are linked in two ways. Some scripts are linked as follows:

```
K{two-digit number}f{script name}
```

Other scripts are linked as shown here:

```
S{two-digit number}f{script name}
```

All the scripts that are prefixed with K are run with the stop argument, and all the scripts that are prefixed with S are run with the start argument. The two-digit number is used to set the execution order. Thus, a script called `S01foo` will be run before `S01bar`. These S and K scripts are run by the `/etc/rc.d/rc` script.

After the rc script is finished, the processing done by init also finishes, and the system becomes available in the new run level.

## The /etc/rc.d/rc.local script

The rc.local script typically is run once at the end of run levels 2, 3, and 5. You can add anything that needs to be run once per boot in this file.

## The /etc/rc.d/rc.serial script

The rc.serial script typically is run once at the end of run level 1 or 3 to initialize serial ports.

## Booting Up Your System

During the bootup process, init first runs the rc.sysinit script and then runs the script for the default run level. The default run level is set in `/etc/inittab`, using a line such as the following:

```
id:3:initdefault:
```

Here, the default run level is set to 3. This means that init will run the script needed to put the system in multiuser mode.

Looking back at Listing 2-1, the following line specifies what needs to be run for run level 3:

```
1:3:wait:/etc/rc.d/rc 3
```

The rc script is run with an argument of 3. As previously mentioned, this script runs all the scripts whose names start with S in the `/etc/rc.d/rc3.d` directory. It also supplies start as an argument to each of the S-prefixed scripts. After all the S scripts are run, the rc script finishes and the system becomes available at the default run level.

![](img/f9ec99365f159bfe663f8ac29732663c_59_0.png)

## Tip

It is possible to override the default run level at the LILO prompt. For example, if you want to boot the system in single-user mode, you can specify `linux single` to boot in single-user mode. If you use a label other than "linux" to boot Linux, you have to specify `yourlabel single`, instead, where `yourlabel` is the name of the appropriate label.
