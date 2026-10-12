
The output from this who command shows that the user name is `chris`. Here, `chris` is logged in on `tty1` (which is the monitor connected to the computer), and his login session began at 20:57 on January 13. The `IDLE` time shows how long the shell has been open without any command being typed (the dot indicates that it is currently active). `COMMENT` would show the name of the remote computer the user had logged in from, if that user had logged in from another computer on the network, or the name of the local `X` display if you were using a Terminal window (such as `:0.0`).

## Checking directories and permissions

Associated with each shell is a location in the Linux file system known as the *current or working directory*. As previously mentioned, each user has a directory that is identified as the user's home directory. When you first log in to Linux, you begin with your home directory as the current directory.

When you request to open or save a file, your shell uses the current directory as the point of reference. Simply give a filename when you save a file, and it will be placed in the current directory. Alternatively, you can identify a file by its relation to the current directory (relative path). Or you can ignore the current directory and identify a file by the full directory hierarchy that locates it (absolute path). The structure and use of the file system is described in detail later in this chapter.

To find out what your current directory is, type the `pwd` command:

```
$ pwd
/usr/bin
```

In this example, the current/working directory is `/usr/bin`. To find out the name of your home directory, type the `echo` command, followed by the `$HOME` variable:

```
$ echo $HOME
/home/chris
```

In the preceding example, the home directory is `/home/chris`. To get back to your home directory, you can simply type the `change directory` (`cd`) command. Although `cd`, followed by a directory name, changes the current directory to the directory that you choose, simply typing `cd` takes you to your home directory:

```
$ cd
```

At this point, list the contents of your home directory, using the `ls` command. Either you can type the full path to your home directory to list its contents, or you can use the `ls` command without a directory name to list the contents of the current directory. Using the `-a` option to `ls` enables you to view the hidden files (dot files) as well as all other files. With the `-l` option, you can see a long, detailed list of information on each file. (You can put multiple single-letter options together after a single dash, for example, `-la`.)

```
$ ls -la /home/chris
total 158
drwxrwxrwx 2 chris sales 1024 May 12 13:55 .
drwxr-xr-x 3 root root 1024 May 10 01:49 ..
-rw------- 1 chris sales 2204 May 18 21:30 .bash_history
-rw-r--r-- 1 chris sales 24 May 10 01:50 .bash_logout
-rw-r--r-- 1 chris sales 230 May 10 01:50 .bash_profile
-rw-r--r-- 1 chris sales 124 May 10 01:50 .bashrc
drw-r--r-- 1 chris sales 4096 May 10 01:50 .kde
-rw-rw-r-- 1 chris sales 149872 May 11 22:49 letter
```

Displaying a long list (`-l` option) of the contents of your home directory shows you more about file sizes and directories. Directories such as the current directory (`.`) and the directory above the current directory (`..`) are noted as directories by the letter “d” at the beginning of each entry. In this case, dot (`.`) represents `/home/chris` and two dots (`..`), which is also referred to as the parent directory, represents `/home`. The `/home` directory is owned by root. All other files are owned by the user chris (who belongs to the sales group).

The file or directory names shown on the right are mostly dot (`.`) files that are used to store GUI properties (`.kde`) or shell properties (`.bash` files). The only non-dot file shown in this example is the one named `letter`. At the beginning of each line are the permissions set for each file. (Permissions and configuring shell property files are described later in this chapter.) Other information in the listing includes the size of each file in bytes (column 4) and the date and time each file was most recently modified (column 5).

| Permissions | Links | Owner | Group | Size | Month | Day | Time | Name |
|-------------|-------|-------|-------|------|-------|-----|------|------|
| drwxrwxrwx | 2 | chris | sales | 1024 | May | 12 | 13:55 | . |
| drwxr-xr-x | 3 | root | root | 1024 | May | 10 | 01:49 | .. |
| -rw------- | 1 | chris | sales | 2204 | May | 18 | 21:30 | .bash_history |
| -rw-r--r-- | 1 | chris | sales | 24 | May | 10 | 01:50 | .bash_logout |
| -rw-r--r-- | 1 | chris | sales | 230 | May | 10 | 01:50 | .bash_profile |
| -rw-r--r-- | 1 | chris | sales | 124 | May | 10 | 01:50 | .bashrc |
| drw-r--r-- | 1 | chris | sales | 4096 | May | 10 | 01:50 | .kde |
| -rw-rw-r-- | 1 | chris | sales | 149872 | May | 11 | 22:49 | letter |

