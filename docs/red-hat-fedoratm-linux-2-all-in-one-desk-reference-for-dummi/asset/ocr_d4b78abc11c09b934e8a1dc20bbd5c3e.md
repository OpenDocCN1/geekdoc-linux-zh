To switch to run level 5 immediately, type the command `init 40 5`. The number after the `-t` option indicates the number of seconds `init` waits before changing the run level.

You can also use the `telinit` command, which is simply a symbolic link (a shortcut) to `init`. If you make changes to the `/etc/inittab` file and want `init` to reload its configuration file, use the command `telinit q`.

# ## Understanding the Fedora Core startup scripts

The `init` process runs a number of scripts at system startup. If you look at the `/etc/inittab` file, you find the following line near the beginning of the file:

```
```text
# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit
```
```

The first one is a comment line. The second line causes `init` to run the `/etc/rc.d/rc.sysinit` script — the first Fedora Core startup script that `init` runs. The `rc.sysinit` script performs many initialization tasks, such as mounting the file systems, setting the clock, configuring the keyboard layout, starting the network, and loading many other driver modules. The `rc.sysinit` script performs these initialization tasks by calling many other scripts and reading configuration files located in the `/etc/sysconfig` directory.

After executing the `/etc/rc.d/rc.sysinit` script, the `init` process runs the `/etc/rc.d/rc` script with the run level as argument. For example, for run level 5, the following line in `/etc/inittab` specifies what `init` executes:

```
```text
15:5:wait:/etc/rc.d/rc 5
```
```

This example says `init` executes the command `/etc/rc.d/rc 5` and waits until that command completes.

The `/etc/rc.d/rc` script is somewhat complicated. Here’s how it works:

+   - It changes to the directory corresponding to the run level. For example, to change to run level 5, the script changes to the `/etc/rc.d/rc5.d` directory.
+   - In the directory that corresponds with the run level, `/etc/rc.d/rc` looks for all files that begin with a `K` and executes each of them with the `stop` argument. This argument kills any currently running processes. Then it locates all files that begin with an `S` and executes each file with a `start` argument. This argument starts the processes needed for the specified run level.