
# Writing Scripts

One of many possible actions defined by the readline library, which is one of the basic text-mode input libraries used by Linux.

In most cases, there's no need to adjust the ~/.inputrc file, because the default readline mappings work well for x86 systems with standard keyboards. If you find that certain keystrokes don't work the way they do in text mode, though, you may want to research this configuration filter.

> X uses its own keyboard input routines, so /.inputrc doesn't affect programs run in X, even text-mode programs run inside xterm windows.

# Writing Scripts

You'll do much of your work on a Linux system by typing commands at a shell prompt. As you use Linux, you're likely to find some of these tasks to be repetitive. If you need to add 100 new users to the system, for instance, typing userid 100 times can be tedious. Fortunately, Linux includes a way to cut through the tedium: shell scripts. These are simple programs written in an interpreted language that's embedded in the Linux shell you use to type commands.

Most Linux users use bash by default, so shell scripts are often written in the bash scripting language; tcsh and other scripting languages are similar. In fact, it's not uncommon to see shell scripts that run in any common Linux shell. You're not restricted to running shell scripts written in your default shell, however; the first line of a shell script identifies the shell that should be used to run it.

> Many Linux startup scripts, including SysV startup scripts, are in fact shell scripts. Therefore, understanding shell scripting is necessary if you want to modify a Linux startup script.

Like any programming task, shell scripting can be quite complex. Consequently, this chapter barely scratches the surface of what can be accomplished through shell scripting. Consult a book on the topic, such as Cameron Newham's Learning the Bash Shell, 3rd Edition (O'Reilly, 2005) or Richard Blum and Christine Bresnan's Linux Command Line and Shell Scripting Bible, 2nd Edition (Wiley, 2011), for more information.

To create a script, you must first know how to begin editing. Once you do, you'll find that one of the easiest tasks to do is to call external commands. More advanced tasks include using variables and using conditional expressions.

# Beginning Shell Script

Shell scripts are plain-text files, you create them in text editors. A shell script begins with a line that identifies the shell that's used to run it, such as the following:

```bash
#!/bin/sh
```

The first two characters of the line are a special character that tells the Linux kernel that this is a script and to use the rest of the line as a pathname to the program that's to interpret the script (This line is sometimes called the shebang, hashbang, hasplbang, or pound line). Shell languages use a hash mark (#) as a comment character, the shell utility ignores this line, the kernel doesn't. On many systems, /bin/sh is a symbolic link that points to /bin/bash, which guarantees that any Linux system will have a shell program to run the script; specifying the script by /bin/sh guarantees that any Linux system will have a shell program; if the script uses any specific features of a particular shell, you should specify that shell instead—for instance, by using /bin/bash or /tcsh instead of /bin/sh.

When you're down to execute the script, you should modify it so it's executable. You do this with the chmod command, as described in Chapter 4, "Managing Files." Specifically, you use the +x option to add execute permissions, probably in conjunction with to add these permissions for all users. For make a file called my-script executable—for instance, you should use the following command:

```bash
$ chmod +x my-script
```

You'll be able to execute the script by typing its name, possibly preceded by ./ to run it in the current directory rather than searching the path. If you fail to make the script executable, you can still run it by running the shell program followed by the script name (in bash my-script), but it's generally better to make the script executable. If the script is one you run regularly, you might want to move it to a location on your path, such as /usr/local/bin. When you do, you won't have to type the complete path or move to your directory to execute; you can just use my-script.

> It's possible to set a script's SUID or SGID bits (See Chapter 4 for information about the SUID and SGID bits). Doing so is potentially dangerous, particularly if the script is owned by root, for reasons described in Chapter 4. You should be very careful about applying the SUID bit to scripts.

![](img/35f616c7eba4e79e12bfd762129c5d27_488_0.png)

Another way to run a script requires mention: sourcing it. You can source a script using the keyword or a dot (.), as follows:

```bash
$ source my-script
$ . my-script
```

Sourcing a script causes it to run in the current shell, as opposed to launching a new instance of the shell, as occurs when you run a script by typing its name alone or using the exec command, as described in Chapter 1. This has some important implications:

- * When you source a script, it will have access to environment variables set in the calling shell, even if you haven't exported them. Ordinarily, only environment variables that you explicitly export become available to scripts you run.
- * If you source a script, any changes it makes to the environment will persist after the script finishes. If you run the script in a subshell, the changes will be lost when the shell exits.
- * Sourcing a script can be faster than executing it, because you don't have to start a new shell process.
- * Sourcing a script can be dangerous if the script contains malicious code. You should only source scripts that you trust.

# Using Commands

One of the most basic features of shell is the ability to run commands. You can type commands at a prompt or enter them in a script. Many commands are built into the shell, while others are external programs located in directories that are in your PATH.

**Normal File Manipulation Commands** The file manipulation commands, such as ls, mv, cp, and rm, are often used in scripts. You can use these commands to help automate repetitive tasks.

**grep** This command is described in Chapter 1. It locates files that contain specific strings.

**find** Where grep searches for patterns within the contents of files, find does so by filenames, ownership, and similar characteristics. This command is described in Chapter 4.

**cut** This command extracts text from fields in a file. It is frequently used to extract information from file whose contents are highly patterned. To use it, you pass one or more options to specify what information you want, followed by one or more filenames. For instance, `cut -f 6 -d ":" /etc/passwd` to extract information. The same command in a script will extract this information, which you'll probably save to a variable or to a subsequent command.

**sed** This program is described in Chapter 1. It provides many of the capabilities of a conventional text editor but via commands that can be typed at a command prompt or entered in a script.

**echo** Sometimes a script must provide a message to the user; echo is the tool to accomplish this. You can pass various options to echo or just a string to be shown to the user. For instance, `echo "Press the Enter key"` causes a script to display the specified string.

**mail** The mail command can be used to send email from a script. Pass it the -s subject parameter to specify a subject line, and give it an email address as the last argument. If used at the command line, then type a message and terminate it with a Ctrl+D keystroke. If used from a script, you might omit the subject entirely, or pass it an external file as the message using redirection, or use a document tool to pass text to the mail command as input. (Chapter 1 describes input redirection and here documents.) You might want to use this to send mail to the superuser about the actions of a startup script or a script that runs on an automated basis. This command is described in more detail later in this chapter.
