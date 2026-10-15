

environment variable HISTCMD that contains the current command number. Fortunately, you can use a shortcut:

Click here to view code image

```
In /, oh master: PS1="(The current command is #\!) $ "
(The current command is #132) $
```

The number shown is the command number, as used by the shell history mechanism, with a slightly more succinct variation:

Click here to view code image

```
(132) $ echo hi
hi
(133) $ ls News
mailing.lists.usenet  usenet.l          usenet.alt
(134) $ !132
echo hi
hi
(135) $
```

Here’s another example that you might find valuable:

```
(135) % PS1="\h (\!) % "
limbo (136) $
```

This is close to what I use myself, but I like to include the basename of the current directory. Basename means the name of the closest directory, so the basename of /home/taylor is taylor, for example. Also, I replace the dollar sign with a colon, which is a bit easier on the eyes:

Click here to view code image

```
limbo (136) $ PS1="\h (\W) \! : "
limbo (taylor) 137 :
```

Experiment until you find a set of variables that can help you customize your Unix prompt. I strongly recommend that you use command numbers to familiarize yourself with the history mechanism.

Taking advantage of the command-alias capability is a helpful way to cut down on entering short commands time and again, but what if you have a series of 5 or 10 commands you often enter in sequence? That’s where shell scripts can help (see Hour 16).

### Summary

This hour introduced you to many of the most powerful aspects of Unix command shells. Practice creating aliases and working with the history list to minimize your typing. Also, find a prompt you like and set it in your .bashrc or .profile so that it will be your default.

### Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

### Key Terms

**basename** The basename is the name of the closest directory. For example, the basename of `/usr/home/taylor` is `taylor`.

**command number** The unique number by which the shell indexes all commands. You can place this number in your prompt by using `\$HISTCMD` and use it with the history mechanism as `!command-number`.

### Exercises

- 1. How do you tell bash that you want it to remember the last 30 commands during a session and to remember the last 10 commands across login sessions?
- 2. Assume that you get the following output from entering history:

```
1  ls -CF
2  who | grep andrews
3  wc -l < test
4  cat test
5  history
```

  What would be the result of entering each of the following history commands?
  `!2  !w  !wh  echo !1`
- 3. Some Unix systems won’t enable you to use the following. What danger do you see lurking in this alias?
  `alias who  who -a`
- 4. Which of the following aliases do you think would be useful?
  `alias alias='who'`
  `alias ls='cp'`
  `alias copy='cp -'`
  `alias logout='vi'`
  `alias vi='logout'`
  `alias bye='logout'`
- 5. Set your prompt to the following value. Remember that 33 should be replaced with the appropriate command number each time:

  Click here to view code image

  `#33 - I know lots about Unix. For example:`

### Preview of the Next Hour

In the next hour, you’ll learn how to get even more out of your shell. You’ll learn about shell programming and how to create shell programs on-the-fly.

## Hour 15. Job Control

### Goals for This Hour

In this hour, you will learn

- About job control in the shell: stopping jobs
- How to put jobs in the background and bring them back to the foreground
- How to find out what tasks are running by using jobs and ps
- How to terminate errant processes by using kill

In this hour you will learn about how Unix handles jobs and how you can manipulate them. Commands you will learn include jobs and ps, to see what processes are running; fg and bg, to move jobs back and forth between the foreground and background; and kill, to terminate jobs you no longer want around.

This hour presents an explanation of a Unix philosophical puzzle: What is a running program? To learn the answer, you are introduced to ps and jobs, for controlling processes; fg and bg, to move your own processes back and forth between the foreground and background; and the quasi-omnipotent kill command, for stopping programs in their proverbial tracks.

### Wrestling with Your Jobs

Every program you run is a job, according to the Unix system, and although it might not be obvious, you have the ability to start and stop jobs at any time.

### Task 15.1: Job Control in the Shell: Stopping Jobs

Whether you’re requesting a man page, listing files with ls, starting vi, or running just about any Unix command, you’re starting one or more processes. In Unix, any program that’s running is a process. You can have multiple processes running at once. The pipeline ls -l | sort | more invokes three processes: ls, sort, and more. Processes in both the C and Korn shells are also known as jobs, and the program you’re running is known as the current or active job.

Any job or process can have various states, with “running” being the most typical state. In both shells, you can stop a job by pressing ^z. To restart it, enter fg (foreground) when you are ready.

- 1. Earlier I was perusing the man page entry for sort. I had reached the bottom of the first screen:

Click here to view code image

```
$ man sort

SORT(1)          DYNIX Programmer's Manual          SORT(1)
```
