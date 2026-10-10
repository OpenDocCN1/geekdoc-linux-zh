What the init process starts depends on the following:

+   - The run level, an identifier that identifies a system configuration in which only a selected group of processes can exist.

+   - The contents of the /etc/initab file, a text file that specifies which processes to start at different run levels.

+   - A number of shell scripts that are executed at specific run levels. (The scripts are located in the /etc/init.d directory and a number of subdirectories in /etc — these subdirectories have names that begin with rc.)

![](bbox=[0.11, 0.33, 0.19, 0.41])

Most Linux distributions use seven run levels — 0 through 6. The meaning of the run levels differs from one distribution to another. Table I-7 shows the meanings of the run levels and points out some of the actions specific to Fedora Core, Debian, MEPIS, SUSE, Ubuntu, and Xandros.

| Table I-7 Run Levels in Linux |
| Run Level | Meaning |
|---|---|
| 0 | Shuts down the system |
| 1 | Runs in single-user standalone mode (no one else can log in; you work at the text console) |
| 2 | Runs in multiuser mode (Debian, Ubuntu, and Xandros use run level 2 as the default run level) |
| 3 | Runs in full multiuser mode (used for text mode login in Fedora Core, MEPIS, and SUSE) |
| 4 | Runs in full multiuser mode (unused in Fedora Core, MEPIS, and SUSE) |
| 5 | Runs in full multiuser mode (used as the default run level with graphical login in Fedora Core, MEPIS, and SUSE) |
| 6 | Reboots the system |

![](bbox=[0.11, 0.71, 0.19, 0.79])

The current run level together with the contents of the /etc/inittab file control which processes init starts in Linux. The default run level is 2 in Debian, Ubuntu, and Xandros. In Fedora Core, MEPIS, and SUSE, run level 3 is used for text mode login screens and 5 for the graphical login screen. You can change the default run level by editing a line in the /etc/inittab file.

To check the current run level, type the following command in a terminal window:

```
```bash
/sbin/runlevel
```
```