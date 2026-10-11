# # Chapter Six

# ## Process Commands

Today’s operating systems are capable of multitasking, which means they can do more than one thing at a time. They switch rapidly between executing programs, and the Linux kernel manages this. Linux uses processes to organize the programs queued for execution in the CPU.

Sometimes, a computer system can become slow, or a specific application might stop working. This chapter is designed to show you the command-line tools you can use to terminate certain processes that don’t work properly during the system operations.

When your system wakes, certain activities are activated as processes by the kernel. This is followed by a program called init being launched. This program runs shell scripts known as init scripts, which are used to start the system services. Lots of these services are implemented as daemon programs, working in the background and doing what they have to do without a user interface. You can find the processes command here:

```
[gha@localhost ~]$ ps
  PID TTY          TIME CMD
   48 hvc0     00:00:00 sh
   82 hvc0     00:00:00 ps
```

The result lists process that are sh and ps respectively. If we add an option to the command ps, we can detailed result on our screens. See the following example.

```
[gha@localhost ~]$ ps x
  PID TTY          STAT TIME COMMAND
   1 ?        S      0:00 /bin/sh /sbin/init
   2 ?        S      0:00 [kthread]
   3 ?        I      0:00 [kworker/0:0]
   4 ?        I<     0:00 [kworker/0:0H]
   5 ?        I      0:00 [kworker/u2:0]
   6 ?        I<     0:00 [mm_percpu_wq]
   7 ?        S      0:00 [ksoftirqd/0]
   8 ?        S      0:00 [kdevtmpfs]
   9 ?        I<     0:00 [netns]
```