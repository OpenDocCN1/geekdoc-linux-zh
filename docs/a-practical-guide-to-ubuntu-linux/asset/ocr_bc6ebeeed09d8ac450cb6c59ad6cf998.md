# PROCESSES 329

(PID 22789). The parent PID number of sleep is the same as the PID number of the shell (21341).

```
$ sleep 10 &
[1] 22789
$ ps -f
UID PID PPID CIME TTY TIME CMD
max 21341 21340 0 10:42 pts/16 00:00:00 bash
max 22789 21341 0 17:30 pts/16 00:00:00 sleep 10
max 22790 21341 0 17:30 pts/16 00:00:00 -f
```

Refer to the ps page for more information on ps and the columns it displays with the -f option. A pair of sleep and ps -f commands shows that the shell is still running by the same process that it for another process to sleep:

```
$ sleep 10 &
[1] 22791
$ ps -f
UID PID PPID CIME TTY TIME CMD
max 21341 21340 0 10:42 pts/16 00:00:00 bash
max 22791 21341 0 17:31 pts/16 00:00:00 sleep 10
max 22792 21341 0 17:31 pts/16 00:00:00 -f
```

You can also use pstree or ps --forest with or without the -e option to see the parent-child relationship of processes. The next example shows the -p option to pstree, which causes it to display PID numbers:

```
$ pstree -p
init(1)--acpid(1395)
|--atd(1750)
|--croud(1702)
```

```
|-kdeinit(2223)--+-firefox(8914)---run-mozilla.sh(8920)---firefox-bin(8925)
  |--gaim(2306)
  |--gqiew(14062)
  |--deinit(2228)
  |--deinit(2294)
  |--deinit(2314)+--bash(2329)---ssh(2561)
    |--bash(2339)
      |--bash(15821)---bash(16778)
      |--deinit(16448)
      |--deinit(20888)
      |--oclock(2317)
      |--pam-panel-icon(2305)---pam_timestamp_c(2307)
```

```
|-login(1823)--bash(20986)+--pstree(21028)
  |--sleep(21026)
```

The preceding output is abbreviated. The line that starts with -kdeinit shows a graphical running many processes, including firefox, gmail, and clock. The line that starts with -login shows a textual representation running sleep in the background and running pstree in the foreground. Refer to $$: PID Number on page 995 for a description of how to instruct the shell to report on PID numbers.