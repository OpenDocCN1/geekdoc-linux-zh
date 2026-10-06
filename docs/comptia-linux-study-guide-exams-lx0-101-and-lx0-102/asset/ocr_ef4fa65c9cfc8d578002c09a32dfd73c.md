+   * When you source a script, it will have access to environment variables set in the calling shell, even if you haven't exported them. Ordinarily, only environment variables that you explicitly export become available to scripts you run.

+   * If you source a script and if that script sets an environment variable, variable will become available (or will be changed) in the calling shell. If you run the script normally, any environment variables it will remain local to it and to the programs that it calls, even if the scripts export the variables.

+   * Running a script in the normal ways imposes overhead costs associated with launching the new shell. These costs are normally negligible, but if a script calls itself recursively or calls many other scripts, sourcing these scripts within the first script may improve performance.

+   * Sourcing a script causes it to execute in the shell's language, whereas running a script normally causes it to use the shell language specified on the hashbang line.

# Using Commands

One of the most basic features of shell is the ability to run commands. You can use both shell internal commands and external commands. Most of the commands you type in a shell prompt are external commands—they're programs located in /bin, /usr/bin, and other directories on path. You can run such programs, as well as internal commands, by including their names in the script. You can also specify parameters to such programs in a script. For instance, suppose you want a script that launches xterm windows and the KMail reader program. Listing 9.1 shows a script that accomplishes this goal.

# Listing 9.1: A simple script that launches three programs

```
#!/bin/bash
/usr/bin/xterm &
/usr/bin/xterm &
/usr/bin/kmail &
```

Aside from the first line that identifies it as a script, the script looks just like the commands you might type to accomplish the task manually, except for one fact: The script lists the complete paths to each program. This is not strictly necessary, but listing the path ensures that the script will find the programs even if the PATH variable changes. On the other hand, if the program files move (say, you upgrade the package from which they're installed and the package decides to move them), scripts that use complete paths will break.

Each program-launch in Listing 9.1 ends in the ampersand (&). This character tells the shell to go on to the next line without waiting for the first to finish. If you omit the ampersands in Listing 9.1, the effect will be waiting for the first xterm will open but the second won't open until the first is closed. Likewise, KMail won't start until the second xterm terminates.