arguments in this way (including the cd and file commands). Some commands can also accept options. Tell the command how to do its work, and they have the format of a hyphen followed by a code that tells the command option(s) to use.

There are several options you can use with ls to change its results, shown in Table 5-1. For example, change into your home directory and use

```
pi@raspberry ~ $ ls -R
```

This lists all the contents in your home directory, and then all contents in the folders that are inside your home directory. You can use the scroll bar on the right side of the shell to see them all.

When you're using options and arguments together, the options come before the arguments, the format of the typical Linux command is

```
command -options arguments
```

For example, try using the -X option to list the contents of the python_games folder. All the .png, .py, and .wav files will be grouped together, so it's easier to see what's there. The command to use is

```
pi@raspberry ~ $ ls -X ~/python_games
```

You can use several options together by adding the option codes after a single hyphen. For example, if you want to list all your directories under your current directory (option R) and you want to group your results by file type (option X) and use symbols to indicate directories and executables beside their filenames (option F), you would use

```
pi@raspberry ~ $ ls -RXF
```

5-2 shows the resulting output. We've scrolled up the scroll bar, so you're looking at the start of the results, not the end. One thing you might notice is that a single period (full stop) is used to refer to the current directory in the pathname, the path for the first set of results is simply a period. This short code for the current directory is similar to the two periods used to refer to the parent directory.

![](bbox=[0.181, 0.807, 0.233, 0.863])

TIP When you're experimenting with ls (or at any other time, to that), use the command clear to empty the screen if it gets messy and hard to follow.