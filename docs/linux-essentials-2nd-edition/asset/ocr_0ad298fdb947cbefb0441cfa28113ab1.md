# Beginning a Shell Script

Shell scripts are plain-text files, so you can edit them in editors such as vi, nano, or, pico, as described in Chapter 10, "Editing Files." A shell script begins with a line that identifies the shell's used to run it, such as the following:

```
#!/bin/bash
```

The first two characters are a special code that tells the Linux kernel that this is a script and to use the rest of the line as a pathname to the program that's to interpret the script. (This line is sometimes called the shebang, hashbang, hasplbang, or pound bang) Shell scripting uses a hash mark (#) as a comment character, the shell utility ignores this line, although on most systems, /bin/sh is a symbolic link that points to /bin/bash, but it can point to another shell. Specifying the script system will have a program to run the script. However, if your script uses any features of a particular shell, you should specify that shell instead—for instance, use /bin/bash or /bin/tsh instead of /bin/sh. This chapter describes Bash scripts. Simple scripts can run in other shells, but more-complex scripts are shell-specific.

When you're writing the shell script, you should modify it so it's executable. You can do this with the chmod command, which is described in more detail in Chapter 14, "Setting Ownership and Permissions." For now, you can use the +x option to add execute permissions for all users. For instance, to make a file called my-script executable, you should issue the following command:

```
$ chmod +x my-script
```

You'll be able to execute the script by typing its name, possibly by ./Linux Linux to run the script in the current directory rather than searching the current path. If you fail to make the script executable, you can still run the script by running the shell program followed by the script name (as in my-script), but it's generally better to make the script executable. If the script is one regularly, you might want to move it to a location on your path, such as /usr/local/bin. When you do that, you won't have to type the complete path or move the script's directory to execute; you can just type my-script.

# Using Commands

One of the most basic features of shell scripts is the ability to run commands. You can use both commands that are built into the shell and external commands—that is, you can run other programs as Most of the