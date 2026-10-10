
# Informational Commands

These commands display information about your system or its users.

## The Name of the Computer

The `hostname` command displays the name of the computer. The following are examples run on my machine, shishi.skoll.ca:

```
$ hostname
shishi.skoll.ca
$ hostname -a # (Aliases)
shishi
$ hostname -f # (Full name)
shishi.skoll.ca
$ hostname -i # (IP address)
192.168.2.3
$ hostname -s # (Short name)
shishi
$ hostname -d # (Domain Name)
skoll.ca
$ hostname newname # (set name - root only)
```

`hostname` has a few more options; see `hostname(1)` for details.

`uname` displays information about your computer. The following shows `uname` in action:

```
$ uname # (Operating system name)
Linux
$ uname -m # (Machine type)
i686
$ uname -n # (Node name)
shishi.skoll.ca
$ uname -r # (Operating system release)
2.2.5
$ uname -s # (Operating system name)
Linux
$ uname -p # (Host processor type)
unknown
$ uname -v # (Operating system version)
#1 Sat Apr 3 21:49:22 MST 1999
$ uname -a # (Everything)
Linux shishi.skoll.ca 2.2.5 #1 Sat Apr 3 21:49:22 MST 1999 i686 unknown
```

## Who Am I?

A number of commands tell you who you are.

```
$ logname # (What's my login name?)
dfs
$ id # (What are my user and group ID's?)
uid=500(dfs) gid=500(dfs) groups=500(dfs),17(postgres)
$ whoami # (What's my effective user-ID?)
dfs
$ who am i # (Who am I?)
shishi.skoll.ca dfs tty0 Jun 28 09:09 (:0.0)
```

Note the last example, `who am i`. It displays who you are as shown in the following table:

| machine | user | terminal | login_time | login_location |
| :--- | :--- | :--- | :--- | :--- |
| shishi.skoll.ca | dfs | tty0 | Jun 28 09:09 | (:0.0) |

## How Long Since the Last Reboot?

The command `uptime` gives information about the system up time:

```
$ uptime
3:31pm up 6:23, 2 users, load average: 0.11, 0.20, 0.13
```

The `uptime` command tells you that the current time is 3:31 p.m. and the computer was last rebooted 6 hours and 23 minutes ago. There are two users. The system load averages for the past 1, 5, and 15 minutes were 0.11, 0.20, and 0.13, respectively. (The load average is the average number of runnable processes at any given instant.)

## Who Is Logged On?

The following command tells you who is logged on:

```
$ w # (Who is logged on and what are they doing?)

3:32pm up 6:24, 2 users, load average: 0.11, 0.20, 0.13
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
dfs ttyD :0.0 9:09am 0.00s 7:49 0.00s w
dfs tty3 shevy 3:36pm 5.00s 0.04s 0.00s -bash
```

The first line of output is the same as for `uptime`. The next line is a header. For each person logged in on a terminal, a line of output is produced. The line contains the following fields:

- **USER** The name of the user.
- **TTY** The terminal device the user is logged on to.
- **FROM** The remote system the user is logged on from. In the first line, this is shown as `:0.0` because the terminal is an xterm in the display `:0.0`. The second line shows that `dfs` is remotely logged in from the machine `shevy`.
- **LOGIN@** The time of login.
- **IDLE** How long the user has been idle.
- **JCPU** The cumulative CPU time of all jobs on the user's terminal.
- **PCPU** The CPU time of the currently running job.
- **WHAT** The foreground job (currently running job) on the user’s terminal.

`who` gives somewhat less information:

```
$ who # (Who is logged on?)
dfs    :0    Jun 28 09:09
dfs    tty p3    Jun 28 15:36 (shevy.skoll.ca)
```

Here, the fields are USER, TTY, LOGIN@, and FROM (if not from the local machine).

The command `last` shows the last time someone logged on. Its syntax is

```
$ last [-n] [user]
```

For example, `last dfs` shows the login history for user `dfs`. The following example shows the last four logins for `dfs`:

