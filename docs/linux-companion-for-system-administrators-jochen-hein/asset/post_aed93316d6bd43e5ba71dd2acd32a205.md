
# Process tree

For each process, the kernel stores the ID of the process that generated it. This is also called the parent process. The newly started processes are child processes. By means of the `pstree` command, which does not exist under other UNIX systems, you can gain an overview of the hierarchy in the process table.

# Process management

A program that has a controlling terminal can usually be aborted with Ctrl- (the interrupt character, also see stty -a). Many processes (for example network daemons) under UNIX have no associated terminal and cannot be controlled with key combinations. It is obviously necessary to address these processes as well; this is one of the applications of the concept of signals. And how a program reacts to signals is implementation-dependent and is usually documented in the man page. The default reaction to many signals is the termination of the program.

The kill program is not only used to abort programs, but also simply to send signals. Signals can be specified either numerically or symbolically. Table 10.8 shows the most important signals; all signals can be listed by means of kill -1.

The signal 0 has a special meaning: the kernel checks that the process exists but does not send a signal. This can be used to check whether or not a task is running. The example in Listing 10.67 checks if a process setiatome is running, and starts it if it is not running.

```
$ crontab -l | killall 0 setiatome | setiatome
```

**Listing 10.67** Using killall to ensure a program is running.

| Signal | Number | Meaning |
| --- | --- | --- |
| SIGHUP | 1 | Hang-up, re-read configuration |
| SIGKILL | 9 | Unconditional program termination |
| SIGUSR1 | 10 | User-defined signal |
| SIGUSR2 | 12 | User-defined signal |
| SIGTERM | 15 | Normal program termination |

**Table 10.8** The most important signals.

It is often necessary to send a daemon a hang-up signal (SIGHUP); this causes many daemons to re-read their configuration file. You can find out the daemon's process number using ps. This process number must then be the signal with kill -HUP PID. Many daemons store their process ID in a file which can also be used directly to send the signal, for example with the command kill -HUP 'cat /var/run/syslog.pid'. The command killall, which is peculiar to LINUX, allows you to send a signal even if you only know the program name, for example killall -HUP syslogd.

In the shell and shell programs, you can process signals by using the trap command. This may be necessary if you want to prevent a user interrupting a shell script as the login scripts. The example in Listing 10.68 shows the interactive use of trap.

```
(Linux):$ trap echo sighup received SIGHUP
(Linux):$ kill -HUP $$
sighup received
```

- **10.68** Processing signals by means of the shell.

## 9.0.2 Jobs and job control

Under UNIX systems which have job control, many shells provide various functions for handling jobs more smoothly. Under UNIX, a job is a process that is started in the background. Job control is the name for the set of functions with which the jobs are controlled and managed. These terms have nothing to do with the 'Job Control Language' known from mainframe computers.

Programs can be sent to the background by means of an ampersand (&). Output, however, is displayed on the terminal from which the job was started. If the program expects an input, the program is halted, and depending on the shell and the configuration, the system displays an appropriate message.

The program can be pulled back into the foreground with it later in the background. If you have started several jobs, you can interrupt the program with Ctrl-Z (also see stty -a, suspend character), then you can shift it into the background with bg.

you will obtain a list with jobs, also see help jobs in the (bash), you can select a job by means of %jobnumber. The character sequence % stands for the job started. These character sequences can also be used in process management by means of kill.

If you want to run larger programs which require much time and memory in the background, you can assign them a lower priority by means of nice. Thus, other users' interactive work is considerably less affected.

The higher the nice value, the 'nicer' you are to other users. The user root is the only user who can also set a negative nice value. These processes are then privileged in the scheduling. If you forgot the call with nice, you can still change the priority at a later time by means of the program renice or top (but only the system administrator is allowed to increase the priority).

When a user of the bash logs out, background processes are sent the SIGHUP signal. Usually, this leads to termination of the program, which is not desired. In such cases, the program must be started with nohup. This is always the case in the shell. If you forget the nohup, there is unfortunately no other solution to restart the program.

Examples of programs that run for a long time and are often started in the background are ftp transfers of large amounts of data, simulation programs or other CPU-intensive programs, and X clients. In all cases, you have the advantage of being able to log out and have the process continue, or at least you can continue using the shell.

## Tools (not only) for programmers

Current LINUX distributions include a whole series of programs and packages from which the user can choose. Therefore it does not appear to make much sense compiling these or other programs oneself. But not all programs are readily available as binary versions, and in case of error corrections, changes are often available only to the source code. This chapter explains what the user can do concerning installation and development of programs. These possibilities are not only of interest to programmers, but also to users who have to carry out frequently recurring tasks.

A number of programming languages are available for LINUX. The most widely used one is C, because the kernel and most utilities are mostly written in this language. Under UNIX, the installation of a C compiler is practically a must, since this is the only way to create a kernel properly adapted to individual hardware. Furthermore, most freely available UNIX programs are implemented in C.

Many other programming languages are available too: C++, Objective C, Pascal (GNU Pascal or Pascal-to-C), FORTRAN (GNU FORTRAN or FORTRAN-to-C), Lisp, and script languages such as Perl, Tcl, and Python. Programs are often implemented in one of these languages, so the corresponding interpreter or compiler must be installed if these programs are to be used. This is one of the reasons why the GNU project programs have usually been implemented in the C language.

## 11.1 The make program

The program is primarily used for compilation of large programs that consist of many individual modules. When changes are made to the source code, only the modified program parts are recompiled. Compared to a complete compilation, this saves a lot of time; therefore, the sources of nearly all programs are supplied with a Makefile which controls compilation.

GNU make uses one of the following files as control file for the compilation process, provided the file exists: Makefile, or Makefile.Other. Other files can be specified by means of the option -f. If you use special functions of GNU make in your Makefile, you should name this file GNUMakefile.

At the call of make, the default target specified in the Makefile is created. If an additional parameter is specified, that target is created. Let us look at a simple example to explain this (Listing 11.1).

```
# A simple Makefile for prune
all: prune

prune: prune.c
	gcc -s prune.c -o prune

install: prune
	install -m 755 prune /usr/local/sbin/prune
	echo edit /etc/prune.conf to suit your system
```

Listing 11.1 A simple Makefile.

The make command creates the default target all. The default target is the first target in the Makefile. Targets are always written in the first column and terminated with a colon: there is a dependency on the file or target prune. Dependencies are written to the right of the column. Comments in Makefile begin with a hash sign (#) and end with the end of the line.

In the target prune which depends on the file prune, the C compiler is called if the file prune is more recent than the file prune. For this simple function, make already has a so called default rule that would be applied if no command was specified at this point. Commands are entered after a tab. If spaces are used instead of the tabs, it is possible some make versions show an error message.

The make install command executes the commands specified in the target install. First, however, it checks whether the program prune must be newly created. The install command copies the program to the location in the
