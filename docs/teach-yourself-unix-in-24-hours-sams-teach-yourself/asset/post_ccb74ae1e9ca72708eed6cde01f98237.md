
This script is intended to be part of a pipeline, and it will send a copy of the stream of information either to the default address (SENDTO) or to a specified person ($1 is the first argument given to the script in this case). As shown earlier in the discussion of system prompts, any text that appears in backquotes is interpreted as a command and is executed, and the results of that command are added in its place in the subsequent command. In this case, the echo command on line 19 computes the number of lines in the specified file, and then the number is included in the output, which typically looks like this: Punted a 17 line news article.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_351_0.png)

JUST A MINUTE

The very first character of this file is a colon. It turns out that the C shell interprets scripts only if the very first character of the script is a #. Otherwise, it lets the Bourne shell (sh) run the commands, in this case.

- 3. That's all and interesting, but I want to create a new script. The first step is to make sure I'm creating the script in a directory that is included in my search path (otherwise, I won't be able to use the script as a command):
Limbo (bin) 46 : pwd
/users/taylor/bin
Limbo (bin) 47 : echo $PATH
:/users/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local:/usr/etc:/usr/locate/bin:/usr/unip/bin (bin) 48 :

Here's a very simple shell script that shows how shell scripts can be for assistance:
Limbo (bin) 86 : cat new.script
# sample shell script

echo searching for shell scripts
pwd
echo

```bash
ls -F | grep script | sed 's/:/ /' | awk '{print $1}'
exit 0
```

This script lists the names of all files in the current directory that it identifies as shell scripts:
Limbo (bin) 88 : chmod +x new.script
Limbo (bin) 89 : ./new.script
searching for shell scripts
/users/taylor/bin

bounce.msg
locate
new.script
punt
rumor.mill.sh

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_351_1.png)

# Getting the Most Out of the C Shell

To confirm that the new command works, look at what file reports about this same directory:

```bash
Limbo (bin) 90 : file *
bounce_msg: executable shell script
calc: SYMMETRY i386 executable (0 @0) not stripped version 1
fixit: SYMMETRY i386 executable (0 @0) not stripped version 1
locate: shell script
massage: SYMMETRY i386 executable (0 @0) not stripped version 1
new.script: commands text
punt: shell script
rumor_all: shell script
hay: assist text
Limbo (bin) 91 :
```

- 4. A more interesting script is one that can search through all the directories in my PATH, looking for any occurrences of a specified filename:
Limbo (bin) 92 : cat locate
# locate - find copies of a file
# this should be run by the C Shell

```bash
set name=$1

foreach directory (`echo $PATH | sed 's/:/ /g')
if [ -f $directory/$name ] then
ls -l $directory/$name
endif
end
```

The loop is evaluated from the inside out. Because of the backquotes, my PATH is echoed to sed, which removes the colons separating the directories. Then the C shell goes through the loop once for each directory in PATH, setting the variable directory to the existence of the subsequent value. Each time through the loop, the -f test checks for the existence of the file: in that directory, -l lists some information about it.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_352_0.png)

> Pay careful attention to the backquotes and single quotes in this script.

JUST A MINUTE

Here is locate at work:

```bash
Limbo (bin) 93 : locate ls
-rwxr-xr-x 1 root 32768 May 29 1990 /bin/ls*
Limbo (bin) 94 : locate vi
-rwxr-xr-t 7 root 16384 Nov 29 1990 /usr/ucb/vi* evenLimbo (bin) 95 :
```

# Summary

It would really take an entire book (or two) to describe fully all the ins and outs of shell scripts. The main idea here, however, is that you use a lot of commands repetitively, you should make them into a command alias (if they're short) or drop them all into a shell script. In shell scripts, as in awk, $1 is the first argument, $2 the second, and so on.

This hour introduced you to many of the most powerful aspects of UNIX shells. Practice creating aliases and working with the history list to minimize your typing. Also, find a prompt you like and set it in your .cshrc or .profile (for csh and ksh, respectively) so it will be the default.

# Workshop

The Workshop summarizes the key terms you learned and poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

**basename** The closest directory name. For example, the basename of /usr/home/taylor is taylor.

**command number** The unique number by which the shell indexes all commands. You can place this number in your prompt using ! and use it with the history mechanism as command-number.

# Questions

- 1. How do you tell the C shell that you want it to remember the last 30 commands during a session and to remember the last 10 commands across login sessions?
2. Assume that you get the following output from entering history:
```
1 ls -CF
2 who | grep dunalim
3 wc -l test
4 cat test
5 history
```
What would be the result of entering each of the following history commands?
```
!2
!1
!!
```
3. Some UNIX systems won't enable you to do the following. What do you see?
```
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_353_0.png)

# Getting the Most Out of the C Shell

- 4. Which of the following aliases do you think would be useful?
alias leaning
alias cp
alias vi
- 5. Set your prompt to the following:
alias color
- 6. Find and examine the following:
```bash
```

# Preview of the Next Hour

In the next hour, you learn how to get even more out of.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_354_0.png)

# Hour 16

# Basic Shell Programming

In the previous hour, you learned a few options available to you. For example, remember any line beginning with # is a comment.

# Goals for This Hour

- Shell variables
- Shell arithmetic
- Conditional expressions
- Looping expressions

# Hour 16

Because shells are just interpreted languages, the Bourne shell is slightly different. Because I'm using the C shell, the prompt is different.

Earlier in the book, I illustrated examples using the C shell because that is standard on every platform.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_356_0.png)

JUST A MINUTE

| I strongly urge you to look at the shells you have. The best shell is to use the one that makes you most |

# Task 16.1: Shell Variables

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_356_1.png)

Programming languages usually include variables, and the shell naturally does, too. Variables are tags to identify values that may change as a program is used. In the shell, these variables can take a single value and are always interpreted as strings. Even numeric values are strings to the shell.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_356_2.png)

JUST A MINUTE

| The C shell and Korn shell both support arrays and have means of representing numeric values. |

You can use any string-manipulation command, such as sed or cut, to change a shell variable.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_356_3.png)

Here is an example of setting the value of a shell variable:

```bash
$ color=blue
```

This sets the variable color to the string blue. One can output the value of any variable with the echo command:

```bash
$ echo $color
blue
```

This also indicates how to reference a shell variable: It must be preceded by the dollar sign ($). This can cause some problems. If you are using a shell variable as a prefix and want to immediately append text, you might think this would work:

```bash
$ leaning="anti-"
$ echo Joe is basically $leaningtaxes
```