```
$ last -4 dfs
dfs tty p3 shevy Mon Jun 28 15:36 still logged in
dfs :0          Mon Jun 28 09:09 still logged in
dfs :0          Sun Jun 27 12:23 - 22:43 (10:19)
dfs :0          Sun Jun 27 11:22 - 12:05 (00:43)
```

The fields are USER, TTY, FROM (if not the local machine), login time, logout time, and total time spent logged in.

`last` has several options; consult `last(1)` for details.

## Free Memory

The `free` command displays statistics about memory usage:

```
$ free

          total     used free shared buffers cached
Mem:      128220   100163 28052 59756 4624 55472
-/+ buffers/cache: 40072 88148
Swap:     377516    388 377128
```

The total column shows the total amount of available memory in kilobytes. This computer has 128MB of physical memory and about 368MB of swap space.

The used column shows how much memory is used, and the free column shows how much is free. shared shows how much memory is shared by more than one process. buffers and cached show how much memory is used by file system buffers and caches. Linux caches disk files in memory, but this memory can be claimed by running processes—they take priority. The line `-/+ buffers/cache` shows how much memory is really available for processes. The memory used by the disk cache is subtracted from the used memory.

`free` is Linux-specific; it is not found on other UNIXes. For more details, see the man page `free(1)`.

You can also look at memory statistics by typing `cat /proc/meminfo`. This produces a similar output to `free`, but gives memory statistics to the byte level.

# Disk Space

Linux has two commands for determining the amount of free disk space and the amount of disk space used by files and directories.

## Free Space

The `df` command tells how much disk space you have:

```
$ df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 1554202 73090 1400049 5% /
/dev/hda2 3106103 1131281 1814172 38% /usr
/dev/hda3 4655757 220433 4194349 5% /home
```

The fields have the following meanings:

- **Filesystem** The block special file corresponding to the file system.
- **1k-blocks** The total number of 1KB blocks on the file system.
- **Used** The number of used blocks.
- **Available** The number of available blocks. Note that Used and Available add up to less than 1k-blocks because some blocks are reserved for use by root only.
- **Use%** The percentage of available blocks that are used.
- **Mounted on** The mount point of the file system.

`df` has a number of options; consult `df(1)` for details. My favorite is the `-h` option, which results in human-readable output:

```
$ df -h
Filesystem Size Used Avail Use% Mounted on
/dev/hda1 1.5G 71M 1.3G 5% /
/dev/hda2 3.0G 1.1G 1.7G 38% /usr
/dev/hda3 4.4G 215M 4.0G 5% /home
```

![](img/df365d352a104b50fea29e59a052de4d_994_0.png)

## Used Space

The `du` command computes how much disk space is used by files and directories.

`du` is invoked as shown in the following:

```bash
$ du [options] [pathname,...]
```

For each `pathname`, `du` computes the disk space used by the file or directory. If no `pathname`s are supplied, the current directory is assumed.

`du` recurses into directories given as arguments and displays the space used by all sub-trees as well as the directory given as an argument. For example,

```bash
$ du DFClass
```

```
4	DFClass/.CVS
4	DFClass/src/.CVS
182	DFClass/src
4	DFClass/tests/.CVS
346	DFClass/tests
3	DFClass/include/.CVS
4	DFClass/include/df/.CVS
33	DFClass/include/df
37	DFClass/include
614	DFClass
```

The disk usage for each subtree is shown. On the last line, you see that the total disk space used by the `DFClass` directory and all of its descendants is 614KB.

`du` has a number of options:

- `-s` Summarize disk space. `du` prints disk space only for items explicitly named on the command line. For example,

```bash
$ du -s DFClass B1ge
```

```
614	DFClass
3855	B1ge
```

Details are not shown. The `-s` switch is useful for finding out who is hogging the disk:

```bash
# du -s /home/j/* > /DISKNOGS
```

- `-a` Show all details, even for ordinary files. This produces large amounts of output.

- `-x` Only count space on the same file system as the argument given. This prevents `du` from recursing into a different file system.
