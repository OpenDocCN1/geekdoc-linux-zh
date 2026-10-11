```
# fuser -u /dev/*

/dev/XOR:
	98(root)	100(root)	102(root)	109(root)

/dev/console:
	60(root)	120(root)

/dev/fd:
	552(root)

/dev/gpmdata:
	120(root)

/dev/log:
	93(root)

/dev/mouse:
	120(root)

/dev/null:
	98(root)	100(root)	102(root)	109(root)

/dev/printer:
	102(root)

/dev/psaux:
	120(root)

/dev/stderr:
	524(root)	552(root)

/dev/stdin:
	121(bob)	507(root)	524(root)	552(root)

/dev/stdout:
	524(root)	552(root)

/dev/systty:
	60(root)	120(root)

/dev/tty0:
	60(root)	120(root)

/dev/tty1:
	121(bob)	507(root)	524(root)	552(root)

/dev/tty2:
	122(root)

/dev/tty3:
	123(root)

/dev/tty4:
	124(root)

/dev/tty5:
	125(root)

/dev/tty6:
	126(root)
```

# MANIPULATING PROCESSES

Processes can be manipulated by certain commands. The kill command can do everything from restart a process to completely destroying it. To see a list of commands to send a process, type kill -l (lowercase L). To restart a process, you can use kill -1 [pid] and to completely destroy a process, you can use kill -9 [pid].

```
$ kill -l

1) SIGHUP... 2) SIGINT... 3) SIGQUIT.. 4) SIGILL
5) SIGTRAP... 6) SIGIOT... 7) SIGBUS... 8) SIGFPE
9) SIGKILL... 10) SIGUSR1..11) SIGSEGV.. 12) SIGUSR2
13) SIGPIPE... 14) SIGALRM...15) SIGTERM.. 16) SIGCHLD
18) SIGCONT.. 19) SIGSTOP..20) SIGSTP... 21) SIGTTIN
22) SIGTTOU... 23) SIGURG... 24) SIGXCPU... 25) SIGXFSZ
26) SIGVTALRM..27) SIGPROF..28) SIGWINCH..29) SIGIO
30) SIGPWR...
```

As root, you can change the priority of a process by using nice. You can change the priority to -20 for the highest priority and 19 for the lowest. If you're running critical backups and a user is checking e-mail, you may want to readjust their process to being a lower priority or adjust your process to a higher priority.

```
# nice --adjust=ADJUSTMENT [Command]
```