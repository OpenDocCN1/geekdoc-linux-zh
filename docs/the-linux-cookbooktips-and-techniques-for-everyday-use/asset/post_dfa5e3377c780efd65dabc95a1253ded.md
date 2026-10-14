
[1]+  Stopped                  info -f cookbook.info

In this example, the job number is 1 and the command that has stopped is `info -f cookbook.info`. The `+` character next to the job number indicates that this is the most recent job.

If you have any stopped jobs when you log out, the shell will tell you this instead of logging you out:

```
$ logout RET
There are stopped jobs.
$
```

At this point you can list your jobs (see section [Listing Your Jobs]), stop any jobs you have running (see section [Stopping a Job]), and then log out.

## 4.3.2 Putting a Job in the Background

New jobs run in the foreground unless you specify otherwise. To run a job in the background, end the input line with an ampersand (`&`). This is useful for running non-interactive programs that perform a lot of calculations.

- To run the command **apropos shell > shell-commands** as a background job, type:

```
$ apropos shell > shell-commands &
[1] 6575
$
```

The shell outputs the job number (in this case, 1) and process ID (in this case, 6575), and then returns to a shell prompt. When the background job finishes, the shell will list the job number, the command, and then the text `Done`, indicating that the job has completed successfully:

```
[1]+  Done                  apropos shell > shell-commands
```

To move a job from the foreground to the background, first suspend it (see section [Suspending a Job]) and then type **bg** (for "background").

- For example, to start the command **apropos shell > shell-commands** in the foreground, suspend it, and then specify that it finish in the background, you would type:

```
$ apropos shell > shell-commands RET
C-z
```
```
[1]+  Stopped
apropos shell > shell-commands
$ bg RET
[1]+ apropos shell > shell-commands &
$
```

If you have suspended multiple jobs, specify the job to be put in the background by giving its job number as an argument.

- To run job 4 in the background, type:

```
$ bg %4 RET
```

> NOTE: Running a job in the background is sometimes called "backgrounding" or "amping off" a job.

## 4.3.3 Putting a Job in the Foreground

Type fg to move a background job to the foreground. By default, fg works on the most recent background job.

- To bring the most recent background job to the foreground, type:

```
$ fg RET
```

To move a specific job to the foreground when you have multiple jobs in the background, specify the job number as an option to fg.

- To bring job 3 to the foreground, type:

```
$ fg %3 RET
```

## 4.3.4 Listing Your Jobs

To list the jobs running in the current shell, type jobs.

- To list your jobs, type:

```
$ jobs RET
[1]- Stopped          apropos shell > shell-commands
[2]+ Stopped          apropos bash > bash-commands
$
```

This example shows two jobs—apropos shell > shell-commands and apropos bash > bash-commands. The `+` character next to a job number indicates that it's the most recent job, and the `-` character indicates that it's the job previous to the most recent job. If you have no current jobs, jobs returns nothing.

To list all of the processes you have running on the system, use ps instead of jobs—see Listing System Activity.

## 4.3.5 Stopping a Job

Typing C-C interrupts the foreground job before it completes, exiting the program.

- To interrupt cat, a job running in the foreground, type:

```
$ cat RET
C-c RET
$
```

Use kill to interrupt ("kill") a background job, specifying the job number as an argument.

- To kill job number 2, type:

```
$ kill %2 RET
```

## 4.4 Command History

Your command history is the sequential list of commands you have typed, in the current or previous shell sessions. The commands in this history list are called events.

## The Linux Cookbook: Tips and Techniques for Everyday Use:

By default, `bash` remembers the last 500 events, but this number is configurable (see section [Customizing Future Shells](#)).

Your command history is stored in a text file in your home directory called `.bash_history`; you can view this file or edit it like you would any other text file.

Two very useful things that having a command history lets you do is to repeat the last command you typed, and (as explained earlier in this chapter) to do an incremental backwards search through your history.

The following sections explain how to view your history and specify events from it on the command line. See Info file `bashref.info`, node `Bash History Facilities`, for more information on command history.

- [4.4.1 Viewing Your Command History](#) — Viewing the history of what you typed.
- [4.4.2 Specifying a Command from Your History](#) — Substituting a command from your history.

[<](#) [>](#) [<<](#) [Up](#) [>>](#) [Top](#) [Contents](#) [Index](#) [?](#)

### 4.4.1 Viewing Your Command History

Use `history` to view your command history.

- To view your command history, type:

```
$ history RET
1 who
2 apropos shell > shell-commands
3 apropos bash > bash-commands
4 history
$
```

This command shows the contents of your command history file, listing one command per line prefaced by its *event number*. Use an event number to specify that event in your history (see section [Specifying a Command from Your History](#)).

If your history is a long one, this list will scroll off the screen, in which case you may want to pipe the output to `less` in order to peruse it. It's also common to search for a past command by piping the output to `grep` (see section [Redirecting Output to Another Command's Input](#) and [Searching for a Word or Phrase](#)).

- To search your history for the text `apropos`, type:

```
$ history | grep apropos RET
```
