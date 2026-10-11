level is 20 (or *rice -n 0* from the command line). For the programmer, this scheme is different, because they can use the *rice()* function to set the nice level directly to 0 through 39.

> **TIP** If you have a large compile you need to run but still need to use the system as your desktop, you may run the compile at a higher nice level so that your other applications will have more time at the CPU.

> **WARNING** Inappropriate use of the *nice* command, and in particular the *priocntl* command, can cause your system to respond sluggishly and malfunction and possibly cause you to have to reboot your system should you alter the priority of an essential system function. Changing process priorities isn’t something end users typically do, and it’s rarely done in system administration.

The *priocntl* (priority control) command allows you to display (as you have seen previously with the *-1* option) or set the scheduling parameters of specific processes. The priority range for both time-sharing and interactive processes can range from -60 to +60; real-time processes have a maximum configured priority of 59. System functions like the scheduler and the paging mechanism (*pagedaemon*) are assigned higher priorities, typically in the high 90s so that they execute with strong preference. You can use the *ps -ec1* command to display the global priority of a process. That priority is shown in the seventh (PRI) column. Figure 15.7 shows the output of the *ps -ec1* command.

Using the *priocntl* command, you can alter the performance of the scheduler, allowing you access to the real-time, time-sharing, and interactive classes of processes. The *priocntl* man pages go into great detail about the options of this command.

To use the *priocntl* command to designate a process priority, do the following:

+   1. Switch to a superuser with the *su* command.
+   2. Start a process with a designated priority using the following command:

```
# priocntl -e -c <class> -m <userlimit> -p <pri> <commandname>
```

-e executes the command; *-c <class>* specifies the class, which is typically TS for time-sharing or RT for real time; *-m <userlimit>* is the maximum amount that you change your priority when *-p* is used; and *-p pri <commandname>* is the relative priority for the RT thread. When you use *-p*, you can change a user-designated priority by -20 to +20.