# Learning Who Is Logged In: who

On systems that allow users to log in to other users' machines or special servers, you will want to know who is logged in. You can generate such a report by using the **who** command:

```
[michael@workbox michael]$ **who**
```

The **who** report looks like this:

```
michael tty1 Jun 14 18:22
rwhite pts/9 Jun 14 18:29 (:0:0)
root pts/11 Jun 14 21:12 (:0:0)
root pts/12 Jun 14 23:38 (:0:0)
```

# A Variation on who: w

The **w** command displays the same information that **who** does and a whole lot more. The details of the report include who is logged in, what their terminal is, where they are logged in from, how long they've been logged in, how long they've been idle, and their CPU utilization. The top of the report also gives you the same output as the **uptime** command.

# Networking Tools

If you are starting your experience with Linux in an already networked environment, you may find some of these tools handy for getting around.

![](bbox=[0.12, 0.62, 0.28, 0.665])

These networking tools are useful, but allowing **telnet**, **rsh**, remote X, and **ftp** connections to a server can be risky from a security standpoint. See Module 9 for more information on securing a Linux server.

# telnet

As was mentioned in earlier modules, Linux understands the concept of multiple users logged in to the same workstation at the same time. So in order to allow for someone to log in to another host from remote, the **telnet** command was created.

The format of the command is as follows:

```
[rwhite@workbox rwhite]$ **telnet gregory**
```