# Part III: Advanced Shell Scripting

Instead of using a semicolon to separate the commands, you can use the secondary prompt in the Bash shell. Just enter the first single quotation mark to open the `sed` program script (also called the `sed` editor command list), and Bash continues to prompt you for more commands until you enter the closing quotation mark:

```
```
$ sed -g '
> s/brown/green/
> s/fox/toad/
> s/dog/cat/' data1.txt
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
```

```

You must remember to finish the command on the same line where the closing single quotation mark appears. After the Bash shell detects the closing quotation mark, it processes the command. After it starts, the `sed` command applies each command you specified to each data line in the text file.

# Reading editor commands from a file

Finally, if you have lots of `sed` commands you want to process, it is often easier to store them in a separate file. Use the `-f` option to specify the file in the `sed` command:

```
```
$ cat script1.sed
s/brown/green/
s/fox/toad/
s/dog/cat/

$ sed -f script1.sed data1.txt
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
```

```

In this case, a semicolon is *not* placed after each command. The `sed` editor knows that each line contains a separate command. As with entering commands on the command line, the `sed` editor reads the commands from the specified file and applies them to each line in the data file.

![](bbox=[0.08, 0.82, 0.92, 0.89])

You’ll look at some other `sed` editor commands that come in handy for manipulating data in the “Looking at the `sed` Editor Basic Commands” section. Before that, let’s quickly look at the other Linux data editor.