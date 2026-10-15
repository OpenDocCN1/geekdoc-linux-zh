
# EXPLANATION (CONTINUED)

+   3 The DONE terminator marks the end of the here document. The DONE cannot have space on either side of it. The terminator replaces typing Ctrl-D. The sort command will not receive further input. When finished, sort will send its output to the screen.
+   4 The output from the sort program is displayed.
+   5 The shell prompt reappears.

If the terminator is preceded by the << operator, leading tabs, and only tabs, may precede the final terminator. The user-defined terminating word or symbol must match exactly from "here" to "here". The following examples illustrate the use of the here document at the command line to demonstrate the syntax. It is much more practical to use them in scripts.

## EXAMPLE 7.43

```
1 $ cat << FINISH        # FINISH is a user-defined terminator
2 > Hello there $LOGNAME
3 > The time is `date`
> I can't wait to see you!!!
4 > FINISH                # terminator matches first FINISH on line 1.
5 Hello there ellie
The time is Wed April 22 19:42:16 PST 2004
I can't wait to see you!!!
6 $
```

## EXPLANATION

+   1 The UNIX cat program will accept input until the word FINISH appears on a line by itself.
+   2 A secondary prompt appears. The following text is input for the cat command. Variable substitution is performed within the here document.
+   3 Command substitution, `date`, is performed within the here document.
+   4 The user-defined terminator FINISH marks the end of input for the cat program. It cannot have any spaces before or after it and is on a line by itself.
+   5 The output from the cat program is displayed.
+   6 The shell prompt reappears.

## EXAMPLE 7.44

```
1 $ cat << DONE
> Hello there
> what's up?
> Bye now The time is `date`.
2 > DONE
Hello there
what's up?
Bye now The time is Thu Oct 28 19:48:23 PST 2004.
$
```

## EXPLANATION

+   1. The cat program accepts input until DONE appears on a line by itself. The << operator allows the input and final terminator to be preceded by one or more tabs.
+   2. The final matching terminator, DONE, is preceded by a tab. The output of the cat program is displayed on the screen.

### 7.12.1 Now What?

Now that we have completed our discussion on the interactive shell, it is time to combine many of these features in scripts, to produce programs that will automate repetitive tasks, produce information, monitor processes, and so on. If you are not a programmer, writing shell scripts may be a good place for you to start. It's fun and you get results quickly.

# chapter

# 8

# Programming the Bourne Shell

![](img/60a0b5d254bd6007403850f972cbfad8_358_0.png)

## 8.1 Introduction

Shell programs are usually called shell scripts. Now that you have learned how to use the shell interactively, you are ready to start scripting using what you have learned in addition to the programming constructs provided in this chapter. It doesn't matter whether you are a system administrator, a programmer, or a user. Shell scripts can automate a number of routine tasks to make life a lot easier—and they are fun to write and use!

### 8.1.1 The Steps in Creating a Shell Script

A shell script is normally written in an editor and consists of commands interspersed with comments. Comments are preceded by a pound sign (#) and consist of text used to document what is going on.

# The First Line.

The first line at the top left corner of the script will indicate the program that will be executing the lines in the script. This line, known as the shbang line, is commonly written as

```
#!/bin/sh
```

The #! is called a magic number and is used by the kernel to identify the program that should be interpreting the lines in the script. This line must be the top line of your script.

# Comments.

Comments are lines preceded by a pound sign and can be on a line by themselves or on a line following a script command. They are used to document your script. It is sometimes difficult to understand what the script is supposed to do if it is not commented. Although comments are important, they are often too sparse or not used at all. Try to get used to commenting what you are doing not only for someone else, but also for yourself. Two days from now you may not recall exactly what you were trying to do.
