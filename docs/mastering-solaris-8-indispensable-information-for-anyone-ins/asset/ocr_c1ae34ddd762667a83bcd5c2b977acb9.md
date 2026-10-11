developer, it's not too hard to understand what a program is doing (source code) and what the results or output will be (t truss output).

# ## Debugging Shell Scripts

Shell scripts are a lot easier to debug than compiled executable programs. Most shell scripts have commands and lines of text that a typical system administrator should understand. When it comes to troubleshooting shell scripts, the first step is to check the permissions on the shell script itself. A user needs to have some type of executable permission on a shell script to run the script. The most important things to find out are whether the user can get to the script (directory permissions) and whether the user can execute the script (script executable permission).

When you want to debug a script, you can use the shell's -x option in the Bourne shell or the Korn shell. This option causes the shell to display each command before it runs the command. This trace of a script's execution can give you information about where the bugs are. You can set the -x option for the current shell so that all scripts display commands as they are run or you can use the -x option to affect only the script you are currently debugging. Use the set command at the top of the script:

```
```text
set -x
```
```

Once this option is set, each command that the script executes will be preceded by a plus sign so that you can distinguish the output of the trace from any output that your script produces. To turn off the debug option, set the +x option:

```
```text
set +x
```
```

If the user can execute the shell script but problems occur, the easiest troubleshooting technique is to look for obvious typos. Look for long lines that don't have the proper line wrap character for the particular shell. In most cases, the line wrap character at the end of the line should be the backslash character.

Also look for commands and text files that are not in the correct directory. For example, suppose you are troubleshooting a shell script with the line /etc/1s in it. That line executes the command 1s from the /etc directory. Because 1s does not reside in the /etc directory, that line could be one source of the problem. Use the find / -name 1s command to find the proper location of 1s and repair the incorrect line.

When it comes to small scripts, comment out everything with a # sign before each line of code. Remember, any line in a shell script with the # sign and a space as the first two characters is only a comment. Now slowly uncomment each logical section of code until the problem is found. Add the echo $VARIABLE lines into the code to see what is happening with any variable. It's easy enough to comment out the echo $VARIABLE lines when they are not needed.