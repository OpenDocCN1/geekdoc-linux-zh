
## TABLE 4.2 Common Options to the ps Command

| Option | Action |
|---|---|
| a | Shows all processes that are running, including processes that do not belong to you. |
| u | Lists the username that the process belongs to. |
| w | Enables "wide" output. Basically, this wraps the output of a line to fit in your terminal window instead of just truncating the output as it would otherwise do. |
| x | Shows daemon processes as well as normal processes. In other words, shows processes running in the background that have no terminal attached to them. |
| U username | Lists processes belonging to the user username instead of to yourself. |

Remember that FreeBSD is case sensitive, so u and U in the previous table are treated as different options. Here is some sample output from running the ps command with no options:

```
12572 tty0 S 0:00.01 /usr/local/bin/bash
12578 tty0 T 0:45.04 /usr/local/bin/mutt
12582 tty0 R 1:22:01 grep
```

Let's look at what this output means.

The first number in each line is the process ID number, also known as the PID. The PID is simply a number that FreeBSD (and sometimes you) use to refer to this process.

The second column contains the controlling terminal that started the process. If the process doesn't have a controlling terminal, such as a daemon process that was not started from a terminal, this column will contain ??. The third column contains the status of the process. In this case, the first line contains an S. This means that the process is sleeping, probably because it is waiting for some other event (such as the user to type something and give the process something to do). The second line contains a T in the status column. This means that the process is stopped. A stopped process is basically one that has been paused and can later be resumed. We will look at how to do this later on. The third process has an R in the status column. This means that the process is runnable. In a nutshell, this means that the process is in FreeBSD's queue to be run and is waiting for FreeBSD's scheduler to enable it to access the CPU.

There are more statuses as well. To see all the status codes and their meanings, see the man page for ps.

The third column is the amount of CPU time that the process has used. This can often give you a clue as to a process that has gone out of control and is misbehaving. For example, if people have been complaining that the system is slow, and you find a process in the ps output that has used an hour of CPU time and was only started 65 minutes ago, it is most likely the culprit and needs to be shut down and restarted.

The fourth column, of course, simply gives the name of the process.

## Terminating a Process

Occasionally, a process in FreeBSD might stop responding. (No doubt, Windows users are familiar with this.) When this happens, you might have to force the process to quit, similar to the infamous Ctrl+Alt+Delete, End Task sequence in Windows. From the FreeBSD command line, this can be done with the kill command. The kill command is followed by the PID of the process you want to kill (which you can get from the output of the ps command).

For example, in the last section, one of the processes listed is /usr/local/bin/mutt. Mutt happens to be an email client that is available for FreeBSD. Assume that the mutt program, for whatever reason, has stopped responding to the user's commands. We see in the output from the ps command that the PID of the mutt program is 12578. To kill this process, you can use the command kill 12578. After the command is issued, the mutt program should terminate and the command line should reappear. If the kill command doesn't work, you can use the -9 option to force the misbehaving process to terminate (for example, kill -9 12578). The difference is that the normal kill command attempts to terminate the process gracefully by sending it a signal telling it to clean up after itself and exit. However, the process can ignore this request. In this case, the kill -9 command will forcefully "squash" the process. This command is not a request, but rather a forceful termination that cannot be ignored.

![](img/ba0161b65b37e94cffc801ecbacaba5e_88_0.png)

> The -9 option to the kill command should only be used if the normal kill command failed to terminate the process. -9 basically "pulls the rug" out from under the process. As such, the process will not get a chance to do any pre-termination actions that it might normally do, such as delete temporary files it might have created, and so on.

What happens if you have a busy server with several thousand processes running? Obviously, you don't want to have to read the entire process list, looking for the PID of the correct process. In this case, you can use what is called a pipe. A pipe basically takes the output of one command and "pipes" it into another command for further processing or filtering. In this case, we can use the grep command to search the output of ps and display only the lines that match our search terms. For example, suppose that the mutt mail program is not responding. We could use the following command to find its PID number:

```
ps | grep "mutt"
```

The previous command will display only the lines of the ps output that contain the phrase mutt.

You can also kill a process by name using the killall command. For example, killall mutt will kill any process named mutt.

![](img/ba0161b65b37e94cffc801ecbacaba5e_89_0.png)

> Use the killall command with care because it can have undesirable side effects. For example, if multiple copies of mutt are running, killall will terminate all of them instead of just the one that is misbehaving.

![](img/ba0161b65b37e94cffc801ecbacaba5e_89_1.png)

> To kill processes belonging to users other than yourself, you must be logged in as the root user. Also remember that, by default, the ps command will only list processes belonging to you. So if you are the system administrator, and a user calls you to tell you that her mutt program has locked up for example, you will need to use either the -u option to the ps command with the user's login name or the -a option in order to find the PID for the offending process. Of course, you will also need to be the root user in order to kill the offending process.

## Stopping a Process

If you want to stop a process that is currently running, you can use Ctrl+z. The system will respond with something like the following:

```
[1]+ Stopped         mutt
```

You will then be returned to the command prompt, from which you can run more commands.

The 1 at the beginning of the line is the job number of the process. It is the number you will use when you want to start the job again.

## Restarting a Process

Restarting a process is also known as bringing a job into the foreground. The command to do this is `fg` followed by the job number. For example, to bring the `mutt` program back into the foreground, you would type `fg 1`, which would place you back into `mutt` and allow you to work in it again.

![](img/ba0161b65b37e94cffc801ecbacaba5e_90_0.png)

> If you try to log out of the system while you still have stopped jobs, the system will respond with a message that says There are stopped jobs, and you will be returned to the command prompt. If you really want to log out of the system without handling the stopped jobs first, type `exit` again. You will be logged out and the stopped jobs will be terminated.

## Moving a Process into the Background

The difference between stopping a process and moving a process into the background is that a stopped process has its execution suspended. A process running in the background, however, continues to run, but returns you to the command prompt so that you can do other things while the process runs in the background.

To move a process into the background, first stop it using the `Ctrl+z` key combination as described previously. Next, after the process has been stopped, use the `bg` command, followed by the job number to restart it in the background (for example, `bg 1`). Later, if you want to move it back into the foreground where you can work with it, simply type `fg 1` as before to resume a stopped job.

![](img/ba0161b65b37e94cffc801ecbacaba5e_90_1.png)

> You might be wondering when it would make sense to have a process running in the background where you couldn't interact with it. A good example of where this would be useful is the `find` command. For example, suppose that you have a lost file and you are searching a large file system (50Gb or so) for the file. This is going to take quite a bit of time, as in at least several minutes even on a very fast hard disk.
> 
> If you leave the `find` command in the foreground, you will be unable to use your system for anything else during the time that the command is running. Basically, you will just have to wait until it is finished. In this case, you might want to have `find` direct its output to a text file for later viewing. (You can do this by following the `find` command with a redirect. For example, `> MyLostFile.txt` will send any output that `find` generates into a new file
