![](bbox=[0.1, 0.12, 0.9, 0.48])

Figure 11.3 Setting up a new user account with YaST.

# System Administration Commands

As you start using Linux, you'll want to make sure all parts of the system are running smoothly. There are commands that you can use to monitor currently logged on users, as well as the processes they are running.

If any of your users have a problem with any application, you can use the kill command to kill that application. If an important program or procedure is about to run, commands such as nice and renice can help you raise or lower the priority associated with the program of your choice.

# who and w

Although the who and w commands both tell you which accounts are currently logged on to the Linux system, the w command actually goes into more detail. As an administrator, you should check logons regularly; for example, the following output from who shows the same person logged on from two different locations:

```
mj tty1 Sep 22 10:24
tr tty1 Sep 21 21:28 (linux2.mommabears.com)
mj tty0 Sep 21 21:18 (cracker.notnice.cba)
```

Because user mj is logged on from the local computer and remotely from the cracker computer, you should be concerned that someone else is using mj's username and password to break into your system.