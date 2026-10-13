+   - The `-k` option sends out a fake shutdown message and does not really shut down the machine.
+   - The `-n` option causes shutdown to kill processes itself and not by calling `init`. It turns off quota, accounts, and swapping, and unmounts all file systems. The use of this option is not recommended because it might not behave exactly as expected.
+   - The `-f` option instructs `init` to skip running `fsck` on reboot. `shutdown` creates a file `/fastboot` which is checked at boot time, and if found, the file is removed and `fsck` is skipped.
+   - The `-F` option forces `fsck` to run on reboot. `shutdown` creates a file `/forcefsck` which is checked at boot time, and if found, the file is removed and `fsck` is run.
+   - The `-c` option is used to cancel an already running shutdown command.
+   - The time argument specifies when to shut down the machine. It can be specified in an absolute time format (`hh:mm`), or a relative “minutes from now” format. The relative format uses a plus sign; for instance, `+5` means shutdown in five minutes from now. The special time now can be used to initiate an immediate system shutdown.
+   - The warning message is the message sent to all logged-in users.

The following is a typical shutdown:

```
shutdown -h +5 "System maintenance shutdown - Please log out now"
```

This command indicates that the system should be halted in five minutes and that the message System maintenance shutdown - Please log out now will be sent to all logged-in users.

# telinit AND init

The programs telinit and init can be used to shut down a machine. When these methods of shutdown are used, no message is sent to logged-in users. These commands are useful when broadcasting of shutdown messages to all users is not desired, such as when rebooting a special-purpose server that does not have logged-on users (a DNS or DHCP server, for instance). Examples of using telinit and init to shut down a machine are

```
# telinit 0

or

# init 0
```

These commands instruct init to switch to run level 0, the halt state. Similarly, telinit 1 or init 1 place the system in single-user mode and telinit 6 and init 6 reboot the system by changing to run level 6.

# halt

Running halt causes the shutdown -h command to be executed, halt logs the shutdown, kills the system processes, executes a sync system call to write the data in memory buffers to disk, waits for the write to complete, and then halts the processor.