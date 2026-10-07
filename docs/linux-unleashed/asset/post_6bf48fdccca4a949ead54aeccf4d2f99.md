
you and I remember things. We know that there is always a piece of information called “day of the week” (the environment variable); however, we change the data in this variable, from Monday to Tuesday to Wednesday, and so on, as days go by.

To see the list of *exported* environment variables, type `env`. A typical output from the **env** command looks like this:

```bash
$ env
FMHOME=frame
HOME=/usr/tparker
HUSHLOGIN=FALSE
HZ=100
LOGNAME=tparker
MAIL=/usr/spool/mail/tparker
PATH=:/frame/bin:/bin:/usr/bin:/usr/tparker/bin:.
SHELL=/bin/sh
TERM=ansi
TZ=EST5EDT
```

The environment variable's name is on the left and the value held by the variable is on the right. The word “exported” is used here to mean something special: when an environment variable is exported, it is available to every program and utility on the system that you start. It stays available until you log off. You can define variables that are effective only for a single program or that don't have the same effect as exported variables.

The most important variable to note is the **PATH**, the value of which is your *search path*. As we will see in the next chapter, when you type a command, Linux searches every place listed in your search path for that command.

A longer list of environment variables, consisting of several new variables in addition to the ones shown earlier, is displayed by the command **set**. Here's the output from the set command on the same system as the preceding one:

```bash
$ set
FMHOME=frame
HOME=/usr/tparker
HUSHLOGIN=FALSE
HZ=100
IFS=
 
LOGNAME=tparker
MAIL=/usr/spool/mail/tparker
MAILCHECK=600
OPTIND=1
PATH=:/frame/bin:/bin:/usr/bin:/usr/tparker/bin:.
PS1=$
PS2=>
SHELL=/bin/sh
TERM=ansi
TZ=EST5EDT
```

![](img/e8e6b47ac20475e23d48b4c476f5d891_176_0.png)

The new variables that appear on the list are local: They have not been marked for export. For more information on exporting variables, see Chapter 10. You can think of local variables as items of information needed for only a certain time or location. For instance, remembering the variable “what-floor-am-I-on” becomes an unnecessary piece of information after you leave the building! You may see the same output for both the set and env commands in some cases, but they actually do report slightly different things.

## Processes and How to Terminate Them

In the previous chapter, we learned about the who command, which shows you the login names of everyone who is logged into the system. The who program actually gets its information from the Linux system, which maintains and updates the list of the system’s current users.

In fact, Linux keeps much more detailed records about what is happening on the system than just who is logged in. Because Linux is a multitasking system in which many programs or program threads may be running simultaneously, Linux keeps track of individual tasks or processes. Every time you enter a command, that’s a process. Whenever the system does anything, that, too, is a process. Essentially, everything that Linux does is called a process, and there can be dozens of processes running at the same time.

## The Process Status Command: ps

To find out what processes are running, we use the ps command. “ps” stands for “process status,” not the “post script” you might write at the end of a letter. Remember that ps, like all Linux commands, is lowercase.

Typing ps by itself gives you a concise listing of your own processes. When you don’t specify any options to ps, that’s the default behavior, listing your own processes:

```bash
darkstar:~$ ps
  PID TTY STAT TIME COMMAND
   41 v01 S  0:00 -bash
  134 v01 R  0:00 ps
```

The information in the first column, headed PID, is important. This is the Process ID number, a unique number assigned to each process and which Linux uses to identify that particular process. You must know a process's PID to be able to kill it. Every process on the system has a PID, and the numbers range from 0 to 65,535 then restart from the beginning, making sure each number is used only once at any one time. Linux uses numbers instead of names for each process because it's faster and easier that way.

The **TTY** column shows you which terminal the process was started from. You will see your own terminal listed when you try the **ps** command.

The **STAT** column gives the status of the process. The two most common entries in the status column are **S for sleeping** and **R for running**. A sleeping process is one that isn't currently active. However, don't be misled. A sleeping process might just be taking a very brief catnap! In fact, a process can switch between sleeping and running many times every second.

The **TIME** column shows the amount of system time used by the process. Clearly, neither of our processes is taking up any appreciable system time! That's often the case with modern machines, as most processes execute so quickly that the time column scarcely moves above a single digit.

Finally, the **NAME** column contains the name of the program you're running. This is usually the command you type at the command line. However, sometimes the command you enter starts one or more processes, called children, and in this case, you'll see these additional processes show up as well, without ever having typed them yourself. Your **login** shell will have a - before it, as in **-bash** in the previous example. This helps to distinguish this *primary* shell from any other shells you may enter from it. These will not have the - in front.

### Note

If you are logged in as *root*, you see a list of *all* processes on the system. This is because the *root* username, being the superuser, owns everything that happens on the Linux system.

If you are an "ordinary" user, but have also logged in on another terminal (including another virtual terminal you have selected by pressing Alt+Fn as discussed in Chapter 6, "Getting Started"), you see the processes you are running on the other terminal (or terminals), as well.

Don't be worried if you see slightly different columns of information when you use *ps*. The output tends to vary a little bit, especially with options in use, with different versions of Linux. The basic information is much the same, though.

One useful option with **ps** is **u**. Although it stands for “user,” it actually adds quite a few more columns of information in addition to just the username:

```bash
darkstar:~$ ps -u
USER PID %CPU %MEM SIZE RSS TTY STAT START TIME COMMAND
fido 41 0.1 6.8 364 472 v01 S 23:19 0:01 -bash
fido 138 0.0 3.3 72 228 v01 R 23:34 0:00 ps -u
```

In addition to the username in the **USER** column, other interesting new items include **%CPU** which displays the percentage of your computer’s processing power that is being used by the process, and **%MEM** which displays the percentage of your computer’s memory that is being used by the process.

If you want to see all processes running on the system and not just the processes started by your own username, you can use the **a** command option. (The **root** login sees everyone’s processes automatically and does not have to use **a**, so **root** can get the following output by simply typing **ps**.)

```bash
darkstar:~$ ps -a
PID TTY STAT TIME COMMAND
62 v03 S 0:00 /sbin/agetty 38400 tty3
63 v04 S 0:00 /sbin/agetty 38400 tty4
64 v05 S 0:00 /sbin/agetty 38400 tty5
65 v06 S 0:00 /sbin/agetty 38400 tty6
330 v02 S 0:00 -bash
217 v01 S 0:00 -bash
217 v01 S 0:00 ps -a
```

As you can see, quite a few “other” processes are happening on the system! In fact, most of the processes we see here are running whether or not anyone is actually logged into the Linux system. All the processes listed as running on **tty** are actually system processes and are started every time you boot up the Linux system. Processes of the form /sbin/agetty 38400 tty6 are login processes running on a particular terminal waiting for your login.

It can be useful to combine the **a** and **u** options (if you’re not **root**).

```bash
darkstar:~$ ps -au
USER PID %CPU %MEM SIZE RSS TTY STAT START TIME COMMAND
root 72 0.0 3.6 390 532 v01 S 17:55 0:01 -bash
root 74 0.0 1.5 41 224 v03 S 17:55 0:00 /sbin/agetty 38400 tty3
root 75 0.0 1.5 41 224 v04 S 17:55 0:00 /sbin/agetty 38400 tty4
root 76 0.0 1.5 41 224 v05 S 17:55 0:00 /sbin/agetty 38400 tty5
root 77 0.0 1.5 41 224 v06 S 17:55 0:00 /sbin/agetty 38400 tty6
```
