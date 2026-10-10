# Using the shutdown Command

The normal way to shut down the system is with the shutdown command, which you first read about in Chapter 2 in the section titled “Shutting Down FreeBSD.” Before you actually shut down the system, however, take a moment to learn about several other options for using this command.

The basic syntax of the shutdown command is as follows:

```
shutdown [option] [when] [broadcast message]
```

The first argument tells shutdown what to do, the second argument tells shutdown when to do it, and the third argument tells shutdown the message it should send to all logged-in users. Table 4.1 lists the options that can be used for [option] in shutdown and what they do.

| **Option** | **Result** |
| --- | --- |
| Nothing | Kicks everybody off the system and brings the system down to single-user mode with no network support. This is rude to the users, but quick and efficient. |
| -h | Halts the system. |
| -p | Halts the system and turns off the power (if the system supports automatic power-off and the kernel is configured to support power management). |
| -r | Reboots the system. |
| -k | Kicks everybody off the system and disables any further logins (except from the root user). This option leaves the system in multiuser mode and connected to the network, though. This is useful for occasions when you need to do emergency maintenance but require network access while you do it. |
| -o | Shuts down without sending a signal to init. This is not usually a good idea because it prevents program-specific shutdown scripts from running. |
| -n | If the -o option has also been specified, this option prevents the filesystem cache from being flushed before the shutdown. This is probably never a good idea because it can cause data loss. |

The “when” part of shutdown can be specified in several ways. As you learned in Chapter 2, the keyword now tells shutdown to perform the action immediately. shutdown also recognizes the format +n, where n is the number of minutes shutdown should wait before performing the action (this gives users time to save their files and close their programs). You can use the format yymmddhhmm to specify an exact time when the action should be performed. In this case, yy is the year, mm is the month, hh is the hour (in a 24-hour format), and mm is the minute. If the year and month parts are eliminated, shutdown assumes that the shutdown should happen today. If you specify a time that has already passed, shutdown will complain.