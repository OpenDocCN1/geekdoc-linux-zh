The next entry in `/etc/inittab` looks like this:

```
si::bootwait:/etc/init.d/boot
```

The parameter **bootwait** indicates to carry out this command while booting and wait until it has finished.

The next few entries describe the actions for runlevels 0 to 6:

```
10:0:wait:/etc/init.d/rc 0
11:1:wait:/etc/init.d/rc 1
12:2:wait:/etc/init.d/rc 2
13:3:wait:/etc/init.d/rc 3
#14:4:wait:/etc/init.d/rc 4
15:5:wait:/etc/init.d/rc 5
16:6:wait:/etc/init.d/rc 6

1s:S:wait:/etc/init.d/rc S
---:S:respawn:/sbin/sulogin
```

The parameter **wait** means that when the system changes to the indicated level, the appropriate command is carried out and init waits until it has been completed. The parameter also means that further entries for the level are only performed after this process is completed.

The single user mode S is a special case, as it works even if the file `/etc/inittab` is missing. In such a case, enter **S** at the boot prompt when the computer starts. The command sulogin is started, which allows only the system administrator to log in. The parameter **respawn** indicates to init to wait for the end of the process and to then restart it.

`/etc/inittab` also defines the Ctrl+Alt+Del key combination for restarting:

```
ca::ctrlaltdel:/sbin/shutdown -r -t 4 now
```