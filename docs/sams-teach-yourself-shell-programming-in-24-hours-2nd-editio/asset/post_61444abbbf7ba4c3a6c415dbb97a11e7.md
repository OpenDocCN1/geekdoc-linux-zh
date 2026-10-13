
The two main changes to the function are

- A case statement sets the variable PSOPTS based on the operating system name.
- The STDERR of ps is redirected to /dev/null in order to discard the warning message generated on older versions of Linux.

## Linux ps
In Linux the ps command varies between different versions. In older versions of Linux 2.0, the hyphen in the -auxx command is not properly supported, whereas in current versions the hyphen is supported, as are the System V style -ef options. Taking this into account, you could modify the getPID() function as follows:

```
getPID() {
  if [ $# -lt 1 ]; then
    echo "ERROR: Insufficient Arguments." >&2
    return 1
  fi

  PSOPTS="-ef"
  case `getOSName` in
    bsd|sunOS|darwin)
      PSOPTS="-auxx" ;;
    linux)
      case `uname -r` in
        [01].*) PSOPTS="-auxx" ;;
        2.0*) PSOPTS="-auxx" ;;
      esac
      ;;
  esac

  `/bin/ps $PSOPTS | grep "$1" |`
  awk '/grep/ { next; } { print $2; }'
}
```

This version avoids having to redirect to /dev/null and allows you to detect any problems that might be reported by the ps command.

## Summary
In this chapter, you learned how to determine which version of UNIX is running using uname. In addition, you developed the getOSName and isNS? functions to help adapt shell scripts to multiple versions of UNIX. You also looked at the following techniques for improving the portability of shell scripts:

- Conditional execution
- Abstraction

In conditional execution, the flow of a script was modified depending on the version of UNIX being used. In abstraction, function implementations were altered to account for the differences between versions of UNIX; the overall flow of the script remained the same.

Using the techniques and tips in this chapter, you can port shell scripts across different versions of UNIX.

## Question
- 1. Write a function called getCharCount that prints the number of characters in a file. Use wc to obtain the character count. Linux, FreeBSD, and SunOS (not Solaris), use the -c option for wc, whereas other versions of UNIX use the -m option. Feel free to use the function getOSname.

## Terms
**Abstraction** Scripts that use abstraction retain the same basic flow by placing the conditional execution statements within functions. When a function is called, it decides which commands to execute on a given platform.

**Conditional Execution** Alters the execution of a script based on the system type. A script that uses conditional execution usually contains an if statement at the beginning of the script that sets variables and the commands to use on a particular platform.

## Hour 24

![](img/3def70414996f811615f713b2077a154_418_0.png)

## Shell Programming FAQs
Each of the previous chapters has focused on an individual topic in shell programming, such as variables, loops, or debugging. As you progressed through the book, you worked on problems that required knowledge from previous chapters. This chapter takes a slightly different approach by trying to answer some frequently asked shell programming questions. Specifically, this chapter covers questions from three main areas of shell programming:

- The shell and commands
- Variables and arguments
- Files and directories

Each section includes several common shell programming questions (and answers!). These questions are designed to help you solve or avoid common problems. Some of the questions provide deeper background information about UNIX, whereas others illustrate concepts covered in previous chapters.

## Shell and Command Questions
This section covers some of the common questions about the shell itself and how the shell executes commands.

## Why does #!/bin/sh have to be the first line of my scripts?
Chapter 2 "Script Basics," stated that #!/bin/sh must be the first line in your script to ensure that the correct shell is used to execute your script. This line must be the first line in your shell script because of the underlying mechanism used by a shell to execute commands.

When you ask a shell to execute a command as follows

```
$ date
```

The shell uses the exec system call to ask the UNIX kernel to execute the command you requested. System calls are C language functions built into the UNIX kernel that enable you to access features of the kernel. The shell passes the name of the command that should be executed to the exec system call. This system call reads the first two characters in a file to determine how to execute the command. In the case of shell scripts, the first two characters are #!, indicating that the script needs to be interpreted by another program instead of executed directly. The rest of the line is treated as the name of the interpreter to use.

