# Background commands

Some commands can take a while to complete. Sometimes you may not want to tie up your shell waiting for a command to finish. In those cases, you can have the commands run in the background by using the ampersand (&).

Text formatting commands (such as *nroff* and *troff*, which were described earlier) are examples of commands that you may want to run in the background if you are formatting a large document. You also may want to create your own shell scripts that run in the background to check continuously for certain events to occur, such as the hard disk filling up or particular users logging in.

Here is an example of a command being run in the background:

```
$ troff -me verylargedocument | lpr &
```

There are other ways of managing background and foreground processes. These different methods are described in detail in the “Managing background and foreground processes” section.

# Expanding commands

With command substitution, you can have the output of a command interpreted by the shell instead of by the command itself. In this way, you can have the standard output of a command become an argument for another command. The two forms of command substitution are $(command) or `command`.

The command in this case can include options, metacharacters, and arguments. Here is an example of using command substitution:

```
$ vi $(find /home -print | grep xyzzy)
```

In this command line, the command substitution is done before the *vi* command is run. First, the *find* command starts at the `/home` directory and prints out all files and directories below that point in the file system. This output is piped to the *grep* command, which filters out all files except for those that include the string *xyzzy*. Finally, the *vi* command opens all filenames for editing (one at a time) that include *xyzzy*.

This particular example may be useful if you knew that you wanted to edit a file for which you knew the name but not the location. As long as the string was fairly uncommon, you could find and open every instance of a particular filename existing beneath any point you choose in the file system.

# Expanding arithmetic expressions

There may be times when you want to pass arithmetic results to a command. There are two forms you can use to expand an arithmetic expression and pass it to the shell: ${expression} or $(expression). Here is an example: