```
$ cat >text.file
Ctrl-z
$ logout
There are stopped jobs.
```

At this point you can either deal with the stopped jobs or, if you logout again immediately, the jobs will automatically be terminated and the logout will be successful.

# 4.6 History

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