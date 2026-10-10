ery Linux system, regardless of distribution, network configuration, and overall system design, has these core services: init, inetd, syslog, and cron. The functions performed by these services may be simple, but they are also fundamental. Without their presence we would miss a great deal of Linux’s power.

In this chapter, we’ll discuss each one of the core services, its corresponding configuration file, and suggested method of deployment (if appropriate). You’ll find that the sections covering these simple services are not terribly long, but don’t neglect this material. We highly recommend taking some time to get familiar with their implications (perhaps during those lovely commutes through traffic every morning). Many creative solutions have been realized through the use of these services. Hopefully, this chapter will inspire a few more.

# ## THE INIT SERVICE

The **init** process is the patron of all processes. *Always* be the first process that gets started in any UNIX-based system (such as Linux), init’s process ID is always 1. Should init ever fail, the rest of the system will most definitely follow suit.

The init process serves two jobs: the first is to be the ultimate parent process. Because init never dies, the system can always be sure of its presence and, if necessary, make reference to it. The need to refer to init usually happens when a process dies before all of its spawned children processes have completed. This causes the children to inherit **init** as their parent process. A quick execution of the **ps -af** command will show a number of processes that will have a parent process ID (PPID) of 1.

The second role for init is to handle the various runlevels by executing the appropriate programs when a particular runlevel is reached. This behavior is defined by the *`/etc/initab`* file.

# ### The `/etc/initab` File

The `/etc/initab` file contains all the information **init** needs for starting runlevels. The format of each line in this file is as follows:

```
`id:runlevel:action:process`
```

> **NOTE:** Lines beginning with the hash sign (#) are comments. Take a peek at your own *`/etc/initab`*, and you’ll find that it’s already *liberally* commented. If you ever do need to make a change to *`/etc/initab`* (and it’s unlikely that you’ll ever need to), you’ll do yourself a favor by including liberal comments to explain what you’ve done.

Table 9-1 explains the significance of each item in the *`/etc/initab`* file’s line format.