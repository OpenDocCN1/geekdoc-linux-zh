defaults for ls command. Red Hat, for example, has the -q and -F switches on by default. From the point of view of script writing, it's not safe to use the ls command in a script without specifying the appropriate switches because you can't be sure which defaults a particular distribution uses.

ls hides files that begin with a period. This is the Linux convention for configuration files, history files, and other files that a user isn't normally interested in. To see these files, use the -a (all) switch. Use -A (absolutely all) to show the implicit . and .. files as well.

```
$ ls -A
.bash_history .bash_logout .bash_profile .bashrc archive
check-orders.sh orders.txt
```

The filenames can be printed in color to show the kind of file they are. The colors are defined in a file /etc/DIR_COLORS. You can customize the colors using a .dir_colors file in your own directory. The format of the file is described in the /etc/DIR_COLORS file.

To display the files without color and with symbols instead, use the --color and --classify (or -F) switches. (On most Linux distributions, this feature is turned on using aliases.)

```
$ ls --color=never --classify
archive/ check-orders.sh* orders.txt
```

The --classify symbols are directories (/), programs (*), symbolic links (@), pipes (|), and Unix domain socket files (=). These symbols are not a part of the name: They are hints as to the type of file. In this example, archive is a directory and check-orders.sh is a program.

Another very important switch is --hide-control-chars (or -q). Linux filenames can contain any character, even control characters. It is possible to create a filename with hidden characters in the name. In these cases, you can't rename or delete the file unless you know what the hidden characters are. Contrary to what the name implies, the --hide-control-chars switch displays any unprintable characters in the filename as question marks, making their locations visible.

```
$ rm orders.txt
rm: orders.txt: non-existent
$ ls --color=never --classify --hide-control-chars
archive/ check-orders.sh* orders.txt
```

A complete list of switches appears at the end of this chapter.

# printf Command

The built-in printf (*print formatted*) command prints a message to the screen. You will use this command a lot in shell scripts.

printf is very similar to the C standard I/O printf() function, but they are not identical. In particular, single- and double-quoted strings are treated differently in shell scripts than in C programs.