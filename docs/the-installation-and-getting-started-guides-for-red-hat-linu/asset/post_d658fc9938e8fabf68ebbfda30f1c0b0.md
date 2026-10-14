
init.d contains a bunch of scripts. Basically, you require one script for each service you may need to start at boot time or when entering another runlevel. Services include things like networking, nfs, sendmail, httpd, etc. Services do not include things like setserial that must only be run once and then exited. Things like that should go in rc.local or rc.serial. If you want rc.local, it should be in /etc/rc.d. Most systems include one even though it doesn't do much. You can also include an rc.serial in /etc/rc.d if you need to do serial port specific things at boot time. The chain of events is as follows:

- The kernel looks in several places for init and runs the first one it finds
- init runs /etc/rc.d/rc.sysinit
- rc.sysinit does a bunch of necessary things and then runs rc.serial (if it exists)
- init runs all the scripts for the default runlevel.
- init runs rc.local

The default runlevel is decided in /etc/inittab. You should have a line close to the top like:

```
id:3:initdefault:
```

From this, you'd look in the second column and see that the default runlevel is 3, as should be the case for most systems. If you want to change it, you can edit /etc/inittab by hand and change the 3. Be very careful when you are messing with the inittab. If you do mess up, you can fix it by rebooting and doing:

```
LILO boot: linux single
```

This should allow you to boot into single user mode so you can fix inittab. Now, how does it run all the right scripts? If you enter ls -l on rc3.d, you might see something like:

```
lrwxrwxrwx 1 root root 17 3:11 S10network -> ../init.d/network
lrwxrwxrwx 1 root root 16 3:11 S30syslog -> ../init.d/syslog
lrwxrwxrwx 1 root root 14 3:32 S40cron -> ../init.d/cron
lrwxrwxrwx 1 root root 14 3:11 S50inet -> ../init.d/inet
lrwxrwxrwx 1 root root 13 3:11 S60nfs -> ../init.d/nfs
lrwxrwxrwx 1 root root 15 3:11 S70nfsfs -> ../init.d/nfsfs
lrwxrwxrwx 1 root root 18 3:11 S90lpd -> ../init.d/lpd.init
lrwxrwxrwx 1 root root 11 3:11 S99local -> ../rc.local
```

What you'll notice is that there are no real "files" in the directory. Everything there is a link to one of the scripts in the init.d directory. The links also have an "S" and a number at the beginning. The "S" means to start this particular script and a "K" would mean to stop it. The number is there just for ordering purposes. Init will start all the services based on the order in which they appear. You can duplicate numbers, but it will only confuse you somewhat. You only need to use a two digit number, along with an upper case "S" or "K" to start or stop the services you require to. How does init start and stop services? Simple. Each of the scripts is written to accept an argument which can be "start" and "stop." You can execute those scripts by hand, in fact, with a command like:

```
/etc/rc.d/init.d/httpd.init stop
```

to stop the httpd server. Init just reads the name and if it has a "K," it calls the script with the "stop" argument. If it has an "S" it calls the script with a "start" argument. Why all these runlevels? Some people want an easy way to set up machines to be multipurpose. You could have a "server" runlevel that just runs httpd, sendmail, networking, etc. Then you could have a "user" runlevel that runs xdm, networking, etc.

## Init Runlevels

Generally, Red Hat Linux operates in run level 3—full multiuser mode. The following runlevels are defined in Red Hat Linux:

| Runlevel | Description |
|----------|-------------|
| 0 | Halt |
| 1 | Single user mode |
| 2 | Multiuser mode, without NFS |
| 3 | Full multiuser mode |
| 4 | Not used |
| 5 | Full multiuser mode (with an X-based login screen) |
| 6 | Reboot |

If your machine gets into a state where it will not boot due to a bad /etc/inittab, or will not let you log in because you have a corrupted /etc/passwd or have simply forgotten your password, boot into single user mode by typing linux 1 at the LILO boot prompt. A very bare system will come up and you will be given a shell from which you can fix things.

## Initscript Utilities

The `chkconfig` utility provides a simple command-line tool for maintaining the `/etc/rc.d` directory hierarchy. It relieves system administrators from having to directly manipulate the numerous symlinks in `/etc/rc.d`. In addition, there is the `ntsysv` utility, that provides a screen-oriented interface, versus chkconfig's command-line interface. Please see the chkconfig and ntsysv man pages for more information.
