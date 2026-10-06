```
$ cat read1
echo -n "Go ahead: "
read firstline
echo "You entered: $firstline"
$ read1
Go ahead: This is a line.
You entered: This is a line.
```

The first line of the read1 script uses echo to prompt the user to enter a line of text. The -n option suppresses the following NEWLINE, allowing you to enter a line of text on the same line as the prompt. The second line in read1 reads the text into the variable firstline. The third line verifies the action by displaying the value of firstline. The variable is quoted (along with the text string) in this example because you, the script, cannot anticipate what characters the user might enter in response to the prompt. Consider what would happen if the variable were not quoted and the user * in response to the prompt:

```
$ cat read1_no_quote
echo -n "Go ahead: "
read firstline
echo "You entered: $firstline"
$ read1_no_quote
Go ahead: *
You entered: read1 read1_no_quote script.1
$ ls
read1 read1_no_quote script.1
```

The ls command lists the words as the script, demonstrating that the shell expands the asterisk into a list of all the files in the working directory. When the variable $firstline is surrounded by double quotation marks, the shell does not expand the asterisk. Thus the read1 script behaves correctly:

```
$ read1
Go ahead: *
You entered: *
```

If you want the shell to interpret the special meanings of special characters, do not use quotation marks.

The read2 script prompts for a command line and reads it into the variable command. The script then executes the command line by placing $command on a line by itself. When it executes the script, the shell replaces the variable with its value and executes the command line as part of the script:

```
$ cat read2
echo -n "Enter a command: "
read command
$command
echo Thanks
```