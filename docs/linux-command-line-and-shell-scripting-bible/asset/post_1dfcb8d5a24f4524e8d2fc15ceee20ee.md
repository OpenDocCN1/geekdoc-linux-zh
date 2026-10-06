
# Part II Shell Scripting Basics

The bash shell runs the .bash_profile file when a new shell is run as a result of a new login. Place any scripts that you want to run at login time in this file.

The bash shell runs the .bashrc any time a new shell is started, including when a new login occurs. You can test this by adding a simple echo statement to the .bashrc file in your home directory, then starting a new shell:

```
$ bash
This is a new shell!
$ 
```

If you want to run a script for every user on the system, most Linux distributions provide the /etc/bashrc file (note that there is no period in front of the bashrc filename). The bash shell executes the statements in this file every time you run on the system starts a bash shell.

# Summary

The Linux system allows you to control your scripts by using signals. The bash shell accepts signals, and passes them to any process running under the shell process. Linux signals allow you to easily kill a runaway process or temporarily pause a long-running process.

You can use the trap statement in your scripts to catch signals and perform commands. This feature provides a simple way to check whether a user can interrupt your script while it is.

By default, when you run a script in a terminal session, the interactive shell is suspended until the script completes. You can cause a script or command to run in background mode by adding an ampersand (&) after the command name. When you run a script or command in background mode, the interactive shell returns, allowing you to continue entering more commands. Any background processes run using this method are still tied to the terminal session. If you exit the terminal session, the background processes also exit.

To prevent this from happening, use the nohup command. This command intercepts signals intended for the command that would stop it, for example, when you exit the terminal session. This allows scripts to continue running in background mode even if you exit the terminal.

When you move a process to background mode, you can still control what happens to it. The jobs command allows you to view processes started from the shell session. Once you know the job ID of a background process, you can use the kill command to send Linux signals to the process, or use the fg command to bring the process back to the foreground in the shell session. You can suspend a running process by using the Ctrl-Z key combination, then place it back in background mode using the bg command.

The nice and renice commands allow you to change the priority level of a process. By giving a lower priority, you allow the CPU to allocate less time to it. This comes in when running long processes that take lots of CPU time.

Besides controlling processes while they're running, you can also determine when a process starts on the system. Instead of running a script directly from the command line prompt, you can schedule the process to run at an alternative time. There are several different ways to accomplish this. The at and batch commands allow you to run a script once at a preset time. The cron program provides an interface that can run scripts at a regularly scheduled interval.

Finally, the Linux system provides script files for you to use for scheduling your scripts to run either at system boot time or whenever a user starts a new bash shell. The .rc.local (or boot.local for openSUSE) file allows you to list scripts that start each time the system boots. This system allows administrators to run special scripts for system maintenance at boot time. Similarly, the .bash_profile and .bashrc files are located in every user's home directory to provide a location to place scripts and commands that run with a new shell. The .bash_profile runs scripts each time a user logs in to the system, and the .bashrc file runs scripts on each new instance.

In the next chapter, we'll look at how to write script functions. Script functions allow you to write code blocks once, then use them in multiple locations throughout your script.

# Part III

# Advanced Shell Scripting

| IN THIS PART |
| --- |
| Chapter 14 Creating Functions |
| Chapter 15 Adding Color to Scripts |
| Chapter 16 Introducing sed and gawk |
| Chapter 17 Regular Expressions |
| Chapter 18 Advanced sed |
| Chapter 19 Advanced gawk |

# Chapter 14

## Creating Functions

Often while writing shell scripts you'll find yourself using the same code in multiple locations. If it's just a small code snippet, it's usually not that big of a deal. However, if you're rewriting large chunks of code multiple times in your shell script, that can get tiring. The bash shell provides a way to help you out by supporting user-defined functions. You can encapsulate your shell script code into a function, which you can then use as many times as you want anywhere in your script. This chapter walks you through the process of creating your own shell functions, and demonstrates how to use them in other shell script applications.

| IN THIS CHAPTER |
| --- |
| Creating a function |
| Using parameters |
| Sharing functions |

## Basic Script Functions

As you start writing more complex shell scripts, you'll find yourself reusing parts of code that perform simple tasks. Sometimes it's something simple, such as displaying a text message and retrieving an answer from the script users. Other times it's a complicated calculation that's used multiple times in your script as part of a larger process.

In each of these situations, it can get tiresome writing the same blocks of code over and again in your script. It would be nice to write the block of code once, then be able to refer to it.

## Creating a function

There are two formats you can use to create functions. The first format uses the keyword function, along with the name:

```
function name {
  commands
}
```

The second format for defining a function more closely follows how functions are defined in other languages:

```
name() {
  commands
}
```

The empty parentheses after the function name indicate that you are defining a function.

## Using functions

To use a function in your script, specify the function name on a line, just as you would any other command:

```
$ cat test1
!/bin/bash
# using a function in a script
```

```
function func1 {
  echo "This is an example of a function"
}

count=1
while [ $count -le 5 ];
do
  func1
  count=$[$count + 1 ]
done
```
