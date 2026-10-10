
You should avoid logging in as root directly (especially on a graphical screen). Instead, use the *su* program, in a terminal session started as a normal user, to obtain a shell running as *root*:

```
$ /bin/su -
Password: secret                             Password for root
# _
```

After exiting the root shell (using *exit* or <kbd>Ctrl</kbd>+<kbd>d</kbd>) you end up back in the shell where you originally invoked *su*.

Some distributions try to get by without a separate root account. Ubuntu, for example, allows the first user created during the system’s installation to execute single commands with root privileges by putting *sudo* in front, as in

```
$ sudo less /var/log/syslog            Peruse system log
```

(that user can extend this privilege to other users if required). For larger tasks, it is possible to use “*sudo -i*” to obtain a shell running with administrator privileges.

> Most Linux distributions signal that a shell is running with *root* privileges by outputting a prompt ending in *“#”*. If something else appears—typically *“$”* or *“$”*—, the shell is unprivileged.

## Exercises

-   **12.1 [2]** Try *su*. Why does the example use an absolute path name to invoke the program?

-   **12.2 [2]** You need to know the *root* password for *su*. *sudo* usually asks you for your own password. Which is better?

## 12.2 System Configuration

While other systems bury their configuration details in databases that can only be modified through special tools and are susceptible to “*bit rot*” (cue *Windows* registry), system-wide configuration entries on *Linux* are usually contained in text files within the */etc* directory (a few examples can be seen in Section 10.3), where the system administrator can use a text editor of their choice to modify or extend them. For example, a new user can be added by adding the relevant parameters like the user name, numerical user ID, or home directory name to the */etc/passwd* file. A new hard disk may be configured by appending a line to */etc/fstab* specifying the name of the device file and the directory where the disk is supposed to appear.

> A *Linux* system is a complex system of software components of widely differing provenance (some of which are older than *Linux* itself). From this historically grown setup it follows that the different configuration files within */etc* are structured in a very non-uniform fashion—some are organised by lines, others contain sections delimited by braces, even others are *XML* files or even executable shell scripts. This is certainly a nuisance to administrators who need to deal with all these different formats, but it is also not straightforward to change, since all sorts of software packages would need to be modified.

> However, there are some very widespread conventions: For example, most configuration files allow comments in lines starting with *“#”*.

While the idea of managing the system configuration in separate text files may seem *antediluvian* at first, it does have some tangible advantages:

-   It is usually not possible to damage the system as a whole through mistakes in the configuration of a single software package or service. (Of course there are a few configuration files which are so essential for the system’s functionality that errors in them could, for example, render the system unbootable. But these are a small minority at best.)

-   Most configuration files allow comments. This makes it possible to document the details of individual configuration settings directly where they occur, and thus makes collaboration in a team easier or avoids accidents due to one’s own forgetfulness. It is certainly a lot better than having to remember that there is an entry X in menu Y that lets you open a dialog where on tab Z there is a box that absolutely needs to be checked because otherwise nothing is going to work. (Pieces of paper containing this type of wisdom have the unfortunate tendency of disappearing when they are needed most urgently.)

-   You can “check in” text files to a revision control system such as Git or Mercurial and thereby not just document big changes spanning various files, but also undo them in an orderly manner if required. This also makes it convenient to store the complete configuration of a computer on a central server, such that it is immediately available if the computer needs to be reinstalled for whatever reason—say, after a catastrophic hardware fault. In data centers this is a very decisive advantage, especially if a detailed “auditing” of all configuration changes is desired.

-   Text files allow the convenient configuration of whole computer networks by distributing configuration files from a central server to the computers to be managed. Systems such as “Puppet” or “Salt” make it possible to use “templates” for configuration files that are instantiated using suitable details for the target computer when they are distributed, which can totally obviate the manual configuration of individual computers (the “sneaker net”). This, too, makes the management of big networks easier but is also a definite help with smaller installations.

### Exercises

-   12.3 [3] Snoop around in /etc. Many files there have manual pages—try something like "man fstab". Are there files in /etc that you cannot read as a normal user, and why?

## 12.3 Processes

A program that is being executed is called a “process”. Besides the program code itself (in the machine language of the processor in question), a process includes working storage for the data as well as administrative information like the files currently in use, an environment (for the environment variables), a current directory, and a process number or “PID” identifying the process uniquely within the system. The operating system kernel is in charge of creating processes, assigning them CPU time and storage, and cleaning up after them when they have exited. Processes can call into the operating system kernel to access files, devices, or the network.

New processes come into being when existing processes—not unlike bacteria or other low forms of life—split up into two almost identical copies (“almost identical”, because one process is considered the “parent” and the other the “child”). In addition, a process can arrange to execute a different program: For example, if you invoke the ls command in the shell, the shell creates a child process which is at first also executing the shell’s program code. This code takes care (among other things) of arranging a possible input/output redirection and then replaces itself with the /bin/ls program file. At the end of the `ls` program, the child process ends, and the shell asks you for the next command.

The first process with the PID of 1 is created by the operating system kernel during boot. According to the convention this is a program called `/sbin/init`, and it is also called the “init process”. The init process is responsible for booting the system and, e. g., starting additional processes for system services running in the background.

### ps

You can use the “`ps`” command to obtain information about the processes running on the system. In the simplest case, `ps` shows you all processes running on your current terminal (or, nowadays, the current terminal window on your graphical screen):

```
$ ps

PID TTY   STAT TIME COMMAND
 997 pts/8 S    0:00 -bash
1005 pts/8 R    0:00 ps
$ _
```

The PID and **COMMAND** columns speak for themselves. TTY gives the name of the terminal (“pts/something” usually refers to a terminal window), **TIME** the CPU time used by the processes so far, and **STAT** the “process state”.

A process on Linux is always in one of a number of states, namely (process state)

-   **Runnable (R)** The process may be assigned CPU time.
-   **Sleeping (S)** The process is waiting for an event, typically input or output—a key press or data from disk.
-   **In deep (uninterruptible) sleep (D)** The process is waiting for an event and cannot be disturbed. Processes should not remain in this state for too long because they can only be removed by booting the system. If that happens it is usually due to some error.
-   **Temporarily stopped (T)** The process was temporarily stopped by its owner or an administrator, but can continue running later on.
-   **Zombie (Z)** The process has really finished, but its exit code has not yet been picked up by its parent. This means the process cannot “die” but remains undead within the system. Unlike in real life, zombies are not really a problem because they do not take up resources other than a slot in the process table. If your system is infested with a horde of zombies, this indicates a problem with the program that created the processes in the first place—terminating that program should make the zombies disappear.

Use parameters to control which information `ps` provides. For example, you could enter a process number to find out about a particular process:

```
$ ps 1

PID TTY   STAT TIME COMMAND
 1 ?      Ss   0:00 init [2]
```

The `l` option gives you more detailed information about a process:

```
$ ps l $$

F   UID   PID  PPID PRI  NI VSZ  RSS WCHAN  STAT TTY      TIME COMMAND
 0  1000  3542 3491  20   0  21152 2288   -    Ss   pts/8  0:00 /bin/bash
```
