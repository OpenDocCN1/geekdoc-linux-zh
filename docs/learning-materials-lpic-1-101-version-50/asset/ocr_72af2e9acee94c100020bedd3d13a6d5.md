```
kill-window Window one? (y/n)
```

Other interesting window commands include:

+   *   **Ctrl** + **b** + **f**
+   	find window by name.
+   *   **Ctrl** + **b** + **.**
+   	change window index number.

To read the whole list of commands, consult the manual page.

# ## Panes

The window-splitting facility of **screen** is also present in **tmux**. The resulting divisions are not called *regions* but *panes*, though. The most important difference between regions and panes is that the latter are complete pseudo-terminals linked to a window. This means that killing a pane will also kill its pseudo-terminal and any associated programs running within.

To split a window horizontally, we use **Ctrl** + **b** + **-**:

```
Tasks:   93 total,   1 running,  92 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  4050960 total,  3730920 free,  114880 used,  205160 buff/cache
KiB Swap:  4192252 total,  4192252 free,       0 used.  3716004 avail Mem

  PID USER     PR  NI  VIRT   RES  SHR S %CPU %MEM   TIME+ COMMAND
1340 carol  20   0 44876  3400 2800 S  0.3  0.1   0:00.24 top
   1 root     20   0 139088 6988 5264 S  0.0  0.2   0:00.50 systemd
   2 root     20   0      0     0    0 S  0.0  0.0   0:00.00 kthreadd
   3 root     20   0      0     0    0 S  0.0  0.0   0:00.04 ksoftirqd/0
   4 root     20   0      0     0    0 S  0.0  0.0   0:01.62 kworker/0:0
   5 root     0 -20      0     0    0 S  0.0  0.0   0:00.00 kworker/0:0H
   7 root     20   0      0     0    0 S  0.0  0.0   0:00.06 rcu_sched
   8 root     20   0      0     0    0 S  0.0  0.0   0:00.00 rcu_bh
   9 root      rt   0     0     0    0 S  0.0  0.0   0:00.00 migration/0
  10 root     0 -20      0     0    0 S  0.0  0.0   0:00.00 lru-add-drain
  11 root      rt   0     0     0    0 S  0.0  0.0   0:00.01 watchdog/0
  12 root     20   0      0     0    0 S  0.0  0.0   0:00.00 cpuhp/0

$ ____________
```