Here is an example of a command being run in the background:

```
`$ troff -me very_large_document | lpr &`
```

There are other ways to manage background and foreground processes (described in the “Managing Background and Foreground Processes” section later in this chapter).

# ### Expanding Commands

With command substitution, you can have the output of a command interpreted by the shell instead of by the command itself. In this way, you can have the standard output of a command become an argument for another command. The two forms of command substitution are `$(command)` or `` `command` ``. (The first case is the preferred method.)

The command in this case can include options, metacharacters, and arguments. Here is an example of using command substitution:

```
`$ vi $(find /home | grep xyz123)`
```

In this command line, the command substitution is done before the `vi` command is run. First, the `find` command starts at the `/home` directory and prints out all files and directories below that point in the file system. This output is piped to the `grep` command, which filters out all files except for those that include the text `xyz123`. Finally, the `vi` command opens all filenames for editing (one at a time) that include `xyz123`.

This particular example might be useful if you knew that you wanted to edit a file for which you knew the name but not the location. As long as the string was uncommon, you could find and open every instance of a filename existing beneath a point you choose in the file system.

# ### Expanding Arithmetic Expressions

There may be times when you want to pass arithmetic results to a command. There are two forms you can use to expand an arithmetic expression and pass it to the shell: `[$expression]` or `$((expression))`. Here is an example:

```
```
$ echo "I am $[2009 - 1979] years old."
I am 30 years old.
```
```

In this example, the shell interprets the arithmetic expression first ($2009 - 1979$), and then passes that information to the `echo` command. The `echo` command displays the text, with the results of the arithmetic ($30$) inserted.