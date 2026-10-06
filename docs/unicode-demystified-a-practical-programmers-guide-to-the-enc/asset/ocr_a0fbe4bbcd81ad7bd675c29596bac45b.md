# System Operation 961

The action is one of the following keywords: respawn, wait, once, boot-wait, demand, powerfail, powerwait, powerokwait, powerfailnow, crtlalld, kbrequest, off, offend, initdefault, or sysinit. This keyword controls how the process is executed when it is executed. The most commonly used keywords are wait and respawn.

The wait keyword instructs to start process and wait for it to terminate. All subsequent scans of inittab ignore this wait. Because a wait entry is started only once (on runlevel) and not executed again while the system remains at runlevel, it is often used to redirect output to the console.

The respawn entry tells it to start process if it does not exist but not to wait for it to terminate. If process does exist, it goes on to the next entry in the inittab. The utility continues to rescan inittab, looking for processes that have died. When a process dies, a respawn entry causes it to restart it.

The initdefault entry tells what runlevel the system goes to (see Table 17-7 on page 943). Without this information, it prompts for a runlevel on the system console. The value of the initdefault entry is set when you configure the system or when you edit inittab directly.²³

Each virtual console (page 36) has in inittab a mingety entry that includes a unique identifier (such as tty1, which is short for /dev/tty1). Add or remove mingety lines to add or remove virtual consoles. Remember to leave a virtual console for each X window that you want to run. Following is the mingety entry for /dev/tty2:

```
2:2345:respawn:/sbin/mingety tty2
```

The id on a mingety line corresponds to the tty number.

All the actions are documented in the inittab man page. For more information, refer to “Booting the System” on page 943.

/etc/motd Contains the message of the day, which is displayed each time someone logs in. The file typically contains site policy and legal information. The file should be kept short because users tend to see the message many times.

/etc/mtab When you mount without any arguments, it consults this file and displays a list of mounted devices. Each time (on an rc script) call mount or unmount, these utilities make the necessary changes to mtab. Although this is an ASCII text file, you should not edit it. See also /etc/fstab.

> ²³ Be careful when you edit inittab by hand. Always make a backup copy in the same directory before you edit the file. If you make a mistake, you may not be able to boot the system. If this happens, refer to “Emergency Mode” on page 948.