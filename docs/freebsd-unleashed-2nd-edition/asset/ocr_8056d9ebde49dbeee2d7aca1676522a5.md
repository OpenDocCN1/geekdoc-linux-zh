process table and the tools that interact with it are an embodiment of what makes a Unix system what it is: a fully accessible machine with all the moving parts exposed and all the nuts and bolts showing. This accessibility gives you the power to tune everything the system does, no matter how minute. That’s the essence of Unix.

This chapter discusses several process-monitoring tools—namely ps, top, and kill. Some are more user friendly than others, and some are more versatile than others. The chapter also takes a look at the cron program, which is a scheduler for tasks that have to happen periodically—another feature that separates the servers from the desktops.

# ## Performance Monitoring with top

The easiest to use of the process-monitoring utilities is top, so named because it was originally designed to list the top-10 processes currently running on the system, in descending order of CPU usage. The current version of FreeBSD’s top by default shows you every process currently running in any state—somewhere around 30 processes on a freshly installed FreeBSD system.

The benefit that top provides is that it’s interactive and works in real time. When you run it, it takes over your terminal and updates itself every second, giving you instantaneous information about the state of the system at that moment. You can also pass top commands, such as the kill and renice commands (covered later in this chapter), or give it different options for filtering the processes it shows you. This makes top an immensely useful tool for reining in an out-of-control server, fine-tuning the performance of certain tasks, or simply keeping an eye on things as you work in another window.

# ### top Output Explained

When you run the top program, you get output similar to what’s shown in Listing 13.1.

| LISTING 13.1 Sample Output of top | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|
| last pid: 30283; load averages: 0.51, 0.89, 0.87 up 52+15:48:43 11:19:03 | | | | | | | | | | | |
| 126 processes: 1 running, 124 sleeping, 1 zombie | | | | | | | | | | | |
| CPU states: 0.7% user, 0.0% nice, 2.8% system, 0.7% interrupt, 95.8% idle | | | | | | | | | | | |
| Mem: 142M Active, 35M Inact, 59M Wired, 7496K Cache, 35M Buf, 4256K Free | | | | | | | | | | | |
| Swap: 500M Total, 48M Used, 452M Free, 9% Inuse | | | | | | | | | | | |
| | | | | | | | | | | | | |
| PID | USERNAME | PRI | NICE | SIZE | RES | STATE | C | TIME | WCPU | CPU | COMMAND |
| 19460 | mysql | 2 | 0 | 25908K | 2692K | poll | 0 | 112:20 | 2.20% | 2.20% | mysqld |
| 30283 | bob | 2 | 0 | 1360K | 976K | swwait | 1 | 0:00 | 6.02% | 1.56% | qpopper |
| 30282 | root | 29 | 0 | 2076K | 1236K | CPU1 | 0 | 0:00 | 3.14% | 0.93% | top |
| 245 | root | 2 | 0 | 868K | 232K | select | 1 | 177:39 | 0.00% | 0.00% | healthd |
| 18427 | root | 2 | 0 | 7592K | 5092K | select | 0 | 80:24 | 0.00% | 0.00% | named |
| 86694 | frank | 10 | 0 | 1700K | 56K | nanslp | 0 | 76:46 | 0.00% | 0.00% | elm |
| | | | | | | | | | | | |