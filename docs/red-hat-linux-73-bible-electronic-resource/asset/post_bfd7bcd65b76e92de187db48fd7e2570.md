
+   BASH_VERSION — A number that represents the current version of the bash command.
+   BASH_ENV — This value identifies the location of a file that contains commands used to initialize the shell. For the bash shell, this file is probably $HOME/.bashrc. See the section about creating configuration files for information on working with the .bashrc file.
+   EUID — This is the effective user ID number of the current user. It is assigned when the shell starts, based on the user’s entry in the /etc/passwd file.
+   FCEDIT — If set, this indicates the text editor used by the fc command to edit history commands. If this variable isn’t set, the vi command is used.
+   HISTFILE — The location of your history file. It is typically located at $HOME/.bash_history.
+   HISTFILESIZE — The number of history entries that can be stored. After this number is reached, the oldest commands are discarded. The default value is 1000.
+   HISTCMD — This returns the number of the current command in the history list.
+   HOME — This is your home directory. It is your current working directory each time you log in or type the cd command with no options.
+   HOSTTYPE — A value that describes the computer architecture on which the Linux system is running. For Intel-compatible PCs, the value is i386, i486, i586, or i686.
+   MAIL — This is the location of your mailbox file. The file is typically your user name in the /var/spool/mail directory.
+   OLDPWD — The directory that was the working directory before you changed to the current working directory.
+   OSTYPE — A name identifying the current operating system. In our case, this will say linux-gnu. (Bash can run on other operating systems as well.)
+   PATH — The colon-separated list of directories used to find commands that you type. This value is initially set by the operating system, although most people modify it. The default value for regular users is:

```
/bin:/usr/bin:/usr/local/bin:/usr/bin/X11:/usr/X11R6/bin:~/bin
```

For the root user, the value also includes /sbin, /usr/sbin, and /usr/local/sbin.
+   PPID — The process ID of the command that started the current shell (for example, its parent process).
+   PROMPT_COMMAND — Can be set to a command name that is run each time before your shell prompt is displayed. Setting PROMPT_COMMAND=date prints the current date and time before the prompt line appears.
+   PS1 — Sets the value of your shell prompt. There are many items that you can read into your prompt (date, time, user name, host name, and so on). Sometimes a command requires additional prompts, which you can set with the variables $PS2, $PS3, and so on. (Setting your Prompt is described later in this chapter.)
+   $PWD — This is the directory that is assigned as your current directory. This value changes each time you change directories using the `cd` command.
+   $RANDOM — Accessing this variable causes a random number to be generated. The number is between 0 and 99999.
+   $SECONDS — The number of seconds since the time the shell was started.
+   $SHLVL — The number of shell levels associated with the current shell session. When you log in to the shell, the SHLVL is 1. Each time you start a new bash command (by, for example, using `su` to become a new user, or by simply typing `bash`), this number is incremented.
+   $TMOUT — Can be set to a number representing the number of seconds the shell can be idle without receiving input. After the number of seconds is reached, the shell exits. This is a security feature that can help make it less likely for unattended shells to be accessed by unauthorized people. (This must be set in the login shell for it to actually cause the shell to log out the user.)
+   $UID — The user ID number assigned to your user name. The user ID number is permanently stored in the /etc/passwd file.

## Set your own environment variables

Environment variables can provide a handy way of storing bits of information that you use often from the shell. You are free to create any variables that you want (although I would avoid those that are already in use) so that you can read in the values of those variables as you use the shell. (See the bash man page for a listing of shell environment variable names that are already in use.)

To set an environment variable temporarily, you can simply type a variable name and assign it to a value. Here is an example:

```
$ AB=/usr/dog/contagious/ringbearer/grind ; export AB
```

This example causes a long directory path to be assigned to the AB variable. The export AB command says to export the value to the shell so that it can be propagated to other shells you may open. With AB set, you can go to the directory by typing the following:

```
$ cd $AB
```

> **TIP:** You may have noticed that environment variables shown here are in all caps. Though case does matter with these variables, setting them as uppercase is a convention, not a necessity. You could just as easily set a variable to xyz as to XYZ (they are not the same, but either will work).

