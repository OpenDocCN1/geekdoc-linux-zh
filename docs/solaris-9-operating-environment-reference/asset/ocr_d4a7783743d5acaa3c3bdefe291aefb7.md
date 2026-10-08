# 1274

# sh, jsh

The shell parameter PATH defines the search path for the directory containing the command. Alternative directory names are separated by a colon (:). The default path is /usr/bin. The current directory is specified by a null path name that can appear immediately after the equal sign, between two colon delimiters anywhere in the path, or at the end of the path. If the command name contains a r, the search path is not used. Otherwise, each directory in the path is searched for an executable file. If the file has execution permission but is not a, it is assumed to be a file containing shell commands. A subshell is spawned to read it. A parenthesized command is also executed in a subshell.

The location in the search path where a command was found by the shell (to avoid unnecessary exec commands later). If the command was found in a relative directory, its location must be recalculated whenever the current directory changes. The shell forgets all remembered locations whenever the PATH variable is changed or the hash -r command is executed (see below).

# Special Commands

Input/output redirection is permitted for these commands. File descriptor 1 is the default output location. When job control is enabled, additional special commands are added to the shell's environment (see "Job Control" on page 1279).

+   - Do not. Return a exit code.

+   - filename Read and execute commands from filename, and return. Use the search path specified by PATH to the directory containing filename.

```
bg [%jobid ...]
```

When job control is enabled, the bg command to your environment to manipulate jobs. Resume the execution of a stopped job. If you omit %jobid, assume the current job. (See "Job Control" on page 1279 for more detail.)

+   - break [n] Exit from the enclosing or while loop if any. If you specify n, break levels.

+   - cd [argument] Change the current directory to argument. The shell parameter HOME is the default argument. The shell parameter CDPATH defines the search path for the directory containing argument. Alternate directory names with a colon (:). The default path is null (specifying the current directory). Note that the current directory is specified by a null path name that can appear immediately after the equal sign or between the colon delimiters

anywhere else in the path list. If argument begins with a /, do not use the search path. search each directory in the path for argument.

+   - chdir [dir]

The shell's working directory to dir. If you specify no argument, change to your home directory. If dir is a relative path not found in the current directory, check for it in directories listed in the CDPATH variable. If dir is the name of a shell variable whose value starts with a /, change to the directory by that value.