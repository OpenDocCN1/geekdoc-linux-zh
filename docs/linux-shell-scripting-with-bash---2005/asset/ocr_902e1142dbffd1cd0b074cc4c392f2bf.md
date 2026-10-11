No matter what their source, commands fall into a number of informal categories. *Utilities* are general-purpose commands useful in many applications, such as returning the date or counting the number of lines in a file.

*Filters* are commands that take the results of one command and modify them in some way, such as removing unwanted lines or substituting one word for another. Many commands act as filters under the right circumstances.

To execute a command, type it at the Bash command prompt. The prompt is usually a $, but often Linux distributions customize it to something else. S.u.S.E., for example, uses a > command prompt.

The date command prints the current date and time on the screen.

```
$ date
Wed Apr 4 10:44:52 EDT 2001
```

All files, including shell commands, are case-sensitive. By convention, all shell commands are in lowercase.

```
$ DATE
bash: DATE: command not found
```

*Arguments* are additional information supplied to a command to change its behavior. The date command takes a format argument to change the appearance of the date and time.

```
$ date '+%H:%M'
10:44
```

*Switches* (also called “options” or “flags”) are characters preceded by a minus sign that enable command features. To see the date in Coordinated Universal Time (UTC, formerly called GMT), use the -u switch.

```
$ date -u
Wed Apr 4 14:46:41 UTC 2001
```

Because the terms “options” and “flags” are used in so many contexts, they are referred to as switches in this book.

Switches and arguments are collectively called *parameters*. Some commands allow any number of parameters or have parameters that can be arranged in complex ways.

The GNU and Linux convention is for longer, more readable options to be proceeded by a double minus sign. The longer equivalent to the -u switch is --universal.

```
$ date --universal
Wed Apr 4 14:46:41 UTC 2001
```

The long switches remind the reader exactly what the switch does. This makes future debugging of shell scripts much easier because there is no standard convention for the short switches across Linux commands. Most Linux commands recognize the long switches --help, --verbose, and --version.