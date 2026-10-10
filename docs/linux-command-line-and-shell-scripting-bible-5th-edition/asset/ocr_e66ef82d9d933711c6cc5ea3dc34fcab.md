# TABLE 6.2 Continued

| Variable | Description |
| --- | --- |
| S H L V L | Indicates the shell level, incremented by one each time a new Bash shell is started |
| T I M E F O R M A T | A format specifying how the shell displays time values |
| T M O U T | The value of how long (in seconds) the select and read commands should wait for input (the default of 0 indicates to wait indefinitely) |
| T M P D I R | Directory name where the Bash shell creates temporary files for its use |
| U I D | The numeric real user ID of the current user |

You may notice that not all default environment variables are shown when the set command is used. When not in use, a default environment variable is not required to contain a value.

> Whether or not a default environment variable is in use on your system sometimes depends on the version of the Bash shell running. For example, EPOCHREALTIME is only available on Bash shell version 5 and above. You can view your Bash shell’s version number by typing bash --version and pressing Enter at the CLI.

# Setting the PATH Environment Variable

When you enter an external command (see Chapter 5, "Understanding the Shell") in the shell CLI, the shell must search the system to find the program. The PATH environment variable defines the directories it searches looking for commands and programs. On this Ubuntu 24.04 Linux system, the PATH environment variable looks like this:

```
$ echo PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin: /sbin:/bin:/usr/games:/usr/local/games: ./snap/bin: $
```

The directories in the PATH are separated by colons. And this shows that there are nine directories where the shell looks for commands and programs.

If a command’s or program’s location is not included in the PATH variable, the shell cannot find it without an absolute directory reference. If the shell cannot find the command or program, it produces an error message:

```
$ myprog myprog: command not found
```