Usually the interpreter is /bin/sh, but you can also specify options to the shell on this line. Sometimes options such as -x or -v are specified to enable debugging. This also enables you to write scripts tuned for a particular shell such as ksh, bash, or zsh by using /bin/ksh, /bin/bash, or /bin/zsh instead of /bin/sh. (The exact path to the shell may vary from system to system.)

## How can I access the name of the current shell in my initialization scripts?
In your shell initialization scripts, the name of the current shell is stored in the variable $0.

Users who have a single .profile that is shared by sh, ksh, and bash use this variable in conjunction with a case statement near the end of this file to execute additional shell-specific startups. For example, you can use the following case statement in your .profile to set up the prompt, PS1, differently depending on the shell:

```
case "$0" in
*bash) PS1="\t \h \# " ;;
*ksh) PS1="\u@\h \$ " ;;
*sh) PS1="\u@\h \$ " ;;
esac
export PS1
```

Here, you have specified the shells as *bash, *ksh, and *sh, because some versions of UNIX place the - character in front of login shells, but not in front of other shells.

## How do I tell whether the current shell is interactive or non-interactive?
Some scripts need the capability to determine whether they are running in an interactive shell or a non-interactive shell. Usually this is restricted to your shell initialization scripts because you don't want to perform a full-blown initialization every time these scripts execute. Some other examples include scripts that can run from the at or cron commands.

You can tell whether a shell is interactive by checking the value of the variable $-. If the value contains the letter i, the shell is interactive. Otherwise, it is non-interactive. The following case statement illustrates one method for checking the value of $- :

```bash
case $- in
*i) : # interactive
    # commands for interactive shells go here
    ;;
*)  : # non interactive
    # commands for non-interactive shells go here
    ;;
esac
```

The following example illustrates the use of this case statement:

```bash
isInteractive () {
case $- in
  *i) echo Interactive ; ec=0 ;;
  *)  echo Non-Interactive ; ec=1 ;;
esac
return $ec
}
```

This function can be used to determine whether the current shell is interactive.

## How do I discard the output of a command?
Sometimes you will need to execute a command, but you don't want the output displayed to the screen. In these cases you can discard the output by redirecting it to the file /dev/null:

```bash
cmd > /dev/null
```

Here cmd is the name of the command you want to execute. The file is a special file (called the bit bucket) that automatically discards all its input. For example, the following command discards the output of the grep command:

```bash
if grep soda /etc/hosts > /dev/null ; then
echo 'Soda found!'
fi
```

Because commands also output error messages, you will often have to redirect STDERR to /dev/null. If you do not redirect STDERR, when a command fails your script will display that error message, which can be confusing to a user. To discard both your output command and its error output, you can redirect STDERR (file descriptor 2) to STDOUT (file descriptor 1) and redirect STDOUT to /dev/null as follows:

```
cmd > /dev/null 2>&1
```

The following example illustrates redirecting both STDERR and STDOUT to /dev/null:

```
if grep soda /etc/hosts > /dev/null 2>&1 ; then
 echo "Soda found!"
fi
```

## How can I display messages on STDERR?
You can display a message on to STDERR by redirecting STDOUT into STDERR as follows:

```
echo msg 1>&2
```

Here msg is the message you want to display. For example, the output of the following command is displayed on STDERR instead of STDOUT:

```
$ echo 'This is an error message' 1>&2
```

If you are interested in shell functions that perform additional formatting, please consult Chapter 21, "Problem Solving with Functions," which covers several shell functions that display messages on to STDERR.

## How can I determine whether a command executed successfully?
You can determine whether a command executed successfully by checking the command's exit code, which the shell stores in the variable $?. By convention, the exit code of a successful command is 0. A nonzero exit code indicates a failure.

An if statement of the following form is often used to check whether a command executed successfully:

```
cmd
if [ $? -eq 0 ] ; then
  # cmd successful
else
  # cmd failed
fi
```
