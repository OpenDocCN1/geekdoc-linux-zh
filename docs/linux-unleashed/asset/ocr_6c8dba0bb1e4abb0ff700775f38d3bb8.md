```
```
console tty6
vt100 tty0
vt100 tty1
vt100 tty2
vt100 tty3
```
```

The terminal type in the first column is used to set the `TERM` environment variable when you log in, unless you override the value.

The `/etc/inittab` file is used to set the behavior of each terminal. The format of the `/etc/inittab` file follows this pattern:

`ID:runlevel:action:process`

The `ID` is a one- or two-character string that uniquely identifies the entry. In most cases, this corresponds to the device name, such as 1 for `tty1`.

The `runlevel` decides the capabilities of the terminal with the various states that the Linux operating system can be in (run levels vary from 0 to 6, and A, B, and C). If no entry is provided, all `runlevels` are supported. Multiple `runlevels` may be mentioned in the field.

The `action` section shows how to handle the `process` field. The `action` field has several valid entries:

| boot | Runs when inittab is first read |
| bootwait | Runs when inittab is first read |
| initdefault | Sets initial run level |
| off | Terminates the process if it is running |
| once | Starts the process once |
| ondemand | Always keeps the process running (the same as respawn) |
| powerfail | Executes when init gets a power fail signal |
| powerwait | Executes when init gets a power wait signal |
| sysinit | Executes before accessing the console |
| respawn | Always keeps the process running |
| wait | Starts the process once |

The `action` indicates the behavior of the terminal device when the system starts and when a `getty` process is terminated on it.

A simple `/etc/inittab` file (taken from an earlier version of Linux for clarity's sake because the latest version complicates the lines a little) looks like this: