
## 138 Linux Administration: A Beginner's Guide

In the runlevel directories, symbolic links are made to scripts in the `/etc/rc.d/init.d/` directory. Instead of using the name of the script as it exists in the `/etc/rc.d/init.d/` directory, however, the symbolic links are prefixed with an `S` if the script is to start a service, or with a `K` if the script is to stop (or kill) a service. (See Chapter 6 for information on symbolic links.)

In many cases, the order in which these scripts are run makes a difference. (You can't use DNS to resolve hostnames if you haven't yet configured a network interface!) To enforce order, a two-digit number is suffixed to the S or K. Lower numbers execute before higher numbers; for example, `/etc/rc5.d/S10network` starts before `/etc/rc5.d/S51named` starts (which configures the network settings and then starts the DNS server).

The scripts pointed to in the `/etc/rc.d/init.d/` directory are the workhorses; they perform the actual process of starting and stopping services. When `/etc/rc4.d/rc` runs through a specific runlevel's directory, it invokes each script in numerical order. It first runs the scripts that begin with a K, and then the scripts that begin with an S. For scripts starting with K, a parameter of `stop` is passed. Likewise, for scripts starting with S, the parameter `start` is passed.

Let's peer into the `/etc/rc.d/2.d/` directory and see what's there:

```
[root@froot rc2d]# ls -l

total 0
lrwxrwxrwx  1 root  root     15 Aug 11 1998 S32hspd -> ../init.d/hspd
lrwxrwxrwx  1 root  root     15 Jul 29  1998 S51sound -> ../init.d/sound
lrwxrwxrwx  1 root  root     16 Jun 10  09:16 K20rsatd -> ../init.d/rsatd
lrwxrwxrwx  1 root  root     17 Jul 29  1998 K42syslog -> ../init.d/syslogd
lrwxrwxrwx  1 root  root     15 Jul 29  1998 K51svcd -> ../init.d/svcd
lrwxrwxrwx  1 root  root     16 Sep 27  1998 K22dipimd -> ../init.d/dipimd
lrwxrwxrwx  1 root  root     19 Sep 27  1998 K53x3sysd -> ../init.d/x3sysd
lrwxrwxrwx  1 root  root     19 Sep 27  1998 S35x3d -> ../init.d/x3d
lrwxrwxrwx  1 root  root     16 Sep 27  1998 K35sysrep -> ../init.d/sysrep
lrwxrwxrwx  1 root  root     15 Feb 22  22:02 K58named -> ../init.d/named
lrwxrwxrwx  1 root  root     19 Jun 19  1998 S30init -> ../init.d/init
lrwxrwxrwx  1 root  root     14 Jul 29  1998 K32reboot -> ../init.d/reboot
lrwxrwxrwx  1 root  root     13 Jul 29  1998 K48xfsd -> ../init.d/xfsd
lrwxrwxrwx  1 root  root     15 Jun 19  09:32 S55serv -> ../init.d/fta
lrwxrwxrwx  1 root  root     17 Jun 19  09:32 S19portmap -> ../init.d/portmap
lrwxrwxrwx  1 root  root     14 Jun 19  09:29 S19swap -> ../init.d/swapd
lrwxrwxrwx  1 root  root     17 Jul 29  1998 S15network -> ../init.d/network
lrwxrwxrwx  1 root  root     14 Jul 29  1998 S25mandas -> ../init.d/mandas
lrwxrwxrwx  1 root  root     15 Jul 29  1998 S31x3log -> ../init.d/x3log
lrwxrwxrwx  1 root  root     15 Jul 29  1998 S41crond -> ../init.d/crond
lrwxrwxrwx  1 root  root     16 Jan 19  1998 S53pcfd -> ../init.d/pcfd
lrwxrwxrwx  1 root  root     13 Jun 19  1998 S56ipd -> ../init.d/ipdd
lrwxrwxrwx  1 root  root     19 Jun 29  1998 S50smail -> ../init.d/smail
lrwxrwxrwx  1 root  root     13 Jul 29  1998 S38dns -> ../init.d/dns
lrwxrwxrwx  1 root  root     23 Jul 29  19 1998 U11umount -> ../init.d/11umount
lrwxrwxrwx  1 root  root     11 Jun 19  1998 D981local -> ../etc.local
```

Thus, when `K50` is invoked, it really starts `/etc/rc.d/init.d/<sub> stop`. Instead, if `S90xfs` is invoked, `/etc/rc.d/init.d/xfs start` is what really gets run.

## Writing Your Own rc Script

