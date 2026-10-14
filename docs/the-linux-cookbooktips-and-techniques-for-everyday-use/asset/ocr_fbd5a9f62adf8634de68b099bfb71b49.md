[1]+  Stopped                  info -f cookbook.info

In this example, the job number is 1 and the command that has stopped is `info -f cookbook.info`. The `+` character next to the job number indicates that this is the most recent job.

If you have any stopped jobs when you log out, the shell will tell you this instead of logging you out:

```
```text
$ logout RET
There are stopped jobs.
$
```
```

At this point you can list your jobs (see section [Listing Your Jobs]), stop any jobs you have running (see section [Stopping a Job]), and then log out.

# 4.3.2 Putting a Job in the Background

New jobs run in the foreground unless you specify otherwise. To run a job in the background, end the input line with an ampersand (`&`). This is useful for running non-interactive programs that perform a lot of calculations.

+   - To run the command **apropos shell > shell-commands** as a background job, type:

```
```text
$ apropos shell 62; shell-commands 38; RET
[1] 6575
$
```
```

The shell outputs the job number (in this case, 1) and process ID (in this case, 6575), and then returns to a shell prompt. When the background job finishes, the shell will list the job number, the command, and then the text `Done`, indicating that the job has completed successfully:

```
```text
[1]+  Done                  apropos shell 62;shell-commands
```
```

To move a job from the foreground to the background, first suspend it (see section [Suspending a Job]) and then type **bg** (for "background").

+   - For example, to start the command **apropos shell > shell-commands** in the foreground, suspend it, and then specify that it finish in the background, you would type:

```
```text
$ apropos shell 62; shell-commands RET
C-z
```
```