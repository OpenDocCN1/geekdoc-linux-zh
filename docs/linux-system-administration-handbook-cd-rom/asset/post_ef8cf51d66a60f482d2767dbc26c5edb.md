
## Compile the Kernel and Modules

To properly build the kernel, issue the following commands:

```
# make depend
<vmlinux
<lots of output here>
# make clean
<lots of output here>
# make
<several bucketloads of output here
```

Now, if you want to install the compressed kernel in the root partition, type

```
# make zlilo
<output ending in...>
tools/build bootsect compressed/vmlinux.out > zImage
Root device is (8, 1)
Boot sector 512 bytes.
Setup is 4348 bytes.
System is 368 kb
sync
if [ -f /vmlinuz ]; then mv /vmlinuz.old; fi
if [ -f /System.map ]; then mv /System.map /System.old; fi
cat zImage > /vmlinuz
cp /usr/src/linux/System.map //
if [ -x /sbin/lilo ]; then /sbin/lilo; else /etc/lilo/install; fi
Added 1
Added 12
Added 13
```

make[1]: Leaving directory `/usr/src/linux-2.0.29/arch/i386/boot`

This command installs the kernel and reruns lilo to update the boot map. If you want to install it on a floppy disk, make zImage (instead of zlilo) and copy the image to a high-density floppy.

```
# cp /usr/src/linux/arch/i386/boot/zImage /dev/fd0
```

Reboot your machine with the new kernel:

```
# /sbin/reboot
```

If the kernel doesn't boot, you can reboot again (using the familiar CONTROL-ALT-DELETE key sequence) and at the LILO: prompt tell it which other kernel to boot. As you can see from the above output, there are three kernels installed. If you typed “12” at the LILO: prompt, the kernel whose label is “12” in /etc/lilo.conf will be booted. Now check your hardware and its settings against your configuration (just run make xconfig and it will load your last configuration into the GUI).

## 18.7 Summary

Hopefully we've managed to take some of the intimidation out of the process of compiling your own kernel. On the other hand, we also want to be sure that you take a few simple precautions in case you make a kernel that won't boot up on your system.

If you are interested in the inner workings of the kernel, you can consult various HOWTOs, in particular the Kernel Hacking HOWTO for Linux-specific information or any of a number of books on general OS theory and design.

For more detailed information on booting and LILO, see the chapter on booting and shutdown.

## System 19 Monitoring

Using syslog to keep an eye on your system.

Monitor your Linux machine from the console or remotely using the syslog program.

The syslog program monitors kernel and user events and routes the messages based on what you want to do. These events can be minor things, such as root logging in, or can be serious, such as a hard drive failure, kernel panic, or reboot.

The syslog program gets started up at boot time and uses the /etc/syslog.conf file to know what to do. Here's the default file for RedHat 4.1:

```
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
kern.* /dev/console
```

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages.
*.info;mail.none;authpriv.none /var/log/messages
```

```
# The authpriv file has restricted access.
authpriv.*                                     /var/log/secure
```

```
# Log all the mail messages in one place.
mail.*                                            /var/log/maillog
```

```
# Everybody gets emergency messages, plus log them on another
# machine.
  *.emerg
```

```
# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit                                 /var/log/spooler
```

Any line with a # in front of it is ignored and is a comment. Each line is an entry and consists of two fields. The first field lists the events to monitor. The second field lists what to do when that event has occurred.

Each event is in two parts, separated by a period. The first part is the facility, or type of program generating the event. The second part is the priority or severity of the event, ranging from debug to emerg.
There are twenty facilities available:

- auth
- auth-priv
- cron
- daemon
- kern
- lpr
- mail
- mark
- news
- syslog
- user
- uucp
- local0 through local1

There are eight priorities available:

- debug
- info
- notice
- warning
- err
- crit
- alert
- emerg

### 19.1 Facilities and Priorities

The facility/priority combination that you list will then report all the messages that get sent to syslog for that priority and higher. A priority of debug will report all messages. A priority of emerg will report only emergency messages.

### 19.2 Actions

The facility/priority combination that you list will then report all the messages that get sent to syslog for that priority and higher. A priority of debug will report all messages. A priority of emerg will report only emergency messages.

### 19.3 Logging Procedures

How you log depends on what you want to log. For an initial setup, you should probably start by logging just about everything. As the system becomes stable and it is working correctly, continue debugging but change the priority to something like warn or err.

### 19.4 Summary

One of the keys of having a long uptime is knowing everything that is going on the system. By monitoring your machine carefully, you can catch potential problems or breakouts as they occur, and fix the problem before it gets out of hand.

## Backing Up 20 Your Data

> When all else fails . . . restore from backup!

Keeping good backups is frequently the only way to recover from many accidents, disasters, or break-ins. Linux has a number of methods for archiving your data, ranging from tools like tar or cpio to drives that come with Linux to feature-rich, sophisticated commercial packages.

There are a number of ways to keep backups, ranging from simply taring your entire file system to a tape using dump and a well-designed backup schedule to running a high-end commercial backup and restore program.

Of course, you also have a variety of backup media to choose from: floppies (if you are truly desperate), tape drives (from old nine up to DAT), write once, read many (WORM) drives, magneto-optical floppies (written magnetically, read optically), and Zip and Jaz drives. Of these, only the newer tape options and Jaz drives have gigabyte capacity and only exabyte and DAT can handle more than a couple of gigabytes. Unfortunately, tapes are in many ways the most cumbersome to work with because of their sequential access nature.
