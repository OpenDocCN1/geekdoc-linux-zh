# Log Management

Log management is a mundane daily task for all system administrators. Logs tell the story of your systems; you should consider them sacred and watch over them at all times. Properly managed logs do not take up too much space on a file system, are of a usable size, are archived for future reference, and provide an adequate view into the past activity of your systems. Many Unix systems provide tools that handle some of these tasks automatically, but a few tweaks here and there can make the job even easier.

Log management involves four major functions: location, file size, rotation, and archiving. This section describes each of these functions and how to implement and tune them on your own systems.

# Location

The location of log files in a Unix file system is critical to the performance and scalability of the overall system. The most important aspect of a log file is that it grows, and sometimes growth can become out of control. A system administrator’s great fear is the log file growth will quickly fill up the file system where the file is located. This fear is justified; most (if not all) administrators have seen a single log file fill a file system to capacity.

The best way to mitigate this situation is to place your logs in their own dedicated file system. Putting logs in the / or /var file systems is probably a bad idea, as those systems usually contain critical file systems. Filling up /var can have a disastrous effect on a running system, often requiring maintenance in single-user mode

Although you may lose logs when the /var partition fills up, the logs are the only thing you’ll lose. The operating system will keep running, and most applications that are already running will go about their normal business. However, /var is often a part of the / file system by default; you may have to force its creation during installation.

![](bbox=[0.235, 0.735, 0.365, 0.803])

# Create a Separate /var/log File System

If you are running an application on a server that makes heavy use of the /var file system, you may want to create a separate /var/log file system (separate from /var itself). This prevents overactive log files from interfering with your applications and vice versa. Sendmail is an example of such an application; its default message queue is located in /var/spool/queue.