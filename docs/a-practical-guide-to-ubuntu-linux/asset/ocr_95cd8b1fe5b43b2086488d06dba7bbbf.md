# 320 CHAPTER 9 THE BOURNE SHELL

The default value of PATH is determined when bash is compiled. It is not set in a startup file, although it may be modified. Normally the default specifies that the shell search several system directories used to hold common commands. These system directories include /bin and /usr/bin and other directories appropriate to the local system. When you give a command, if the shell does not find the executable—readable—file named by the command in any of the directories listed in PATH, the shell generates one of the aforementioned error messages.

Working directory The PATH variable specifies the directories in the order the shell should search them. Each directory must be separated from the next by a colon. The following command sets PATH so that a search for an executable file starts with /usr/local/bin directory. If it does not find the file in this directory, the shell looks next in /bin, and then in /usr/bin. If the search fails in those directories, the shell looks in ~bin directory, a subdirect of the user's home directory. Exporting PATH makes its value accessible to sub:

```
$ export PATH=$usr/local/bin:/bin:/usr/bin:-
```

A null value in the string indicates the working directory. In the preceding example, A null value (nothing in between the colon and the end of the line) appears as the last element of the string. The working directory is represented by a leading colon (not recommended; see the following security tip), a trailing colon (as in the example), or two colons next to each other anywhere in the string. You can also represent the working directory explicitly with a period (.).

Because Linux has many executable files in directories named bin (binary), users typically put their executable files in their ~/bin directories. If you put your own bin directory at the end of your PATH, as in the preceding example, the shell looks for any commands that cannot find in directories earlier in PATH.

# PATH and security

security Do not put the working directory first in PATH when security is a concern. If you are working root, you should never put the working directory first in PATH. It is common for root's PATH to omit the working directory entirely. You can execute a file in the working directory by prepending : to the name: /myprog.

Putting the working directory first in PATH can create a security hazard. Most people type is the first command when entering a directory. If the owner places an executable file named is in the directory, and the working directory appears in a user's PATH, the user giving an is command from the directory executes the ls in the working directory instead of the system ls utility, possibly with undesirable results.

If you want to add directories to PATH, you can reference the old value of the PATH variable in setting PATH to a new value (but see the preceding security tip). The following command adds /usr/local/bin to the beginning of the current PATH bin directory in the user's home directory (~bin) to the end: