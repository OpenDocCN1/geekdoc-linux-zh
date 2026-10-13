# FIGURE 9-9

```
[root@server1 ~]# iostat
Linux 2.6.32-71.el6.x86_64 (server1.example.com)      01/26/2011      _x86_64_
(2 CPU)
CPU and storage device statistics
avg-cpu:  %user   %nice %system %iowait  %steal %idle
           0.05    0.00    0.03    0.03    0.00 99.88

Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
sda               0.00       0.01       0.00      2368        0
sdb               0.00       0.01       0.00      2144        0
scd0              0.00       0.03       0.00      7392        0
vda               0.21       2.70       1.97    765626    556858
dm-0              0.00       0.00       0.00       256        0

[root@server1 ~]#
```

Process priorities in Linux specify numbers that seem counterintuitive. The range of available nice numbers can vary from -20 to 19. A process given a priority of -20 takes precedence over all other processes. In contrast, a process given a priority of 19 will wait until the system is almost completely free before taking any resources. The default nice number of a process is 0.

The nice command prefaxes other commands. For example, if you have an intensive script to be run at night, you might choose to start it with a command like the following:

```
$ nice -n 19 ./intensivescript
```

This command starts the noted script with the lowest possible priority. If started at night (or at some other time when a system is not loaded by other programs), the script is run until just about any other jobs, such as a script in the /etc/cron.* directories, are scheduled for execution. As such scripts are run on a schedule, they normally should take priority over some user-configured programs.

Sometimes a program is just taking up too many resources. If you need to make sure that program continues to run, one step before killing the associated process is to lower its priority with the renice command. Normally, the easiest way to identify a process that's taking up too many resources is by its PID in the output to the top command. That PID number is in the left-hand column of the output. For example, if you identify a process that's monopolizing current CPU and memory resources, copy the PID number of that process. If that number were 1234, the following command would change the nice number of that process to -10, which gives that process a higher priority than the default of 0.

```
# renice -10 1234
```