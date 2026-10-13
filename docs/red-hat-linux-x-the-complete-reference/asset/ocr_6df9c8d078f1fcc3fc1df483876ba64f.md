# Command Line Interface

When using the command line interface, you are given a simple prompt at which you type in your command (see Chapter 8). Even with a GUI, you sometimes need to execute commands on a command line. Linux commands make extensive use of options and arguments. Be careful to place your arguments and options in their correct order on the command line. The format for a Linux command is the command name followed by options, and then by arguments, as shown here:

```
$ command-name options arguments
```

An option is a one-letter code preceded by one or two hyphens, which modifies the type of action the command takes. Options and arguments may or may not be optional, depending on the command. For example, the ls command can take an option, -s. The ls command displays a listing of files in your directory, and the -s option adds the size of each file in blocks. You enter the command and its option on the command line as follows:

```
$ ls -s
```

An argument is data the command may need to execute its task. In many cases, this is a filename. An argument is entered as a word on the command line after any options. For example, to display the contents of a file, you can use the more command with the file's name as its argument. The more command used with the filename mydata would be entered on the command line as follows:

```
$ more mydata
```

The command line is actually a buffer of text you can edit. Before you press ENTER, you can perform editing commands on the existing text. The editing capabilities provide a way to correct mistakes you may make when typing in a command and its options. The BACKSPACE and DEL keys let you erase the character you just typed in. With this character-erasing capability, you can BACKSPACE over the entire line if you want, erasing what you entered. CTRL-U erases the whole line and enables you to start over again at the prompt.

Tip
You can use the UP ARROW key to redisplay your last-executed command. You can then reexecute that command, or you can edit it and execute the modified command. This is helpful when you have to repeat certain operations over and over, such as editing the same file. This is also helpful when you've already executed a command you entered incorrectly.