The problem with setting environment variables in this way is that as soon as you exit the shell in which you set the variable, the setting is lost. To set variables more permanently, you should add variable settings to your bash configuration files, which is described later in the section on adding environment variables.

If you want to have other text right up against the output from an environment variable, you can surround the variable in braces. This protects the variable name from being misunderstood. For example, if you wanted to add a command name to the `AB` variable shown earlier, you could do the following:

```
$ echo $AB/adventure
/usr/dog/contagious/ringbearer/grind/adventure
```

Remember that you need to export the variable for it to be picked up by other commands. You need to add the export line to a shell configuration file for it to take effect the next time you log in. The `export` command is fairly flexible. Instead of running the `export` command after you set the variable, you could do it all in one step, as follows:

```
$ export XYZ=/home/xyz/bin
```

You can override the value of any environment variable at any time. This can be temporary by typing the new value in the shell. Or you can add the changed variable command line to your `$HOME/.bashrc` file. One useful variable to update is the `PATH` variable. Here is an example:

```
$ export PATH=$PATH:/home/xyz/bin
```

In this example, I temporarily added the `/home/xyz/bin` directory to the `PATH`. This is useful if, during a shell session, you find yourself wanting to run a bunch of commands from a directory that is not normally in your `PATH`. This temporary addition saves you from typing the full or relative path each time you want to run a command.

If you decide that you no longer want a variable to be set, you can use the `unset` command to erase its value. For example, you could type `unset XYZ`, which would cause `XYZ` to have no value set. (Remember to remove the `export` from the `$HOME/.bashrc` file — if you added it there — or it will return the next time you open a new shell.)

## Managing background and foreground processes

If you are using Linux over a network or from a *dumb terminal* (a monitor that allows only text input with no GUI support), your shell may be all that you have. You may be used to a windowing environment where you have a lot of programs active at the same time so that you can switch among them as needed. This shell thing can seem pretty limited.

Though the `bash` shell doesn’t offer you a GUI for running many programs, it does offer a way to move active programs between the background and foreground. In this way, you can have a lot of stuff running, while selectively being able to choose the one you want to deal with at the moment.

There are several ways to place an active program in the background. One mentioned earlier is to add an ampersand (&) to the end of a command line. Another way is to use the at command to run one or more commands in a way in which they are not connected to the shell.

To stop a running command and put it in the background, press Ctrl+z. After the command is stopped, you can either bring it to the foreground to run (the fg command) or start it running in the background (the bg command).

## Starting background processes

If you have programs that you want to run while you continue to work in the shell, you can place the programs in the background. To place a program in the background at the time you run the program, type an ampersand (&) at the end of the command line. For example:

```
$ find /usr -print > /tmp/allusrfiles &
```

This command finds all files on your Red Hat Linux system (starting from the /usr directory), prints those filenames, and puts those names in the file /tmp/allusrfiles. The ampersand (&) runs that command line in the background. To check which commands you have running in the background, use the jobs command, as follows:

```
$ jobs
[1]  Stopped (tty output)  vi /tmp/myfile
[2]  Running     find /usr -print > /tmp/allusrfiles &
[3]  Running     nroff -man /usr/man2/* >/tmp/man2 &
[4]- Running     nroff -man /usr/man3/* >/tmp/man3 &
[5]+ Stopped     nroff -man /usr/man4/* >/tmp/man4
```

The first job shows a text-editing command (vi) that I placed in the background and stopped by pressing Ctrl+z while I was editing. Job two shows the find command I just ran. Jobs three and four show nroff commands currently running in the background. Job five had been running in the shell (foreground) until I decided too many processes were running and pressed Ctrl+z to stop job five until a few processes had completed.

The plus sign (+) next to number 5 shows that this is the job that was most recently placed in the background. The minus sign (-) next to number 4 shows that it was placed in the background just before the most recent background job. Because job 1 requires terminal input, it cannot run in the background. As a result, it appears as Stopped until it is brought to the foreground again.

> **TIP**: To see the process ID for the background job, add an -l option to the jobs command. If you type ps, you can use the process ID to figure out which command is associated with a particular background command.
