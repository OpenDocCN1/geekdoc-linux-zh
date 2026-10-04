# Shell Scripts

You have seen that bash has a very powerful set of interactive facilities available from the keyboard in the form of I/O redirection, pipes, job control, history lists, command line editing, and so on. In this chapter you will see that this is only half of the story. The shell goes on to provide a full programming language interpreter and a mechanism for reading and executing your own shell programs. These shell programs are called *Shell Scripts.*

# 6.1 Command Files

Any standard Linux command or pipeline, or any sequence of these things, can be entered into a text file with cat or with an editor like vi, made executable with chmod and then executed just by entering its name, like any other system command.

The following command sequence shows this idea in action:

```
$ cat >dirsize
ls /usr/bin | wc -w
Ctrl-d
$ chmod 700 dirsize
$ ls -l dirsize
-rwx------ 1 pc book 20 Jun 10 22:04 dirsize
$ dirsize
459
```

Here, the pipeline ls /usr/bin | wc -w is entered into the text file dirsize. This file is then flagged as executable, with the command chmod 700 dirsize. The following ls command now allows you to check that the file's permission flags have been set as required. Finally, using the filename (dirsize) as a command name causes the pipeline in the file to be executed by a shell, just as though it had been entered from the command line. The output (459) is the count of the number of files in the directory specified in the shell script.