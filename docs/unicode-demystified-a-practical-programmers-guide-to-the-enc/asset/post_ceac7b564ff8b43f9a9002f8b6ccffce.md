
about each background job: its job number in brackets followed by the PID of the
last process in the job.
Using job control, you can move commands from the foreground to the back-
and versa, stop commands temporarily, and get a list of the commands
that are currently running or stopped.

## jobs: Lists Jobs

The built builtin jobs lists all background jobs. The following sequence demonstrates
what happens when you give the command jobs from the Bourne Again Shell. In the
following example the sleep command run in the background creates a background
job that can report on, and jobs builtin displays job information:

```
$ sleep 60 &
[1] 7809
$ jobs
[1] + Running      sleep 60&
```

## fg: Brings a Job to the Foreground

The shell assigns a job number to commands that you run in the background
(page 548). In the following example several jobs are started in the background. For
each the Shell lists the job number and PID number immediately, just before it assigns
a prompt.

```
$ xmas &
[1] 1246
$ date &
[2] 1247
$ Sun Dec 7 11:44:40 PST 2003
[2]+ Done
date
$ find /usr -name ace -print > findout &
[2] 1269
$ jobs
[1]- Running      xman &
[2]+ Running      find /usr -name ace -print > findout
```

The command lists the first job, xman, as job 1. The date command does not
appear in the jobs list because it completed before find was run.
command completed before find was run, the find command became job 2.

- 1. Job numbers are discarded when a job is finished and can be reused. When you start or put a job in the
background, the shell assigns the lowest number that is not in use and is not less than a job number
that is currently in use.

To move a background job into the foreground, use the fg builtin with a percent sign (%) followed by the job number as an argument. The following example moves job 2 into the foreground:

```
$ fg %2
```

You can also refer to a job by following the percent sign with a string that uniquely identifies the beginning of the command line to start the job. Instead of the preceding command, for example, you could have used fg %find or fg %f, because either one uniquely identifies job 2. If you follow the percent sign with a question mark and a string, the string matches itself over the command line. In the preceding example, %?ace also refers to job 2.

Often the job you wish to bring into the foreground is the only job running in the background or is the job that jobs lists with a plus (+). In these cases you can use fg without any arguments.

## bg: Sends a Job to the Background

To put the foreground job into the background, you must first suspend the job by pressing the suspend key (usually CONTROL-z). Pressing the suspend key stops the job immediately. Once the job is suspended, use the bg builtin to resume execution of the job, putting it in the background:

```
$ bg
```

If a background job attempts to read from the terminal, the shell stops it (puts it to sleep [pages 142 and 562]) and notifies you that the job has been stopped and is waiting for input. When this happens, you must move the job into the foreground so that it can read from the terminal. The shell displays the command line as it moves the job into the foreground:

```
$ sleep 5; cat > mytext &
[1] 1343
$ date
Sun Dec 7 11:58:20 PST 2003
[1]+ Stopped (tty input) ( sleep 5; cat >mytext )
$ fg
( sleep 5; cat >mytext
Remember to let the cat out!
CONTROL-D
```

In this example, the shell displays the job number and PID number of the background job as soon as it starts, followed by a prompt. This point user enters date, and its output appears on the screen. The shell waits until just it issues a prompt (after date has finished) to notify you that job 1 is waiting for input. The reason for this delay is so that the notice does not disrupt your work: the default
behavior of the shell. After the shell puts the job in the foreground, you can enter
input that the command was waiting for. Terminate the input with a CONTROL-D
signify EOF (end of file), and the shell displays another prompt.

The shell keeps you informed about changes in the status of a job, notifying you
a background job starts, completes, or is waiting for input from the terminal.
The shell also lets you know when a foreground job is suspended. Because notices
about a job being in the background can disrupt your work, the shell delays
notices until it is ready to display a prompt.

If you try to leave a shell while jobs are stopped, the shell gives you a warning
and does not allow you to exit. If, after the warning, you use jobs to review the list
of jobs or you immediately try to leave the shell again, the shell allows you to leave
and terminates your stopped jobs. Jobs that are running (not stopped) in the-
continue to run. In the following example, find job (1) continues to run after
the second exit terminates the shell, but cat job (2) is terminated:

```
$ find /-size +100k $HOME/bigfiles 2>&1
[1] 1426
$ cat mytestest &
[2] 1428
$ exit
```

There are stopped jobs.

[2]+ Stopped (tty input) cat > mytext
$ exit

login:

## Manipulating the Directory Stack

Using a shell you can store a list of directories you are working with, enabling
to move them easily among. The list is referred to as a stack. You can think of it
as a stack of dinner plates; you typically add plates and remove plates from the
top of the stack: a first-in-last-out, or FILO, stack.

## dirs: Displays the Stack

The dirs builtin displays the contents of the directory stack. If you call dirs when
the directory stack is empty, it displays the name of the working directory:

```
$ dirs
~/literature
```

558 Chapter 12 The Shell II: The Bourne Again Shell

![](img/aa8214d49e1cf50152c432845129fb3b_607_0.png)

## Figure 12-2 The directory structure in the examples

The dirs builtin uses a tilde (~) to represent the name of the user's home directory. The examples in the next several sections assume that you are referring to the directory structure shown in Figure 12-2.

## pushd: Pushes a Directory on the Stack

To change directories and at the same time add a new directory to the top of the stack, use the pushd (push directory) builtin In addition to changing directories, the pushd builtin displays the contents of the stack. The following example is illustrated in Figure 12-3:

```
$ pushd ../demo
~demo ~/literature
$ pwd
/home/scott/names
$ pushd ../demo ~/names
~names ~/demo ~/literature
$pwd
/home/scott/names
```

![](img/aa8214d49e1cf50152c432845129fb3b_607_1.png)

## Figure 12-3 Creating a directory stack

## Manipulating the Directory Stack

![](img/aa8214d49e1cf50152c432845129fb3b_608_0.png)

**Figure 12-4 Using pushd to change directories**

When you use pushd without an argument, it swaps the top directories and makes the new top directory (which was the second directory) the new working directory (Figure 12-4):

```
$ pushd
~/demo ~/names
```

Using pushd in this way, you can easily move back and forth between two directories. To access another directory in the stack, call pushd with a numeric argument. The directories in the stack are numbered starting with the top directory, which is 0.

```
$ pushd +2
~/literature ~/demo
$pwd
/home/scott/literature
```

## popd: Pops a Directory off the Stack

To remove a directory from the stack, use the popd (pop directory) built-in Figure 12-5 shows, without an argument popd removes the top directory from the stack and changes the working directory to the new top directory:

```
$ popd
~/demo ~/names
$pwd
/home/scott/demo
```

To remove a directory other than directory number 0 on the stack, this command does not change the working directory.

```
$ popd +1
~/demo
$pwd
/home/scott/demo
```

## Processes

A process is the execution of a command by GNU/Linux. The shell that starts up when you log in is a command, or a process, like any other. Whenever you give the name of a GNU/Linux utility on the command line, you initiate a process. Whenever you run a shell script, another shell process is started, and additional processes are created for each command in the script. Depending on how you invoke the shell script, the script is run either by a new shell or a subshell of the current shell. A process is not started when you run a shell builtin, as cd from the command line or within a script.

## Process Structure

The file structure, the process structure is hierarchical, with parents, children, and even a root. A parent process forks a child process, which in turn can fork other processes. (You can also use the term spawn; the words are interchangeable.) The operating system routine, or system call, that creates a new process is named fork. One of the first things GNU/Linux does to begin when a machine is started up is init, a single process, called a spontaneous process, with PID number 1. This process holds the same position in the process structure as the root directory in the file structure: It is the ancestor of all processes that each

- The term fork is used to convey that, as with a fork in the road, one process turns into two. Initially the two forks are identical except that one is identified as the parent and one as the child.

![](img/aa8214d49e1cf50152c432845129fb3b_609_0.png)
