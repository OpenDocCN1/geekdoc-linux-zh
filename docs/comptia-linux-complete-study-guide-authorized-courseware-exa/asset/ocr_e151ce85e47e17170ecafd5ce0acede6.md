by including their names in the script. You can also specify parameters to such programs in a script. For instance, suppose you want a script that launches two xterm windows and the KMail mail reader program. Listing 9.1 presents a shell script that accomplishes this goal.

# Listing 9.1: A Simple Script That Launches Three Programs

```
#!/bin/bash
/usr/bin/xterm &
/usr/bin/xterm &
/usr/bin/kmail &
```

Aside from the first line that identifies it as a script, the script looks just like the com- mands you might type to accomplish the task manually, except for one fact: The script lists the complete paths to each program. This is usually not strictly necessary, but listing the complete path ensures that the script will find the programs even if the PATH environment variable changes. On the other hand, if the program files move (say, because you upgrade the package from which they’re installed and the packager decides to move them), scripts that use complete paths will break.

Each program-launch line in Listing 9.1 ends in an ampersand (&). This character tells the shell to go on to the next line without waiting for the first to finish. If you omit the ampersands in Listing 9.1, the effect will be that the first xterm will open but the second won’t open until the first is closed. Likewise, KMail won’t start until the second xterm terminates.

Although launching several programs from one script can save time in startup scripts and some other situations, scripts are also frequently used to run a series of programs that manipulate data in some way. Such scripts typically do not include the ampersands at the ends of the commands because one command must run after another or may even rely on output from the first. A comprehensive list of such commands is impossible because you can run any program you can install in Linux as a command in a script—even another script. A few commands that are commonly used in scripts include the following:

+   - **Normal file manipulation commands** The file manipulation commands, such as 1s, mv, cp, and rm, are often used in scripts. You can use these commands to help automate repet- itive file maintenance tasks.
+   - **grep** This command is described in Chapter 1. It locates files that contain specific strings.
+   - **find** Where grep searches for patterns within the contents of files, find does so based on filenames, ownership, and similar characteristics. This command is described in Chapter 4.
+   - **cut** This command extracts text from fields in a file. It’s frequently used to extract variable information from a file whose contents are highly patterned. To use it, you pass it one or more options that specify what information you want, followed by one or more filenames. For instance, users’ home directories appear in the sixth colon-delimited field of the /etc/ passwd file. You can therefore type cut -f 6 -d ":" /etc/passwd to extract this informa- tion. The same command in a script will extract this information, which you’ll probably save to a variable or pass to a subsequent command.