## Checking system activity

In addition to being a multiuser operating system, Linux is also a multitasking system. Multitasking means that many programs can be running at the same time. An instance of a running program is referred to as a process. Linux provides tools for listing running processes, monitoring system usage, and stopping (or killing) processes when necessary.

The most common utility for checking running processes is the `ps` command. With `ps`, you can see which programs are running, the resources they are using, and who is running them. The following is an example of the `ps` command:

```
$ ps -au
 USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
 root 2146 0.0 0.8 1908 1100 tty0 S 14:50 0:00 login -- jake
 jake 2147 0.0 0.7 1836 1020 tty0 S 14:50 0:00 -bash
 jake 2310 0.0 0.7 2592 912 tty0 R 18:22 0:00 ps -au
```

In this example, the `-a` option asks to show processes of all users that are associated with your current terminal, and the `-u` option asks that user names be shown, as well as other information such as the time the process started and memory and CPU usage. The concept of terminal comes from the old days when people worked exclusively from character terminals, so a terminal typically represented a single person at a single screen. Now you can have many "terminals" on one screen by opening multiple Terminal windows.

On this shell session, there isn't much happening. The first process shows that the user named jake logged in to the login process (which is controlled by the root user). The next process shows that jake is using a bash shell and has just run the `ps au` command. The terminal device `tty0` is being used for the login session. The STAT column represents the state of the process, with R indicating a currently running process and S representing a sleeping process.

The USER column shows the name of the user who started the process. Each process is represented by a unique ID number referred to as a process ID (PID). (You can use the PID if you ever need to kill a runaway process.) The %CPU and %MEM columns show the percentage of the processor and random access memory, respectively, that the process is consuming. VSZ (virtual set size) shows size of the image process (in kilobytes), and RSS (resident set size) shows the size of the program in memory. START shows the time the process began running, and TIME shows the cumulative system time used.

Many processes running on a computer are not associated with a terminal. A normal Red Hat Linux system has many processes running in the background. Background system processes perform such tasks as logging system activity or listening for data coming in from the network. They are often started when Red Hat Linux boots up and run continuously until it shuts down. To see and thereby monitor all the processes running on your Red Hat Linux system, type:

```
$ ps aux | less
```

I added the pipe (`|`) and the `less` command to `ps aux` to allow you to page through the many processes that will appear on your screen. Use the spacebar to page through and type `q` to end the list. A pipe lets you direct the output of one command to be the input of the next command.

| USER | PID | %CPU | %MEM | VSZ | RSS | TTY | STAT | START | TIME | COMMAND |
|------|-----|------|------|-----|-----|-----|------|-------|------|---------|
| root | 2146 | 0.0 | 0.8 | 1908 | 1100 | tty0 | S | 14:50 | 0:00 | login -- jake |
| jake | 2147 | 0.0 | 0.7 | 1836 | 1020 | tty0 | S | 14:50 | 0:00 | -bash |
| jake | 2310 | 0.0 | 0.7 | 2592 | 912 | tty0 | R | 18:22 | 0:00 | ps -au |

## Exiting the shell

To exit the shell when you are done, either type `exit` or press Ctrl+D. If you are exiting from your login shell (the shell that started when you first logged in), type `logout` to exit the shell.

I just showed a few commands designed to familiarize you quickly with your Linux system. There are hundreds of other commands that you can try that are contained in directories such as `/bin` and `/usr/bin`. There are also administrative commands in `/sbin` or `/usr/sbin` directories. Many of these commands are described in the remainder of this chapter.

## Understanding the Red Hat Linux Shell

Before icons and windows took over computer screens, you typed commands to run most computers. On UNIX systems, from which Red Hat Linux was derived, the program used to interpret and manage commands was referred to as the shell.
