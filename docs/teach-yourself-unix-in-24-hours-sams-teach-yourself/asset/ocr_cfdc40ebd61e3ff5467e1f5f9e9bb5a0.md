# Job Control

```
% Broken pipe
% kill 7460
7460: Not owner
%
```

5. Finally, if you forget and leave stopped jobs in the background and try to log out,
here's what happens:

```
% logout
There are stopped jobs.
%
```

You must use fg to bring each job into the foreground and terminate
normally, or use kill to terminate each of the jobs, then log out.

In this task, you have been introduced to the kill command and some of the signals
associated with it.

![](bbox=[0.125, 0.365, 0.203, 0.386])

![](bbox=[0.875, 0.345, 0.972, 0.447])

# Summary

Although the file is the underlying unit in the UNIX file system, including all directories,
the most fundamental piece of UNIX is the process. In this hour, you learned how to have
background processes, how to stop and restart processes, and how to use kill to quit any
errant program—running or not.

# Workshop

The Workshop summarizes the key terms you learned and some poses questions about the
topics presented in this chapter. It also provides you with a preview of what you will learn
in the next hour.

# Key Terms

+   **control number** A unique number that the C shell assigns to each background job for
reference and for using with other commands, such as fg and kill.

+   **current job** The job that is currently running on the terminal and keyboard (it's the
program you're actually running and working within).

+   **foreground job** A synonym for current job.

+   **errant process** A process that is not performing the job you expected it to perform.

+   **job** A synonym for process.

+   **kill** Terminate a process.