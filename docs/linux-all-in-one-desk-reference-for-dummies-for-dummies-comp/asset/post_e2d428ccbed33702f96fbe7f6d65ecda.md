
In Debian, the **runlevel** command prints an output like this:

```
N 2
```

The first character of the output shows the previous run level (N means no previous run level), and the second character shows the current run level (2). In this case, the system started at run level 2. If you are in a GUI desktop in Fedora Core or MEPIS, the **runlevel** command should show **5** as the current run level.

## Examining the /etc/inittab file

The `/etc/inittab` file is the key to understanding the processes that `init` starts at various run levels. You can look at the contents of the file by using the **more** command, as follows:

```
more /etc/inittab
```

To see the contents of the `/etc/inittab` file with the **more** command, you don’t have to log in as **root**.

To interpret the contents of the `/etc/inittab` file, follow these steps:

- 1. **Look for the line that contains the phrase `initdefault`.**
   Here is that line from the `/etc/inittab` file from a Debian system:

   ```
   id:2:initdefault:
   ```

   That line shows the default run level. In this case, it’s 2.

- 2. **Find all the lines that specify what `init` runs at run level 2. Look for a line that has a 2 between the first two colons (:). Here is a relevant line in Debian:**

   ```
   l2:2:wait:/etc/init.d/rc 2
   ```

   This line specifies that `init` executes the file `/etc/init.d/rc` with **2** as an argument.

If you look at the file `/etc/init.d/rc` in a Debian system, you find it’s a shell script. You can study this file to see how it starts various processes for run levels **1** through **5**.

Each entry in the `/etc/inittab` file tells `init` what to do at one or more run levels — you simply list all run levels at which the process runs. Each `inittab` entry has four fields — separated by colons — in the following format:

```
id:runlevels:action:process
```

Table 1-8 shows what each field means.

### Table 1-8: Meaning of the Fields in Each inittab Entry

| Field | Meaning |
| :--- | :--- |
| *id* | A unique one- or two-character identifier. The *init* process uses this field internally. You can use any identifier you want, as long as you don't use the same identifier on more than one line. |
| *runlevels* | A sequence of zero or more characters, each denoting a run level. For example, if the *runlevels* field is 12345, that entry applies to each of the run levels 1 through 5. This field is ignored if the *action* field is set to *sysinit*, *boot*, or *bootwait*. |
| *action* | Tells the *init* process what to do with that entry. If this field is *initdefault*, for example, *init* interprets the *runlevels* field as the default run level. If this field is set to *wait*, *init* starts the program or script specified in the *process* field and waits until that process exits. |
| *process* | Name of the script or program that *init* starts. Of course, some settings of the *action* field require no *process* field. For example, when the *action* field is *initdefault*, there is no need for a *process* field. |

## Trying a new run level with the init command

To try a new run level, you don't have to change the default run level in the /etc/inittab file. If you log in as *root*, you can change the run level (and, consequently, the processes that run in Linux) by typing **init** followed by the run level.

For example, to put the system in single-user mode, type the following:

```
init 1
```

Thus, if you want to try run level 3 without changing the default run level in /etc/inittab file, enter the following command at the shell prompt:

```
init 3
```

The system ends all current processes and enters run level 3. By default, the *init* command waits 20 seconds before stopping all current processes and starting the new processes for run level 3.

To switch to run level 3 immediately, type the command **init -t0 3**. The number after the *-t* option indicates the number of seconds *init* waits before changing the run level.

You can also use the `telinit` command, which is simply a symbolic link (a shortcut) to `init`. If you make changes to the `/etc/inittab` file and want `init` to reload its configuration file, use the command `telinit q`.

## Understanding the Linux startup scripts

The `init` process runs a number of scripts at system startup. In the following discussions, I use a Debian system as an example, but the basic sequence is similar in other distributions — only the names and locations of the scripts may vary.

![](img/11709a8f88c8cd03868a929dc94c0e2b_413_0.png)

If you look at the `/etc/inittab` file in a Debian system, you find the following lines near the beginning of the file:

```
# Boot-time system configuration/initialization script.
si::sysinit:/etc/init.d/rcS
```

The first line is a comment line. The second line causes `init` to run the `/etc/init.d/rcS` script — the first Linux startup script that `init` runs in a Debian system. The `rcS` script performs many initialization tasks, such as mounting the file systems, setting the clock, configuring the keyboard layout, starting the network, and loading many other driver modules. The `rcS` script performs these initialization tasks by calling many other scripts and reading configuration files located in the `/etc/rcS.d` directory.

After executing the `/etc/init.d/rcS` script, the `init` process runs the `/etc/init.d/rc` script with the run level as argument. For example, for run level 2, the following line in `/etc/inittab` specifies what `init` executes:

```
l2:2:wait:/etc/init.d/rc 2
```

This example says `init` executes the command `/etc/init.d/rc 2` and waits until that command completes.

The `/etc/init.d/rc` script is somewhat complicated. Here’s how it works:

- It executes scripts in a directory corresponding to the run level. For example, for run level 2, the `/etc/init.d/rc` script runs the scripts in the `/etc/rc2.d` directory.
- In the directory that corresponds with the run level, `/etc/init.d/rc` looks for all files that begin with a `K` and executes each of them with the `stop` argument. This argument kills any currently running processes. Then it locates all files that begin with an `S` and executes each file with a `start` argument. This argument starts the processes needed for the specified run level.

To see it executed at run level 2, type the following command:

```
ls -l /etc/rc2.d
```

In the resulting listing, the K scripts — the files whose names begin with K— stop (or kill) servers, whereas the S scripts start servers. The /etc/init.d/rc script executes these files in exactly the order in which they appear in the directory listing.

## Manually starting and stopping servers

In Linux, the server startup scripts reside in the /etc/init.d directory. You can manually invoke scripts in this directory to start, stop, or restart specific processes — usually servers. For example, to stop the FTP server (the server program is called vsftpd), type the following command:

```
/etc/init.d/vsftpd stop
```

If vsftpd is already running and you want to restart it, type the following command:

```
/etc/init.d/vsftpd restart
```

You can enhance your system administration skills by familiarizing yourself with the scripts in the /etc/init.d directory. To see its listing, type the following command:

```
ls /etc/init.d
```

The script names give you some clue about which server the script can start and stop. For example, the samba script starts and stops the processes required for Samba Windows networking services. At your leisure, you may want to study some of these scripts to see what each one does. You don't have to understand all the shell programming; the comments help you discover the purpose of each script.

## Automatically starting servers at system startup

You want some servers to start automatically every time you boot the system. The exact commands to configure the servers vary from one distribution to another.

![](img/11709a8f88c8cd03868a929dc94c0e2b_414_0.png)

In Fedora Core and SUSE, use the chkconfig command to set up a server to start whenever the system boots into a specific run level. For example, if you start the SSH server, you want the sshd server to start whenever the system starts. You can make that happen by using the chkconfig command.
