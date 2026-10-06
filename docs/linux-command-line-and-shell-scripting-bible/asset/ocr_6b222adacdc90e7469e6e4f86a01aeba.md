The command line options provide an easy way to customize features in the awk program.

# Using gawk

You can use awk either directly from the command line or from within your shell scripts. This section demonstrates how to use the gawk program, and how to enter scripts for awk to process.

# Reading the program script from the command line

A awk program script is defined by an opening and closing brace. You must place script commands between the two braces. Since the awk command line assumes that the script is a single text string, you must also enclose your script in single quotation marks. Here's an example of a simple gawk program script specified on the command line:

```
$ gawk '(print $1)'
```

This script will display the first data field in every line of the input stream.

# Using multiple commands in the program script

A programming language wouldn't be very useful if you could only execute one command. The awk programming language allows you to combine commands into a normal program. To use multiple commands in the program script specified on the command line, just place a semicolon between each command:

```
$ echo "My name is Rich" | gawk '$(4="Dave"; print $0)'
My name is Dave
```

The script performs two commands: first it replaces the fourth data field with a different value, then it displays the entire data line in the stream.

# Reading the program from a file

Just as with the sed editor, the awk editor allows you to store your programs in a file and refer to them in the command line:

```
$ script2
( print $5 "'s userid is " $1 )
$ gawk -F: -f script2 /etc/passwd
```

The awk program processes all of the commands specified in the file on the input stream.