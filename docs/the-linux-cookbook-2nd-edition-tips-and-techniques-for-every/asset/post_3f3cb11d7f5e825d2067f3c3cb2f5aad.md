
- \a An alert or "bell" character, which rings the system bell (you can ring it yourself by typing CTRL-G).
- \d The current date.
- \h The hostname of the system.
- \n A newline character.
- \t The current system time, in 24-hour format.
- \@ The current system time, in 12-hour a.m./p.m. format.
- \w The current working directory.
- \u Your username.
- \! The history number of this command.

You can combine any number of these special characters with regular characters when creating a value for PS1.

→ To change the prompt to the current date followed by a space character, the hostname of the system in parentheses, and a greater-than character, type:

```
$ PS1='\d (\h)' [RET]
14 Dec 1999 (ithaca)>
```

In this example, the system's hostname is ithaca.

## 3.5.7 Adding to Your Path

To add or remove a directory in your path, use a text editor to change the shell variable PATH as it's defined in the .bashrc file in your home directory (see Chapter 10 [Editing Text], page 231).

For example, suppose the line that defines the PATH variable in your .bashrc file looks like this:

```
PATH="/usr/bin:/bin:/usr/bin/X11:/usr/games"
```

You can add the directory /home/nancy/bin to this path, by editing the line like so:

```
PATH="/usr/bin:/bin:/usr/bin/X11:/usr/games:/home/nancy/bin"
```

NOTES: See Chapter 5 [Files and Directories], page 125, for a complete description of directories and the path.

## 3.5.8 Controlling How the Shell Checks Your Mail

When new mail arrives for you, the shell will notify you of this before it gives you a new shell prompt. The interval between checks, in seconds, is kept in the MAILCHECK variable. The default value is 60.

⇒ Here are two ways to use this.

- To have the shell check for mail every five minutes, type:
  $ MAILCHECK=300 [RET]
- To have the shell check for mail every hour, type:
  $ MAILCHECK=3600 [RET]

The MAIL variable contains the full pathname to your system mail file, usually a directory in /var/spool/mail/ whose name is the same as your username. This is where your incoming mail arrives on the system, and it is the file that the shell checks to see if you have mail. When new messages are written to this file, the shell will tell you, before giving you another input line, that you have mail waiting. To turn off mail call, set MAIL to nothing.

⇒ To turn off mail call in the shell, type:

```
$ MAIL= [RET]
```

## 3.5.9 Seeing How Long Your Shell Has Been Running

The special variable SECONDS contains the current number of seconds that the shell has been running.

⇒ To see how many seconds the current shell has been running, type:

```
$ echo $SECONDS [RET]
```

> NOTES: To find out how long the shell has been running in minutes, hours, or some other unit of time, you can convert the number of seconds output with units (see Recipe 29.5.1 [Converting an Amount between Units of Measurement], page 567).

## 3.6 Using Alias Words

An alias is a word that represents some other command or commands—perhaps the name of a tool, a long command line, or whatever you like. Aliases are useful for creating short command names for lengthy and frequently used commands.

Once you see how an alias works, you might be tempted to make an alias for everything. However, there are differences between aliases and scripts (discussed in the next section) that you should know.

With an alias, the command you run will show up in your shell history instead of the alias name you use to call it, whereas with a shell script, only the name of the script will appear and not the commands in the script. Only you can run an alias; a script, if it is put in a public bin directory, can be run by everyone on the system.

Aliases are best for calling a tool, with or without options or arguments, by another name. How to do that is shown below.

### 3.6.1 Calling a Command by Some Other Name

Use alias to assign an alias for a command; follow it with the name of the alias, an equals sign (=), and the quoted string that the alias word should represent.

⇒ To make “bye” an alias for the exit command, type:

```
$ alias bye="exit" [RET]
```

This command makes “bye” an alias for the exit tool in the current shell, so typing bye would then run exit.

You can also include options and arguments in an alias. When you do, be sure to enclose the entire alias in double quotes.

⇒ To make “ls” an alias for the command to list a directory in color on terminals that allow color display, type:

```
$ alias ls="ls --color=auto" [RET]
```

This command makes “ls” an alias for the ls file listing tool with its --color=auto option specified, which sets color when the output is directed to a terminal that is capable of displaying it.

This is a common alias, and many Linux systems come preconfigured with it in the default .bashrc file. It’s also common to make “l” an alias for ls with the -l option (see Recipe 5.3.3 [Listing File Attributes], page 136).

When you have this alias defined you can still pass other options to ls just by specifying them; so typing ls -l in this case will execute ls --color=auto -l as the actual command.

Aliases are always expanded before the shell looks on your path, so to run a tool or program whose name is also an alias, give the full path name of
