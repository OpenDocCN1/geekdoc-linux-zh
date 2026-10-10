
## Beginning a Shell Script

Shell scripts are plain-text files, so you create them in text editors. A shell script begins with a line that identifies the shell that's used to run it, such as the following:

```
#!/bin/sh
```

The first two characters are a special code that tells the Linux kernel that this is a script and to use the rest of the line as a pathname to the program that's to interpret the script. (This line is sometimes called the *shebang, bashbang, hashbungle, or pound bang* line.) Shell scripting languages use a hash mark (#) as a comment character, so the script utility ignores this line, although the kernel doesn't. On most systems, */bin/sh* is a symbolic link that points to */bin/bash*, but it can point to some other shell. Specifying the script as using */bin/sh* guarantees that any Linux system will have a shell program to run the script; but if the script uses any features specific to a particular shell, you should specify that shell instead—for instance, use */bin/bash* or */bin/tcsh* instead of */bin/sh*.

When you're done writing the shell script, you should modify it so that it's executable. You do this with the *chmod* command, as described in Chapter 4, “Managing Files.” Specifically, you use the +*x* option to add execute permissions, probably in conjunction with a *t* to add these permissions for all users. For instance, to make a file called *my-script* executable, you should issue the following command:

```
$ chmod a+x my-script
```

You'll then be able to execute the script by typing its name, possibly preceded by ./* to tell Linux to run the script in the current directory rather than searching the current path. If you fail to make the script executable, you can still run the script by running the shell program followed by the script name (as in *bash my-script*), but it's generally better to make the script executable. If the script is one you run regularly, you may want to move it to a location on your path, such as */usr/local/bin*. When you do that, you won't have to type the complete path or move to the script's directory to execute it; you can just type *my-script*.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_495_0.png)

> It's possible to set a script's SUID or SGID bits. (See Chapter 4 for information about the SUID and SGID bits.) Doing so is potentially dangerous, particularly if the script is owned by *root*, for reasons described in Chapter 4. You should therefore be very cautious about applying the SUID bit to scripts.

## Using Commands

One of the most basic features of shell scripts is the ability to run commands. You can use both shell internal commands and external commands. Most of the commands you type in a shell prompt are external commands—they're programs located in */bin*, */usr/bin*, and other directories on your path. You can run such programs, as well as internal commands, by including their names in the script. You can also specify parameters to such programs in a script. For instance, suppose you want a script that launches two xterm windows and the KMail mail reader program. Listing 9.1 presents a shell script that accomplishes this goal.

### Listing 9.1: A Simple Script That Launches Three Programs

```
#!/bin/bash
/usr/bin/xterm &
/usr/bin/xterm &
/usr/bin/kmail &
```

Aside from the first line that identifies it as a script, the script looks just like the commands you might type to accomplish the task manually, except for one fact: The script lists the complete paths to each program. This is usually not strictly necessary, but listing the complete path ensures that the script will find the programs even if the PATH environment variable changes. On the other hand, if the program files move (say, because you upgrade the package from which they’re installed and the packager decides to move them), scripts that use complete paths will break.

Each program-launch line in Listing 9.1 ends in an ampersand (&). This character tells the shell to go on to the next line without waiting for the first to finish. If you omit the ampersands in Listing 9.1, the effect will be that the first xterm will open but the second won’t open until the first is closed. Likewise, KMail won’t start until the second xterm terminates.

Although launching several programs from one script can save time in startup scripts and some other situations, scripts are also frequently used to run a series of programs that manipulate data in some way. Such scripts typically do not include the ampersands at the ends of the commands because one command must run after another or may even rely on output from the first. A comprehensive list of such commands is impossible because you can run any program you can install in Linux as a command in a script—even another script. A few commands that are commonly used in scripts include the following:

- **Normal file manipulation commands**: The file manipulation commands, such as *ls*, *mv*, *cp*, and *rm*, are often used in scripts. You can use these commands to help automate repetitive file maintenance tasks.
- **grep**: This command is described in Chapter 1. It locates files that contain specific strings.
- **find**: Where grep searches for patterns within the contents of files, find does so based on filenames, ownership, and similar characteristics. This command is described in Chapter 4.
- **cut**: This command extracts text from fields in a file. It’s frequently used to extract variable information from a file whose contents are highly patterned. To use it, you pass it one or more options that specify what information you want, followed by one or more filenames. For instance, users’ home directories appear in the sixth colon-delimited field of the /etc/passwd file. You can therefore type `cut -f 6 -d ":" /etc/passwd` to extract this information. The same command in a script will extract this information, which you’ll probably save to a variable or pass to a subsequent command.

- **sed**: This program is described in Chapter 1. It provides many of the capabilities of a conventional text editor but via commands that can be typed at a command prompt or entered in a script.
- **echo**: Sometimes a script must provide a message to the user; `echo` is the tool to accomplish this goal. You can pass various options to `echo` or just a string to be shown to the user. For instance, `echo 'Press the Enter key'` causes a script to display the specified string.
- **mail**: The `mail` command can be used to send e-mail from within a script. Pass it the `-s subject` parameter to specify a subject line, and give it an e-mail address as the last argument. If used at the command line, you then type a message and terminate it with a `Ctrl+D` keystroke. If used from a script, you might omit the subject entirely, pass it an external file as the message using input redirection, or use a here document to pass text to the `mail` command as input. (Chapter 1 describes input redirection and here documents.) You might want to use this command to send mail to the sysuser about the actions of a startup script or a script that runs on an automated basis. This command is described in more detail later in this chapter.

> Many of these commands are extremely complex, and completely describing them is beyond the scope of this chapter. You can consult these commands' man pages for more information. A few of them are described elsewhere in this book.

Even if you have a full grasp of how to use some key external commands, simply executing commands you might when typing them at a command prompt is of limited utility. Many administrative tasks require you to modify what you type at a command, or even what commands you enter, depending on information from other commands. For this reason, scripting languages include additional features to help you make your scripts useful.

## Using Variables

*Variables* can help you expand the utility of scripts. A variable is a placeholder in a script for a value that will be determined when the script runs. Variables' values can be passed as parameters to scripts, generated internally to the scripts, or extracted from the script's environment.

Variables that are passed to the script are frequently called *parameters*. They're represented by a dollar sign ($) followed by a number from 0 to 9—$0 stands for the name of the script, $1 is the first parameter to the script, $2 is the second parameter, and so on. To understand how this might be useful, consider the task of adding a user. As described in Chapter 7, “Administering the System,” creating an account for a new user typically involves running at least two commands—`useradd` and `passwd`. You may also need to run additional site-specific commands, such as commands that create unusual user-owned directories aside from the user's home directory.
