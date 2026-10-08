# Job Control

| Flag | Meaning |
| --- | --- |
| -l | Gives the long listing format for each line. |
| -t xx | Lists processes associated with the specified ttyxx. |
| -u | Produces user-oriented output. |
| -w | Uses wide output format. If repeated (-ww), it will show much of each command as possible. |
| -x | Shows all processes in the system. |

The -a, -g, and -x flags affect how much information is displayed by ps. To use either the -g or -x command, you must also use the -a command. On most machines, -ax yields considerably more than -ag. The most commonly used flags (and combinations) are -u, to have only your processes in a friendly format; -aux, to see everything on the machine (you almost always want to pipe this to grep or more, to be overrun with hundreds of lines of information); and -wxx, to show all the processes associated with ttyxx.

![](bbox=[0.875, 0.363, 1.0, 0.433])

> The ps program varies from System V to Berkeley UNIX more than any other command. Unfortunately, the two or three most common flags are similar across the two systems. To explore more about the ps command on your system, you should start by reading the man page.

![](bbox=[0.117, 0.483, 0.223, 0.545])

# ACTION

+   1. To begin, I'm going to start vi in the background:

```
% vi dickens.note &
[1] 4352
%
```

I'll start that awk job again, too:

```
% tawk
awk -F: '{print $1 = "$5"} < /etc/passwd | awk -F, '{print $1}'
|! awk "{if (NF = 2) print $0}' | sort > ! who.is.who &
[2] 4532 4534 4537
%
```

The jobs command will show what processes it has running:

```
% jobs
[1] + Stopped (tty output) vi dickens.note
[2] - Running awk -F: '{print $1 = "$5"} < /etc/passwd | awk -
F., | awk '{ if (NF > 2) print $0 } | sort > ! who.is.who
%
```

* With*