In the course of keeping a Linux system running, you will, at some point, need to modify the startup or shutdown scripts. There are two roads you can take to doing this:

- If your change is to be affected at boot time only, and the change is small, you may want to simply edit the `/etc/rc.d/rc.local` script. This script gets run at the very end of the boot process.
- On the other hand, if your addition is more elaborate and/or requires that the shutdown process explicitly stop, you should add a script to the `/etc/rc.d/init.d` directory. This script should take the parameters `start` and `stop` and act accordingly.

The first option, editing the `/etc/rc.d/rc.local` script, is of course the easier of the two. To make additions to this script, simply open it in your editor of choice and append the commands you want run at the end. This is good for simple one- or two-line changes.

If you do need a separate script, however, you will need to take the second option. The process of writing an rc script is not as difficult as it may seem. Let's step through it using an example, to see how it works. (You can use our example as a skeleton script, by way, changing it to add anything you need.)

Assume you want to start a special program that pops up a message every 60 minutes and reminds you that you need to take a break from the keyboard (a good idea if you don't want to get carpal tunnel syndrome!). The script will include the following:

- A description of the script's purpose (so we don't forget it a year later!)
- Verification that the program really exists before trying to start it
- Acceptance of the `start` and `stop` parameters and performance of the required actions

Given these parameters, here's the script we will write. (Notice that lines starting with a `#` symbol are comments only and not part of the script's actions, except for the first line.)

```
#!/bin/sh
#
# Carpa. Start/Stop the Carpal Notice Daemon
#
# description: Carpald is a program which wakes up every 60 minutes and
# tells us that we need to take a break from the keyboard
# or we'll lose all functionality of our wrists and never
# be able to type again as long as we live.
#
# processname: carpald

# Source function library.
. /etc/rc.d/init.d/functions

[ -f /usr/local/sbin/carpald ] || exit 0

# See how we were called.
case "$1" in
start)
echo -n "Starting carpald: "
daemon carpald
echo
touch /var/lock/subsys/carpald
;;
stop)
echo -n "Stopping carpald services: "
killproc carpald
echo
rm -f /var/lock/subsys/carpald
;;
status)
status carpald
;;
restart|reload)
$0 stop
$0 start
;;
*)
echo "Usage: carpald [start|stop|status|restart|reload]"
exit 1
esac

exit 0
```

Once you have a new script written, simply add the necessary symbolic links (symlinks, as described in Chapter 6) from the appropriate runlevel directory to have the script either start or stop. In our sample script, we want it to start only in either runlevel 3 or runlevel 5. This is because we are assuming these are the only two runlevels during which we will do normal day-to-day work. Lastly, we want the daemon to be shut down when we go to runlevel 6 (reboot). Here are the commands we enter to create the required symlinks:

```
[root@ford /root]# cd /etc/rc.d/rc3.d
[root@ford rc3.d]# ln -s ../init.d/carpald S99carpald
[root@ford rc3.d]# cd ..
[root@ford /etc/rc.d]# cd rc5.d
[root@ford rc5.d]# ln -s ../init.d/carpald S99carpald
[root@ford rc5.d]# cd ..
[root@ford /etc/rc.d]# cd rc6.d
[root@ford rc6.d]# ln -s ../init.d/carpald K00carpald
```

Notice that for runlevels 3 and 5 we used the number 99 before the S prefix; this ensures that the script will be one of the last things to get started as part of the boot process. For runlevel 6, we wanted the opposite—carpald should shut down before the rest of the components. The sequence for starting components generally goes from most critical to least critical, whereas shutting components goes from least critical to most critical.

Seems rather elaborate, doesn't it? Well, the good news is that now that we've set up its script, we won't ever need to do it again. More importantly, the script will automatically run during startup and shutdown and be able to manage itself. The overhead up front is well worth the long-term benefits.

## Enabling and Disabling Services

At times, you may find that you simply don't need a particular service to be started at boot time. This is especially true if you are considering Linux as a replacement for a Windows NT File and Print server.

As described in the preceding sections, you can cause a service not to be started by simply renaming the symbolic link in a particular runlevel directory; rename it to start with a K instead of an S. Once you are comfortable with working the command line and the symbolic links, you'll find this to be the quickest way of enabling and disabling services.

While getting your feet wet in this process, however, you may find the graphical interface, `system-config-services` (or similar GUI tool, often referred to in context as the service manager), easier to deal with. Although it was designed for use with the KDE environment, it will work with the default installed GNOME environment under Red Hat Linux 6.0. To start it, simply open an xterm window and type in the command. A window will pop up displaying all of your options, including a help section if you need it (see Figure 7-1).
