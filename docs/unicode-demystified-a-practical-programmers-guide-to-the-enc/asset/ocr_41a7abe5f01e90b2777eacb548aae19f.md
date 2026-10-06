# Shell Variables That Take on Values

**argv** This array contains the command line arguments (positional parameters) from the command line that invoked the shell. The array is indexed starting at 1, so that argv[1] contains the first command line argument. You can change any element of this array, use argv[*] to reference all the arguments together, and abbreviate references to argv as $* (short for argv[*]) and $n (short for argv[n]). Refer to “Positional Parameters” on page 581, but note that bash does not use the argv form, only the abbreviated form. Use $0 to refer to the name of the calling program.

**$argv or $@** Holds the number of elements in the **argv** array. Refer to “Special Variable Forms” on page 706.

**autolist** Controls command and variable completion (page 694).

**autologout** Enables tesh’s automatic logout facility, which logs out if you leave the shell idle for too long. The value of the variable is the number of minutes of inactivity that tash waits before logging out. The default is 60 minutes if you are Superuser; otherwise, this variable is initially unset.

**cdpath** Affects the operation of **cd** in the same way as **CDPATH** variable (page 580). It takes on an array of absolute paths (see **path**, following) and is usually set in the `.login` file with a command line like:

```
tsh $ set cdpath = /home/scott /home/scott/letters
```

When **cd** with a simple filename, it searches the working directory for a subdirectory with that name. If one is not found, **cd** searches the directories listed in **cdpath** for the file.

**correct** Set to **cd** for automatic spelling correction of command names, to all to correct the entire command line, and to complete automatic completion of command names. On corrections that you make after you press **RETURN**. Refer to “After You Press RETURN” on page 697.

**cwd** The shell sets this variable to the name of the working directory. When you access a directory through a symbolic link, tesh sets **cwd** to the name of the symbolic link. Refer to “Symbolic Links” on page 126.

**dirstack** The shell keeps the stack of directories used with the **push**, **pop**, and **dirs** built in this variable.

**ignore** You can set this variable to an array of suffixes that should be ignored during file-name completion.

**gid** The shell sets this variable to your group ID.

**histfile** Gets the full pathname of the file to be used to save the history list between login sessions. If not set, the default file, **/.history**, is used.