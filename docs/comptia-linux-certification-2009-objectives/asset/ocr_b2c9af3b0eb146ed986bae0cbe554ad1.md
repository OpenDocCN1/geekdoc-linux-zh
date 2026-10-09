# The nohup command

```
```
root@localhost: ~
[root@localhost ~]# nohup rpm -gal &
[1] 2928
[root@localhost ~]# nohup: appending output to `nohup.out`

[root@localhost ~]# 
```
```

*Figure 10-14: Enabling a background process to run after logging out of the system using the nohup command.*

# Running a Process After You Leave the System

If you have a task that cannot be completed until after you leave work, or if you have a task that is CPU intensive and may slow the system, you can start the task before you leave and specify that it continues even after you log out of the system. You can do this by using the nohup (no hangup) command. The nohup command should run in the background so that it does not tie up your terminal. To enable a command to run in the background after you have logged out, use the syntax nohup [command] &.

# How to Work with Delayed and Detached Jobs

# **Procedure Reference: Delay a Job**

To delay a job:

+   1. Login as root.
2. Determine which job you will like to schedule at a later time. Enter sleep [number of seconds to delay]; [command to issue] to schedule the job at a later time.

# **Procedure Reference: Detach a Job**

To detach a job:

+   1. Login as root.
2. Determine which job you will like to run after you log out of the system. Enter nohup [command to issue] & to schedule the job to continue running even after you log out.