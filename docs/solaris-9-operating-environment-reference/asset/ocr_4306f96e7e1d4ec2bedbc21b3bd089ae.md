# 1562

# xargs

with it. An easy rule that you can use to transform any string into a quoted form that xargs interprets correctly is to precede each character in the string with a backslash (\).

On implementations with a large value for {ARG_MAX}, xargs may produce command longer than {LINE_MAX}. For invocation of commands, this is not a problem. If xargs is being used to create a text file, you should explicitly set the maximum command-line length with the -s option

The xargs command returns exit status 127 if an error occurs so that applications can distinguish "failure to find a command" from "invoked command with an error indication." The value 127 was chosen because it is not commonly used for other meanings; most commands use small values for "normal" error conditions, and the values above 128 can be confused with termination of receipt of a signal. The value 126 was chosen in a similar manner to indicate that the command could be found without

Examples

The following example moves all files from directory $1 to directory $2 and echoes each mv just before doing it.

```
ls $1 | xargs -I {} -t mv $1 $2/$
```

The following example combines the output of the parenthesized commands onto one line, which is written to the end of log file.

```
(logname; date; printf "%s\n" "$0 $*") | xargs >>log
```

The following command invokes diff with successive pairs of arguments originally typed as command-line arguments (assuming there are no embedded blank characters in the elements of the original list).

```
printf "%%s\n" "$*" | xargs -n 2 -x diff
```

In the following example, the user is asked which files in the current directory are to be archived. The files are archived into arch either one at a time (for the first example) or many at a time (for the second example).

```
castle@ $1 | xargs -p -L 1 ar -r arch
-r arch Mail?...y
ar: creating arch
-r arch SOLD515.PKG?...y
-r arch catman.man?...y
-r arch examples?...y
castle@
```

```
castle@ $1 | xargs -p -L 1 | xargs ar -r arch
/usr/bin/echo Mail?...y
/usr/bin/echo SOLD515.PKG?...y
/usr/bin/echo arch?...y
/usr/bin/echo catman.man?...y
/usr/bin/echo examples?...y
castle@
```