| Run Level | Meaning |
|---|---|
| 0 | Shuts down the system |
| 1 | Runs in single-user stand-alone mode (no one else can log in; you work at the text console) |
| 2 | Runs in multiuser mode without network |
| 3 | Runs in full multiuser mode with network and text-mode login |
| 4 | Unused |
| 5 | Runs in full multiuser mode with graphical login (default run level) |
| 6 | Reboots the system |

The current run level, together with the contents of the `/etc/inittab` file, control which processes `init` starts in Linux. In SUSE, run level 3 is used for text-mode login screens and 5 for the graphical login screen. You can change the default run level by editing a line in the `/etc/inittab` file.

To check the current run level, type the following command in a terminal window:

```
```sh
/sbin/runlevel
```
```

This runlevel command prints an output like this:

```
```text
N 5
```
```

The first character of the output shows the previous run level (N means no previous run level), and the second character shows the current run level (5). In this case, the system started at run level 5.

# Trying a new run level with
the init command

To try a new run level, you don’t have to change the default run level in the `/etc/inittab` file. Type `su -` at a terminal window to become root, and then you can change the run level (and, consequently, the processes that run in Linux) by typing `init` followed by the run level.

For example, to put the system in single-user mode, type the following:

```
```sh
init 1
```
```