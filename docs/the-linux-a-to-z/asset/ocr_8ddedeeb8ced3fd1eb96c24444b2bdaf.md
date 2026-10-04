```
# cp /vmlinuz /dev/fd0
```

You should now be able to boot the system with your new floppy in just the same way as you will with the floppy created during the setup procedure.

# 7.3.5 The Reboot Procedure

Unless you tried to install lilo during setup you will have to boot your Linux system from floppy disk for the time being. Having two boot floppy disks available, now is a good time to reboot your system to check that all is well – don’t forget you are still running with the root filesystem on a RAM disk at the moment!

Reboot time is one of those particular times when you need to remember that Linux is a big-machine operating system. Under no normal circumstances should you shut down Linux by just switching the machine off or by pressing the reset switch – Linux needs to be shut down properly. Quite a lot of the work that Linux does is retained in memory for as long as possible rather than writing it to disk. The obvious reason for this is that accessing data in memory is orders of magnitude faster than accessing the same data on disk. One consequence of this, however, is that when you want to shut Linux down you need to give it advanced warning so that it has time to transfer all this memory resident data to disk before you pull the plug.

The safest way to shut Linux down is to use the shutdown command. The general form of this command is:

```
shutdown flags time [message]
```

The shutdown command can only be executed by a user logged in as root and when it is given, message is sent to all users. If no message is specified then a default shutdown warning will be given. When shutdown time arrives a SIGTERM signal is sent to all processes to give them the opportunity to terminate cleanly, before the shutdown proper takes place.

The main flags are the command line switches: -h which means halt the machine after the shutdown and -r which means reboot the machine instead. The time parameter specifies when the shutdown should take place. It can be specified as an absolute time in the format hh:mm or it can be given as a number of minutes from the current time, in the format +mm. The word now can be used to mean +0 minutes.

During its operation, the shutdown command ensures that the disk data contents are synchronized with the data stored in memory so that no data will be lost. The following command will shut Linux down immediately and then halt the machine:

```
# shutdown -h now
```

It is also possible to configure the Linux kernel to reboot the machine when you press Ctrl-Alt-Del. This action can obviously be performed by anyone, at