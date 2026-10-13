# Shell and Command Questions

This section covers some of the common questions about the shell itself and how the shell executes commands.

# Why does #!/bin/sh have to be the first line of my scripts?

Chapter 2 "Script Basics," stated that #!/bin/sh must be the first line in your script to ensure that the correct shell is used to execute your script. This line must be the first line in your shell script because of the underlying mechanism used by a shell to execute commands.

When you ask a shell to execute a command as follows

```
$ date
```

The shell uses the exec system call to ask the UNIX kernel to execute the command you requested. System calls are C language functions built into to the UNIX kernel that enable you to access features of the kernel. The shell passes the name of the command that should be executed to the exec system call. This system call reads the first two characters in a file to determine how to execute the command. In the case of shell scripts, the first two characters are #!, indicating that the script needs to be interpreted by another program instead of executed directly. The rest of the line is treated as the name of the interpreter to use.

Usually the interpreter is /bin/sh, but you can also specify options to the shell on this line. Sometimes options such as -x or -v are specified to enable debugging. This also enables you to write scripts tuned for a particular shell such as ksh, bash, or zsh by using /bin/ksh, /bin/bash, or /bin/zsh instead of /bin/sh. (The exact path to the shell may vary from system to system.)

# How can I access the name of the current shell in my initialization scripts?

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