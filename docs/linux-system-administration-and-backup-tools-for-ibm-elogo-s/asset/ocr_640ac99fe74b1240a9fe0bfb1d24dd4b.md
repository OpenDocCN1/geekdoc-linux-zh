**dmesg.** is this command that you run runtime and will display the messages that you see on bootup.

**Mail.** Linux will mail you a copy of the configuration and bootup messages for every reboot. This can be more extensive than the messages from `dmesg`. To access these messages type `mail`.

**turbow.** The `turbow` command will probe your TurboLinux system and will give you a listing of hardware that it finds. It also allows you to generate a text file with detailed information on the hardware installed in your machine, including currently used resources (for example, IRQ, IO ports).

# 5.8 Server Services

Linux uses a concept of runlevels (0-6) to manage the operation of the system. On boot, the system reads the file /etc/initab to determine which runlevel it should enter. Then it reads the subdirectories under /etc/rc.d that conform to that runlevel. The runlevel directories are:

+   - /etc/rc.d/rc0.d
- /etc/rc.d/rc1.d
- /etc/rc.d/rc2.d
- /etc/rc.d/rc3.d
- /etc/rc.d/rc4.d
- /etc/rc.d/rc5.d
- /etc/rc.d/rc6.d

For example, if the runlevel is set to 3, which is the level TurboLinux sets if you ask for a text-mode login during the install, the system reads the directory /etc/rc.d/rc3.d/ and starts or stops services based on the scripts in that directory.

The directory contains a number of symbolic links that point to scripts created to start, stop, and restart all the services provided by Linux. Looking at the directory, you will notice the files look similar. Below are a few examples from /etc/rc.d/rc3.d:

```
S0network
S11port
S14nfslock
S15nfs
```

You can see that they conform to the format [K or S]number less than 100[[filename]]. Each part may be explained as follows: