# Changing Your csh Path

The path statement tells the shell where to look for commands, scripts, and programs. So if you issue a command, the path statement tells the system to look for the command in the named directories in a specific order. As the following steps show, you change your csh path by first identifying where your path statement is located, then editing the file that contains it (Code Listing 8.19).

# To change your csh path:

+   1. grep -i path ~/.cshrc ~/.login
+   To begin, list the configuration files located in your home directory and in the /etc directory. Look through your system configuration files for a path statement. As Code Listing 8.19 shows, it'll look something like set path = (/usr/local/bin /usr/local/bin/X11 /usr/openwin/bin /usr/bin) If you have more than one path statement, find the last one executed.
+   2. cp ~/.cshrc ~/.cshrc.backup
+   Make a copy of the file containing the path statement so that you can recover if you make mistakes. See Chapter 2 if you need more information on copying files.
+   3. vi ~/.cshrc
+   Use the editor of your choice to edit the file with the path statement in it.
+   4. set path = (/usr/local/bin /usr/bin
+   -> /usr/ucb /usr/etc
+   -> /home/users/e/ejray/bin)
+   Edit the path statement to add the full path to the bin subdirectory in your home directory, as shown in Figure 8.6.

```
xmision> grep -i path ~/.cshrc ~/.login
.cshrc:set path = (/usr/local/bin /usr/local
-> /bin/X11 /usr/openwin/bin /usr/bin)
xmision>
```

Code Listing 8.19 Use grep to find the path statement in your configuration files.

![](bbox=[0.58, 0.32, 0.9, 0.58])

Figure 8.6 Edit your path statement to add your home directory.