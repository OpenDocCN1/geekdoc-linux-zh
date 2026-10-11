tr changes the word Halloween to Halloween when displaying myfile to your screen. tr also can be used to encrypt your file using the rotate 13 method. This replaces the first letter of the alphabet with the 13th, the second with the 14th, and so on. An example is

```
tr '[A-M][N-Z][a-m][n-z]''[N-Z][A-M][n-z][a-m]'
```

As you can see, you can use ranges of characters enclosed in square brackets as part of your string. Notice that single quotes are needed because of the special characters.

# wc

The wc utility will tell you the number of words, lines, or characters in a file. Its syntax is

```
wc [options] [filename(s)]
```

If you specify multiple files, the number of words, lines, and characters will be displayed for each file followed by the sum total of words, lines, and characters.

You can use the -c option to display only the number of characters -w to display the number of words, and -l to display the number of lines.

So, if you called wc with days and mwmich listed as filenames, the output would be

```
6      8       68 days
5      17      101 mwmich
11     25      169 total
```

To display the number of lines in days without showing the file's name, you could type

```
wc -l < days
```

# Input and Output

Almost every command can get information passed to it by way of standard input (stdin). This usually is via the terminal, such as when you type a command. However, input also can come from a file.

In addition, each command has two types of output: standard output (stdout) and standard error (stderr). stdout is the results of the command, whereas stderr is where any error messages are sent. By default, both of these are directed to the display, but either or both of these streams can be redirected to a file.

The shell manages how standard input and standard output are handled. By default, your shell directs standard output and standard error from the command to the device file, which is associated with your terminal and causes it to appear on your display. In the same manner, the shell directs standard input from your terminal, or keyboard, to the command.