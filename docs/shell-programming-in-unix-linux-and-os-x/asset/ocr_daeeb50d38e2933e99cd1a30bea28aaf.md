# And Away We Go

Based on our discussions in Chapter 2, “What Is the Shell?,” you should now realize that whenever you type something like

who | wc -1

you are actually programming in the shell. That's because the shell is interpreting the command line, recognizing the pipe symbol, connecting the output of the first command to the input of the second, and initiating execution of all commands.

In this chapter, you'll learn how to write your commands and how to use shell variables.

# Command Files

A shell program can be typed directly, as in

```
$ who | wc -1
```

or it can be typed into a file and the file can be executed by the shell. For example, suppose that you need to find out the number of logged-in users several times throughout the day. It's not unreasonable to type it in the preceding pipeline each time you want the information, but for the sake of example, let's type this pipeline into a file.

We'll call the file nu (for number of users), and its contents will be the pipeline shown previously:

```
$ cat nu
who | wc -1
```

To execute the commands contained inside the file nu, all you now have to do is type nu as the command name to the shell:

```
$ nu
sh: nu: cannot execute
$
```