command language may be nearly unlimited, though, its error message set is painfully concise. "Do you know what you're doing?" is about as strong a warning message as you'll get from *mkfs*, a potentially destructive Unix utility used to initialize new file systems.

Perhaps the most surprising aspect of the MS-DOS environment is that it incorporates some Unix concepts already. For example, MS-DOS provides a "pipe" feature much like the Unix pipe mechanism, as well as a tree-like directory structure. MS-DOS also contains the *MORE* command, which functions much like the *more* command found in Unix implementations. This suggests that there may have been some persons familiar with Unix involved in the early design stages of MS-DOS.

The Unix pipe mechanism allows the output from one command to be fed directly into another command's input without the use of temporary files. A quick example is *find / | grep part*

This command is really two commands-*find* and *grep*. The *find* command outputs a list of the names of all files on the system. The *grep* command selects only those file names containing the string "part." The pipe symbol ("|") is the "pipeline" that allows the data to pass from the output of *find* to the input of *grep*.

Both the *find* and *grep* commands are invoked simultaneously in a style of computing known as "multitasking." As data becomes available on the output of *find*, it is passed directly to *grep*.

MS-DOS pipes differ from Unix pipes, however, in that MS-DOS doesn't provide true multitasking capability. Only one command runs at a time, regardless of how commands are entered on the command line.

In the early 1990s, it looked as though follow-on versions of MS-DOS might contain additional Unix-like features. For example, MS-DOS Version 6 added the ability to support multiple configurations of *CONFIG.SYS* and *AUTOEXEC.BAT* files, a move clearly intended to provide greater flexibility. Unix has supported multiple configurations for years by allowing each user to specify a *.profile* file customized according to personal tastes. It became clear, though, that Microsoft was not interested in adopting the Unix approach, having chosen instead to tread down a path consisting primarily of *GUIs* based on Windows.

^[2] Another measure for success is the number of *nonhuman* users of a program has. The more *other programs* execute a program, the better the program is. See Chapter 10.