
# Terminating/Restarting with the kill Command

You know how to see what processes are dominating your CPU and slowing down your system, but what do you do about it? To terminate a process on a Linux system (and in most other Unix-like systems), you use the kill command. Issued with only a process ID as an argument, the kill command will send a signal to the process telling it to terminate. Some processes are able to catch the signal and cannot be killed easily—the “John Wayne” processes, for which you must use a -9 argument, making the command look like this:

```
$ kill -9 234
```

The -9 cannot be caught, so the process whose ID is specified will terminate. It's generally a good idea to try issuing the kill command without the -9 argument first, because some programs close themselves cleanly this way, without leaving temporary files and so on.

If you need to restart a daemon, because it is hung up or because you've made a configuration file change, you can do this by entering the kill command with a -1 argument before the process ID, as in the example.

```
$ kill -1 234
```

Do not combine this with the -9 argument. Using

```
$ kill -HUP 234
```

will do the same thing. You may notice when you speak to other system administrators that HUP is used as a verb, basically meaning restart.

> NOTE Linux supports a command called nohup, which launches a program in such a way that it ignores the H kill signal. This allows you to run a program that survives a logout, which can be handy if you want to run a program that will be running for a very long time, but you don't need to tie up a terminal or term window with that program. To use this utility, just place it before an ordinary command, as in nohup number-cruncher.

# Terminating/Restarting Processes Using Scripts

In Red Hat Linux (as in many commercial versions of Unix), each daemon has a single script that allows you to kill it, check its status, or restart it. The handling of these scripts is based on run levels. Run levels are more thoroughly discussed in Chapter 5. For now you only need to know that the system has several modes it can boot into. The selection of the run level allows only certain processes to be started by the init process. On Red

![](img/4fb617eb648f87def380ef5d92052d01_110_0.png)

# Chapter 3 Linux Files and Processes

Hat systems, these scripts exist in /etc/rc.d/init.d, one for each daemon that is to be started or shut down by the system either at bootup or level change. Under the /etc/rc.d/ directory, there is a subdirectory for each possible run level, which contains symbolic links to the scripts that should be run for that level. Most scripts contain the ability to start, status-check, and restart their specific daemons.

To kill the sendmail daemon, for instance, you use the stop option:

```
# /etc/rc.d/init.d/sendmail stop
```

If the daemon is stopped, you'll see the message:

Shutting down sendmail: [OK]

The [OK] will be replaced by [FAILED] if the daemon was not shut down as shown below. This might happen if the daemon that you are trying to kill is not currently running.

Shutting down sendmail: [FAILED]

If you wish to start a daemon that is not currently running, substitute the word start for stop:

```
# /etc/rc.d/init.d/sendmail start
```

The system will then attempt to start up the sendmail daemon. A message confirming the successful startup will be displayed.

Starting sendmail: [OK]

If you want to know whether a daemon is running, instead of searching through a ps list, you may use the script in /etc/rc.d/init.d which governs that daemon, specifying the status option, as in:

```
$ /etc/rc.d/rc.local/sendmail status
```

```
sendmail (pid 4437) is running...
```

Last, you may restart a daemon that is currently running—or as some would say, "HUP" the daemon. To do this for sendmail, you would use

```
# /etc/rc.d/init.d/sendmail restart
```

You will then see the message

Shutting down sendmail: [OK]

if the shutdown succeeded, or

Shutting down sendmail: [FAILED]

if the shutdown was unsuccessful. Following the shutdown line, you will see

Starting sendmail: [OK]
if the sendmail daemon started or

Starting sendmail: [FAILED]
it it did not. A failure during the shutdown phase will not automatically prevent the da-
from restarting, although a problem with that daemon might cause both the shut-
downown and the startup to fail.

Shutting down sendmail: [FAILED]
Starting sendmail: [FAILED]

# In

We've looked at the ext2 filesystem: how it developed and how it is laid out. We've also
looked at processes and process management using such commands as ps, fg, bg, and
top. You got a first look at the init process and why it is so important. We'll look
in more detail at the init it scripts in Chapter 5 when we map out the entire startup process.

In Chapter 4, we'll discuss the different elements you'll need to perform system adminis-
tration tasks. Our discussion will include command-line tools, commands, and resources
to help you work through the problems you encounter.

# Tools of the Trade

Just as mechanics must be able to use their tools skillfully to keep your vehicle in working condition, so also must a Linux system administrator be able to use the tools of the trade to maintain a workable Linux system. In either case, what looks to the layman to be magical is in fact the implementation of some skill learned via previous experience. Success comes from knowing what has to be done, having the resources to do it, and implementing what you know. Remember that every task is a tool you might need later. In view of this, system administrators must learn the basic elements of the job to the point where they are second nature. Only then can these elements be used as building blocks to accomplish tasks that are more challenging.

In this chapter, we'll identify several such building blocks like pages, info pages, and Web-based Linux support services before looking at some command-line tools that will be useful in your Linux systems administration experience. We'll give you some basic commands to store in your Linux toolbox, explain how you can make commands work together to solve bigger tasks with piping and redirection, talk about the different ways of locating specific files on your system, and discuss the use of quoting, the history list, and Bash shell commands.

# Locating Help Resources

One of the most important elements in establishing yourself as a system administrator is demonstrating that you know where to find an answer you don't know off-hand. Some really sharp system administrators will advise you never to admit that you don't know something. We wholeheartedly disagree with this approach. Yes, some people become angry when the answer isn't that you can give without verifying the information, but it should never change your policy of being honest. More often than not, people are relieved to hear an honest reply as long as you come back with the answer in a reasonable time. When asked something you don't readily know, always give the same basic answer: "I haven't seen that in a while, but I know where to get the information you need. I'll be back with you as soon as I get it."

If you can't recall the answer, take the honest approach and forget about the knowledge-struct. The knowledgeable strut puts you in a position of having to be (or at least appear be) omniscient, and none of us are. We have also found people who pretend to know all the answers to come off as and some clients love to prove system administrator wrong. You are less of a target if you are honest about your abilities—as long as one of abilities is the ability to find an answer.

To find answers when you need, look at the numerous information resources that are available if you know where to find them. One of features we like about Linux is the availability of resources. In a Microsoft Windows machine, you can't just bring up a page of useful information on a command. There are documents and online help features in Windows, but tools generally don't answer questions unless they fit into a specific mode, or they get almost to the point where they're helpful and then stop. They don't offer enough information to piece together the answers that exist between the lines. In Linux and other Unix-like operating systems, the information is most often there if you know what you're looking for.

# Man Pages

Man (short "manual") pages are online documents that describe the format and functioning of commands and files as well as other tools available on your Linux system. Man pages are not meant to be comprehensive but rather to give general information about usage. Man pages aren't meant to take the place of the source documentation, but instead to highlight how to use the referenced resource. Unless the system was installed without them, man pages are readily available from the command line. Simply type man to get the man page on how to use man pages. The basic format of the command is:

+   - man [options] topic

There is a configuration file for the man command located at /etc/man.config. This file allows you to configure the environment variables that the man command uses if you don't wish to specify them on the command line. The options include the path that should be searched for man pages, the order in which the manual sections should be searched, and whether to store the man pages in a compressed format.
