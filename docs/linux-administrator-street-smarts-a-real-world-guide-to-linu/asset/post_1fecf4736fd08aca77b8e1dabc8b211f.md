
## Using Commands

When you're done writing the shell script, you should modify it so that it's executable. You do this with the `chmod` command, as described in Task 1.2. Specifically, you use the `+x` option to add execute permissions, probably in conjunction with an `a` to add these permissions for all users. For instance, to make a file called `my-script` executable, you'd issue the following command:

```
$ chmod a+x my-script
```

You'll then be able to execute the script by typing its name, possibly preceded by `./` to tell Linux to search in the current directory for the script. If the script is one you run regularly, you may want to move it to a location on your path, such as `/usr/local/bin`. When you do that, you won't have to type the complete path or move to the script's directory to execute it; you can just type `my-script`.

One of the most basic features of shell scripts is the ability to run commands. You can use both shell internal commands and external commands. Most of the commands you type in a shell prompt are in fact external commands—they're programs located in `/bin`, `/usr/bin`, and other directories on your path. You can run such programs, as well as internal commands, by including their names in the script. You can also specify parameters to such programs in a script. For instance, suppose you want to start a script that launches two `xterm` windows and the KMail mail reader program. Listing 1.2 presents a shell script that accomplishes this goal.

### Listing 1.2: A Simple Script That Launches Three Programs

```bash
#!/bin/bash
/usr/bin/xterm &
/usr/bin/xterm &
/usr/bin/kmail &
```

Aside from the first line that identifies it as a script, the script looks just like the commands you might type to accomplish the task manually except for one fact: The script lists the complete paths to each program. (You may need to modify the path to `kmail`; it's not always stored in `/usr/bin`.) This is usually not strictly necessary, but listing the complete path ensures that the script will find the programs even if the `PATH` environment variable changes. Also, each program-launch line in Listing 1.2 ends in an ampersand (`&`). This character tells the shell to go on to the next line without waiting for the first to finish. If you omit the ampersands in Listing 1.2, the effect will be that the first `xterm` will open but the second won't open until the first is closed. Likewise, KMail won't start until the second `xterm` terminates.

Although launching several programs from one script can save time in startup scripts and some other situations, scripts are also frequently used to run a series of programs that manipulate data in some way. Such scripts typically do *not* include the ampersands at the ends of the commands because one command must run after another or may even rely on output from the first. A comprehensive list of such commands is impossible because you can run any program you can install in Linux as a command—even another script. The following list includes a few commands that are commonly used in scripts:

- **Normal file-manipulation commands**: The file-manipulation commands, such as `ls`, `mv`, `cp`, and `rm`, are often used in scripts. You can use these commands to help automate repetitive file maintenance tasks.
- `grep`: This command is described earlier, in “Piping Data between Programs” in Task 1.7. It locates files that contain specific patterns.
- `find`: Where `grep` searches for strings within the contents of files, `find` does so based on file names, ownership, and similar characteristics. This command is described earlier, in Task 1.4.
- `cut`: This command extracts text from fields in a file. It’s frequently used to extract variable information from a file whose contents are highly patterned. To use it, you pass it one or more options that control what it cuts followed by one or more filenames. For instance, users’ home directories appear in the sixth colon-delimited field of the `/etc/passwd` file. You could therefore include `cut -f 6 -d ":" /etc/passwd` in a script to extract this information.
- `sed`: This program provides many of the capabilities of a conventional text editor but via commands that can be typed at a command prompt or entered in a script.
- `echo`: Sometimes a script must provide a message to the user; `echo` is the tool to accomplish this goal. You can pass various options to `echo` or just a string to be shown to the user. For instance, `echo 'Press the Enter key'` causes a script to display the specified string.
- `mail`: The `mail` command can be used to send email from within a script. Pass the `-s subject` parameter to specify a subject line and give it an email address as the last argument. If it’s used from the command line, you would then type a message and terminate it with a Ctrl+D. If it’s used from a script, you might omit the message body entirely or pass it an external file as the message using input redirection. You might want to use this command to send mail to the superuser about the actions of a startup script or a script that runs on an automated basis.

![](img/f430a19bdf014c43ad7c2d594afd5b21_73_0.png)

> Many of these commands are extremely complex. You can consult their man pages for more information.

Even if you have a full grasp of how to use some key external commands, simply executing commands you might type at a command prompt is of limited utility. Many administrative tasks require you to modify what you type at a command, or even what commands you enter, depending on information from other commands. For this reason, scripting languages include additional features to help you make your scripts useful.

### Using Variables

*Variables* can help you expand the utility of scripts. A variable is a placeholder in a script for a value that will be determined when the script runs. Variables’ values can be passed as parameters to scripts, generated internally to the scripts, or extracted from the scripts’ environments.

Variables that are passed to the script are frequently called parameters. They’re represented by a dollar sign ($) followed by a number from 0 up—$0 stands for the name of the script, $1 is the first parameter to the script, $2 is the second parameter, and so on. To understand how this might be useful, consider the task of adding a user. As described earlier, in Task 1.6, creating an account for a new user typically involves running at least two commands—`useradd` and `passwd`. You might also need to run additional site-specific commands, such as commands that create unusual user-owned directories aside from the user’s home directory.

As an example of how a script with a parameter variable can help in such situations, consider Listing 1.3. This script creates an account and changes the account’s password (you’ll be prompted to enter the password when you run the script). It creates a directory in the `/shared` directory tree corresponding to the account, and it sets a symbolic link to that directory from the new user’s home directory. It also adjusts ownership and permissions in a way that may be useful, depending on your system’s ownership and permissions policies.

### Listing 1.3: A Script That Reduces Account-Creation Tedium

```bash
#!/bin/sh
useradd -m $1
passwd $1

mkdir -p /shared/$1
chown $1.users /shared/$1
chmod 775 /shared/$1
ln -s /shared/$1 /home/$1/shared
chown $1.users /home/$1/shared
```

When you use Listing 1.3, you need type only three things: the script name, the desired username, and the password (twice). For instance, if the script is called `mkuser`, you might use it like this:

```bash
# mkuser sjones
Changing password for user sjones
New password:
Retype new password:
passwd: all authentication tokens updated successfully
```

Most of the scripts’ programs operate silently unless they encounter problems, so the interaction (including typing the passwords, which don’t echo to the screen) is a result of just the `passwd` command. In effect, Listing 1.3’s script replaces seven lines of commands with one. Every one of those lines uses the username, so by using this script, you also reduce the chance of an error.

Another type of variable is assigned within scripts themselves—for instance, they can be set from the output of a command. These variables are also identified by leading dollar signs, but they’re typically given names that at least begin with a letter, such as $Addr or $Name. These variables are the same as variables you can set at the command line (as described earlier, in Task 1.8), but unless you use the `export` command, they don’t become environment variables.
