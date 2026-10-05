# Chapter 10: Avoiding Shell Shock 181

through all the files to see whether any accounts have been added or deleted. As you follow along in the chapter, this is exactly what you will be doing.

# Passing information to your shell

The shell program can get several pieces of information from the arguments you use when you invoke the shell. To illustrate the presence of arguments on the command line and the capability of the shell to access them, use a text editor to create a small, simple shell called stuff, and put it in the bin directory of your login account. (Remember to change the shell's mode to be executable by you, the owner).

```
maddog@localhost:~/reports > cat ~/stuff
echo The zeroth argument $0
echo The first argument $1
echo The second argument $2
echo The third argument $3
echo The fourth argument $4
echo The number of expanded arguments $$\$
<CTRL+>
```

```
maddog@localhost:~/reports > chmod u+x ~/stuff
```

That should be enough to put into the shell. Each line that ends with either a number or the character #, preceded by a dollar sign. These are special names inside the shell that will have values assigned to them according to what you type on the command line as a command name and argument you invoke the shell.

You should still be in the reports directory, but just to make sure that you are, change directories to your reports directory. Then execute the shell script that you created:

```
maddog@localhost:~ > cd ~/reports
maddog@localhost:~/reports > stuff
The zeroth argument /home/maddog/bin/stuff
The first argument
The second argument
The third argument
The fourth argument
The number of expanded arguments 0
maddog@localhost:~/reports >
```

Note that the zeroth argument (called $\$0) is the full pathname for the executed shell command. When executing the command name by itself on the line with no additional arguments or options, the zeroth argument is the only argument that receives information.

![](bbox=[0.025, 0.865, 0.135, 0.965])