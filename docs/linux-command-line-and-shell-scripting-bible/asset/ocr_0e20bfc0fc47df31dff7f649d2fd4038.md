# Introducing sed and gawk

To terminate the gawk program, you must signal that the data stream has ended. The bash shell provides a key combination to generate an End-of-File (EOF) character. The Ctrl-D key combination generates an EOF character in bash. Using that key combination terminates the gawk program and returns you to a command line prompt.

# Using data field variables

As I mentioned, one of the primary features of gawk is its ability to manipulate data in the text file. It does this by automatically assigning a variable to each data element in a line. By default, gawk assigns the following variables to each data field it detects in the line of text:

+   $0 represents the entire line of text.
$1 represents the first data field in the line of text.
$2 represents the second data field in the line of text.
$n represents the nth data field in the line of text.

Each data field is defined in a text by a field separation character. When gawk reads a line of text, it delineates each data field using the defined field separation character. The default field separation character in gawk is a whitespace character (such as the tab or space characters).

To demonstrate this, here's an example gawk program that reads a text file and displays only the first data value:

```
$ cat data3
One line of test text.
Two lines of test text.
Three lines of test text.
$ awk '{print $1}' data3
One
Two
Three
$
```

This program uses the $1 field variable to display only the first data field for each line of text.

If you're reading a file that uses a different field separation character, you can specify it by the -F option:

```
$ awk -F: '{print $1}' /etc/passwd
root
bin
daemon
adm
lp
sync
shutdown
halt
...
```