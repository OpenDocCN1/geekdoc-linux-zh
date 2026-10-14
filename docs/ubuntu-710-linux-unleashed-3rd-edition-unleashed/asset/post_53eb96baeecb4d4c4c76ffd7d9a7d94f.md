
This simple script creates command aliases, or convenient shorthand forms of commands, for the ls and cp commands. The ll alias provides a long directory listing: The ldir alias is the ls command, but prints indicators (for directories or executable files) in listings. The copy alias is the same as the cp command. You can experiment and add your own options or create aliases of other commands with options you frequently use.

You can execute myenv in a variety of ways under Linux. As shown in this example, you can make myenv executable by using the chmod command and then execute it as you would any other native Linux command:

```
$ chmod +x myenv
```

This line turns on the executable permission of myenv, which can be checked with the ls command and its -l option like this:

```
$ ls -l myenv
-rwxrwxr-x 1 winky winky 11 Aug 26 17:38 myenv
```

## Running the New Shell Program

You can run your new shell program in several ways. Each method will produce the same results, which is a testament to the flexibility of using the shell with Linux. One way to run your shell program is to execute the file myenv from the command line as if it were a Linux command:

```
$ ./myenv
```

A second way to execute myenv under a particular shell, such as pdksh, is as follows:

```
$ pdksh myenv
```

This invokes a new pdksh shell and passes the filename myenv as a parameter to execute the file. A third way will require you to create a directory named bin in your home directory, and to then copy the new shell program into this directory. You can then run the program without the need to specify a specific location or to use a shell. You do this like so:

```
$ mkdir bin
$ mv myenv bin
$ myenv
```

This works because Ubuntu is set up by default to include the executable path $HOME/bin in your shell's environment. You can view this environment variable, named PATH, by piping the output of the env command through fgrep like so:

```
$ env | fgrep PATH
/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin: \
/usr/X11R6/bin:/sbin:/home/paul/bin
```

As you can see, the user (paul in this example) can use the new bin directory to hold executable files. Another way to bring up an environment variable is to use the echo command along with the variable name (in this case, $PATH):

```
$ echo $PATH
/usr/kerberos/bin:/usr/local/bin:/usr/bin:.:/usr/X11R6/bin:/home/bball/bin
```

## CAUTION

> Never put . in your $PATH in order to execute files or a command in the current directory—this presents a serious security risk, especially for the root operator, and even more so if . is first in your $PATH search order. Trojan scripts placed by crackers in directories such as /tmp can be used for malicious purposes, and will be executed immediately if the current working directory is part of your $PATH.

## Storing Shell Scripts for Systemwide Access

After you execute the command myenv, you should be able to use ldir from the command line to get a list of files under the current directory and ll to get a list of files with attributes displayed. However, the best way to use the new commands in myenv is to put them into your shell's login or profile file. For Ubuntu, and nearly all Linux users, the default shell is bash, so you can make these commands available for everyone on your system by putting them in the /etc/bashrc file. Systemwide aliases for tcsh are contained in files with the extension .csh under the /etc/profile.d directory. The pdksh shell can use these command aliases as well.

## NOTE

> To use a shell other than bash after logging in, use the chsh command from the command line or the system-config-users client during an X session. You'll be asked for your password (or the root password if using system-config-users), as well as the location and name of the new shell (refer to Table 11.1). The new shell will become your default shell, but only if its name is in the list of acceptable system shells in /etc/shells.

## Interpreting Shell Scripts Through Specific Shells

The majority of shell scripts use a shebang line (#!) at the beginning to control the type of shell used to run the script; this bang line calls for an sh-incantation of bash:

```
#!/bin/sh
```

A shebang line (it is short for "sharp" and "bang", two names for # and !) tells the Linux kernel that a specific command (a shell, or in the case of other scripts, perhaps awk or Perl) is to be used to interpret the contents of the file. Using a shebang line is common
