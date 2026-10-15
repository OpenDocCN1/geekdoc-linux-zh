The Solaris version of the ps command supports the following options of the PC-BSD version of the command: S, a, e, r, v, w, and x. However, you invoke them without using a hyphen before them—for example, ps r. Similarly, the -o option also works under Solaris as it does under PC-BSD, but not with all the keywords listed in Table 10.3 or those displayed by the ps -L command on PC-BSD. It works with the following keywords, most of which are common with the ps version on PC-BSD: user, ruser, group, rgroup, uid, ruid, gid, rgid, pid, ppid, pgid, sid, taskid, ctid, pri, opri, pcpu, pmem, vsz, rss, osz, nice, class, time, etime, stime, zone, zoneid, f, s, c, lwp, nlwp, psr, tty, addr, wchan, fname, comm, args, projid, project, pset, and lgrp.

The output of the ps command on Solaris displays four fields, as shown, where pts/1 is pseudo terminal 1:

```
$ ps
  PID TTY      TIME CMD
 7243 pts/1    0:00 bash
 7247 pts/1    0:00 ps
$
```

The sample runs in the following session show the use of the ps command with various options. Note that the output of the ps -l command includes the obsolete fields F and ADDR, and the old-style (obsolete) PRI (known as opri in the list of keywords shown in the previous paragraph), where lower PRI value means higher priority. You can use the -y and -l options together to exclude the columns for the obsolete fields F and ADDR, include the RSS column, and display the PRI value in vogue.

```
$ ps -l
  F S   UID   PID   PPID  C PRI NI ADDR   SZ WCHAN    TTY TIME CMD
  0 O 1007  9784  9624  0  40 20    ? 2333       pts/2 0:00 ps
  0 S 1007  9624  9621  0  50 20    ? 2546       ? pts/2 0:00 bash
$ ps -ly
  S   UID   PID   PPID  C PRI NI  RSS SZ WCHAN    TTY TIME CMD
  S 1007 14081 14080 0  50 20 2284 10188 ? pts/5 0:00 bash
  O 1007 14116 14081 0  40 20 1472  9332       pts/5 0:00 ps
$ pagesize
4096
$
```

The first column, S, shows the state of the process. Process states in Solaris are briefly described in Table 10.4, along with some fields that are different from the fields displayed by the ps command on PC-BSD. Note that the ps command is in the running state and bash is waiting for an event; the event in this case is the termination of its child (i.e., the ps command running in foreground). NI shows the nice value of the process; the