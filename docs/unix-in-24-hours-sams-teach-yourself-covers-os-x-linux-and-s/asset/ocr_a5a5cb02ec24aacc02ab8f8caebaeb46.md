# Hour 15. Job Control

# Goals for This Hour

In this hour, you will learn

+   About job control in the shell: stopping jobs
+   How to put jobs in the background and bring them back to the foreground
+   How to find out what tasks are running by using jobs and ps
+   How to terminate errant processes by using kill

In this hour you will learn about how Unix handles jobs and how you can manipulate them. Commands you will learn include jobs and ps, to see what processes are running; fg and bg, to move jobs back and forth between the foreground and background; and kill, to terminate jobs you no longer want around.

This hour presents an explanation of a Unix philosophical puzzle: What is a running program? To learn the answer, you are introduced to ps and jobs, for controlling processes; fg and bg, to move your own processes back and forth between the foreground and background; and the quasi-omnipotent kill command, for stopping programs in their proverbial tracks.

# Wrestling with Your Jobs

Every program you run is a job, according to the Unix system, and although it might not be obvious, you have the ability to start and stop jobs at any time.

# Task 15.1: Job Control in the Shell: Stopping Jobs

Whether you’re requesting a man page, listing files with ls, starting vi, or running just about any Unix command, you’re starting one or more processes. In Unix, any program that’s running is a process. You can have multiple processes running at once. The pipeline ls -l | sort | more invokes three processes: ls, sort, and more. Processes in both the C and Korn shells are also known as jobs, and the program you’re running is known as the current or active job.

Any job or process can have various states, with “running” being the most typical state. In both shells, you can stop a job by pressing ^z. To restart it, enter fg (foreground) when you are ready.

+   1. Earlier I was perusing the man page entry for sort. I had reached the bottom of the first screen:

Click here to view code image

```
$ man sort

SORT(1)          DYNIX Programmer's Manual          SORT(1)
```