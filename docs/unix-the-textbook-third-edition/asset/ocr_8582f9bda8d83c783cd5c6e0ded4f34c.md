```
root      1  0.0  0.0  9432   756 - SLs   Fri10PM 0:00.08 /sbin/init--
root      2  0.0  0.0    0    16 - DL    Fri10PM 0:00.00 [crypto]
root      3  0.0  0.0    0    16 - DL    Fri10PM 0:00.00 [crypto
returns]
[bob@pcbsd-4976] ~$
```

A similar output can be obtained in Solaris by giving the following command:

```
%ps -ef | head -10
```

The pgrep command displays the PIDs of running processes. Here are some examples of how to use pgrep to find the process IDs of the running processes and pipe those PIDs to another command to produce the output.

Search for kdeinit and run ps (assumes you are running the KDE4 desktop environment).

```
$ ps -p 'pgrep kdeinit'
PID   TT   STAT   TIME   COMMAND
17189 -   Is    00:00.96 kdeinit4: kdeinit4 Running...
(kdeinit4)
... [Output truncated]
$
```

Search for okular and run ps

```
$ ps -fp 'pgrep okular'
PID   TT STAT   TIME   COMMAND
46917 -  I    0:27:14 okular /usr/local/share/pcbsd/
doc/handbook_en.pdf
$
```

Search for okular, improve its priority (assumes Okular, the PDF viewer, is running and you are the superuser).

```
$ renice -1 'pgrep okular'
46917: old priority 0, new priority -1
$
```

The nice and renice commands, as seen in the previous example, change process priorities in the CPU.

Here is an example of using a command with nice to change a command's nice value.

Launch FileZilla at higher priority:

```
$ nice -n -1 filezilla
$
```