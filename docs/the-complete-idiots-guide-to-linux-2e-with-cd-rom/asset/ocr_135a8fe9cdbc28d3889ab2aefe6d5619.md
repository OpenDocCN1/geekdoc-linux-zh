```
root        22  0.0  0.0    0    0 ?  SW   09:46   0:00 (nfsi od)
root        57  0.0  0.6  804  260 ?  S    09:47   0:00 update
          (bdflush)
root       106  0.0  0.8  824  328 ?  S    09:47   0:00 inetd
root       188  0.0  1.5 1108  604 ?  S    11:51   0:00 httpd -f
/etc/httpd/a
```

# Killing a Process: kill

You are able to terminate processes using the kill command. The kill command should be used as a last resort for terminating a program that is not working correctly. The kill command sends a signal (there are many kinds of signals; kill is just one of them) to the program, which should cause it to react appropriately. Otherwise, it will get killed:

```
kill pid
```

Assuming that I wanted to kill my Web server (the httpd process listed previously), I would issue this command:

```
[root@digital /]# kill 188
```

If you are not the owner of the process (see the owner on the first column on the ps output), you would need to be root to kill it.

Sometimes, a rogue program will not respond properly to the default kill signal. At times like this, it is sometimes necessary to use a stronger kill, the KILL (unconditional kill) signal, also known as "signal 9" in Linux. Signal 9 is very strong medicine and should only be used when a rogue program refuses to die in any other way. To kill a program with the KILL signal in Linux, use either of the following:

```
kill -KILL pid
kill -9 pid
```

Replace pid with the number of the process you wish to terminate. No process can ignore or escape the KILL signal.

Some processes that run as daemon, such as httpd, can be restarted by sending them a -HUP (hangup) signal. The restart will make the process reread its configuration files and restart, as in the following:

```
[root@digital /]# kill -HUP 188
```

# "Nicing" a process: nice and renice

Sometimes you'll have a big job to run—say you need to process a few hundred megs of log files for some statistical information about your Web server, perhaps. Although you might want the information fast, having the computer go all out to get it for you will adversely affect the performance of everything else in your system. It could also be that you need that job run as quickly as possible, giving everything else second priority.

To start such a process with a lower priority, just type nice before the name of the command. This will launch the command in a nice state:

```
nice dobigjob
```

With nice, it is possible to set the priority a process executes. Priorities range from 19 (the nicest program) to -20 (the highest priority). Only root can assign a high (negative) priority to a process.

Nice is set up to add 10 to the current priority of any process that by default is zero.

You can also specify a priority by providing the -n flag and a priority setting followed by the PID: