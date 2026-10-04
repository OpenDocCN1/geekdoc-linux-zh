
bolting the two commands together via the temporary file so that they work as one. This is such a common thing to want to do that Linux provides a facility, which the shell takes advantage of, to connect the two programs together directly without the need for, or use of, a temporary file. This facility is called a pipe.

A pipe uses the | redirection operator. Rewriting the previous example to use a pipe gives:

```
$ ls /usr/bin | wc -w
459
```

As Linux is a multi-tasking operating system, this command line (or pipeline as it is called) will be executed by running the two commands ls and wc concurrently, so that the output from ls can be read by wc as it is produced.

A pipeline is not just limited to two commands bolted together. Any number of commands can be joined together, with a pipe operator being used to connect each adjacent pair. With this arrangement, the output from the first command will become the input to the second. The output from the second becomes the input to the third, and so on.

## 4.4 Background Jobs

In all of the command line examples so far, once you have typed in a command and pressed Enter or Return the system seems to go away to perform your command. When your command has finished, the shell finally returns a prompt to you as an invitation to enter another command. Figure 4.1 shows why this is so.

As you can see, once the shell has started a new process and set your command running, it then puts itself to sleep to wait for your command to finish. Only when this has happened is a signal sent back to the shell to wake it up so that it can give you a prompt and look for your next command.

Because Linux is multi-tasking, there is no reason why the shell shouldn't be able to run at the same time as your command and hence return a prompt to you immediately, while your command gets on with its task (see Figure 4.2). This is very useful if, for instance, the command you run will take a long time to complete its task, as it allows you to get on with something else.

The decision as to whether the shell will wait for a command to finish, or return to you immediately with a prompt, is made by you when you run the command. All you do is to put an ampersand character (&) at the end of your command line if you do not want the shell to wait but, rather, to return a prompt straight away. This is called putting the command into the background:

```
$ ls -lR / > /tmp/ls.lR &
[1] 341
$
```

![](img/ad36c2db45661d7b3b68db09c8eea0a1_73_0.png)

### Figure 4.1 The shell waits for a command to finish.

Here the output from an ls command is being written to the file /tmp/ls.lR and, rather than wait while this happens, the command has been run in the background with the & character on the end of the command line. The -R option to ls produces a recursive directory listing that works its way down through all the subdirectories that can be reached from the starting point (/ here). It means that this command produces a sorted long listing of the entire directory hierarchy of the machine – quite a lengthy task. The numbers printed on the line after the command are displayed by the shell. The number in square brackets is the job number for this command line. This is described in Section 4.5. The second number is the PID for the command being executed, or the PID for the last command on the line, if there is a pipeline involved.

In general, commands that you run in the background, must not try to take any input from the keyboard because all the keyboard input will go to the shell, after it gives you a prompt. The default for any background commands that do try to take keyboard input is that their execution is stopped and all their activity is suspended.

![](img/ad36c2db45661d7b3b68db09c8eea0a1_74_0.png)

### Figure 4.2 Executing a background job.

## 4.5 Job Control

Every time you execute a command with bash a job number is allocated to it. For the purposes of this allocation, multiple commands connected together in a pipeline all count as one job which will share a single job number. The shell uses these job numbers as the basis for its job control.

Job control allows you to suspend and subsequently resume the execution of processes at a later time. The shell maintains a list of currently executing jobs which can be displayed with the jobs command. In order to suspend the current foreground job you just press the key sequence Ctrl-z on the keyboard. When you do this, the job will stop running and a shell prompt will be returned, as in the following example:

```
$ cat >text.file
Ctrl-z
[1]+ Stopped              cat >text.file
$ jobs
```

```
[1]+ Stopped                cat >text.file
```

The Ctrl-z in the above command sequence indicates that you should press Ctrl-z at this point, which will suspend the currently executing cat command. The use of the jobs command then shows this job in the shell's list along with its job number and its current status.

When you come to resume execution of this process, you have two choices: you can either start it back in the foreground with the fg command, in which case it will continue from where it left off, or you can push it into the background with the bg command, in which case it will run as though you had initially run the command with an & operator on the end of the line.

In this particular case, you should remember that the cat command has been started in a mode where it is taking its input from the keyboard. This means that if you resume the command in the background it will immediately perform an illegal read from the keyboard and be suspended again, automatically this time, by the system:

```
$ bg
[1]+ cat >text.file &
$ jobs
[1]+ Stopped (tty input)    cat >text.file
```

The fg and bg commands operate, by default, on the most recently stopped job. When you use the jobs command, this default job will be identified by the + symbol immediately following its job number in the shell's output. In general, if you want to refer to any job in the list, not just the default job, you can do this by giving its job number after a percent (%) symbol:

```
$ fg %1
cat >text.file
```

This fg command will restart the cat job back in the foreground so that any subsequent keyboard input (up to Ctrl-d) will be written to the file text.file.

Rather than resume a stopped job, you may just wish to terminate the job altogether. This can be done with the kill command:

```
$ cat >text.file
Ctrl-z
[1]+ Stopped                cat >text.file
$ jobs
[1]+ Stopped                cat >text.file
$ kill %1
[1]+ Terminated             cat >text.file
```

If you try to logout of the system while you have any stopped jobs, you will receive a warning error message and the command will fail:

```
$ cat >text.file
Ctrl-z
$ logout
There are stopped jobs.
```

At this point you can either deal with the stopped jobs or, if you logout again immediately, the jobs will automatically be terminated and the logout will be successful.

## 4.6 History

As you work under Linux, you will often find that you are repeatedly executing the same small sequence of commands. For example, during program development and debugging you will often iterate around the standard loop: edit the source code, compile the source into an executable file, run the executable file to test its performance and then round again to the start. In order to save you repeatedly having to retype the same commands, bash stores your commands as you type them so that you can easily return to them again if you wish. The store that bash uses for this purpose is called the history list and, by default, this list can store the last 500 command lines you have entered.

A history list this size can quite literally represent all the commands entered during many days of work. In order for it to make sense to use a history list of this size, bash automatically arranges to save the current list to a file when you logout. The default file name bash uses is .bash_history, which it stores in your home directory. Notice that the dot at the start of the file name means that the file will not be listed by ls unless the -a command line switch is used. When you login at the start of the next session, the shell will automatically load the contents of the history file into its history list, effectively allowing you to continue on from where you left off at the end of the previous session.

In order to see the stored list of previously entered lines, you use the history command. Remember that the list is up to 500 lines long so you may want to pipe the output of the history command into more or tail:

```
$ history | tail -5
511  cat >text.file
512  cd ..
513  ls -al
514  cd book
515  history | tail -5
```

The lines in the history list are each called events and the numbers along side each line are called event numbers. Once you know the event number for the line you want to repeat, it is a simple matter to execute it. Suppose you wanted to
