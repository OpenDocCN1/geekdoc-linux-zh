7. Note the process ID (PID) for monitor. View the CPU percentage for the process, which is expected to hover around 15% to 20%.

```
$student@servera ~]$ top
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
0671 student 20 0 222448 2964 2716 S 18.7 0.2 00:27:35 monitor
...output omitted...
```

View the load averages. One minute load average is currently less than a value of l. The value observed may be affected by resource contention from another virtual machine or the virtual host.

top - 12:23:45 up 11 days, 1:09, 3 users, load average: 0.21, 0.14, 0.05

8. In the left terminal shell, run a second instance of monitor. Use the ampersand (&) to run the process in the background.

```
$student@servera ~]$ monitor &\n[2] 6498
```

9. In the right terminal shell, note the process ID (PID) for the second monitor process. View the CPU percentage for the process, also expected to hover between 15% and 20%.

```
$student@servera ~]$ top
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
0671 student 20 0 222448 2964 2716 S 19.0 0.2 01:36:53 monitor
6498 student 20 0 222448 2996 2748 R 15.7 0.2 01:16:34 monitor
...output omitted...
```

View the one minute load average, which is still less than l. It is important to wait for at least one minute to allow the calculation to adjust to the new workload.

top - 12:27:33 up 11 days, 1:13, 3 users, load average: 0.36, 0.25, 0.11

10. In the left terminal shell, run a third instance of monitor. Use the ampersand (&) to run the process in the background.

```
$student@servera ~]$ monitor &\n[3] 6881
```

11. In the right terminal shell, note the process ID (PID) for the third monitor process. View the CPU percentage for the process, again expected to hover between 15% and 20%.

```
$student@servera ~]$ top
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
6881 student 20 0 222448 3032 2784 S 18.6 0.2 00:11:48 monitor
6498 student 20 0 222448 2996 2748 S 15.6 0.2 00:47:86 monitor
```