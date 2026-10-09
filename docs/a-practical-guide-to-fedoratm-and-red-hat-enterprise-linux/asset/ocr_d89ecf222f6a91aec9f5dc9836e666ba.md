```
```
$ cat read1_no_quote
read -p "Go ahead: " firstline
echo You entered: $firstline

$ ./read1_no_quote
Go ahead: *
You entered: read1 read1_no_quote script.1
$ ls
read1 read1_no_quote script.1
```
```

The `ls` command lists the same words as the script, demonstrating that the shell expands the asterisk into a list of files in the working directory. When the variable $firstline is surrounded by double quotation marks, the shell does not expand the asterisk. Thus the `read1` script behaves correctly:

```
```
$ ./read1
Go ahead: *
You entered: *
```
```

When you do not specify a variable to receive `read`’s input, `bash` puts the input into the variable named `REPLY`. The following `read1b` script performs the same task as `read1`:

```
```
$ cat read1b
read -p "Go ahead: "
echo "You entered: $REPLY"
```
```

The `read2` script prompts for a command line, reads the user’s response, and assigns it to the variable `cmd`. The script then attempts to execute the command line that results from the expansion of the `cmd` variable:

```
```
$ cat read2
read -p "Enter a command: " cmd
$cmd
echo "Thanks"
```
```

In the following example, `read2` reads a command line that calls the `echo` builtin. The shell executes the command and then displays **Thanks**. Next `read2` reads a command line that executes the `who` utility:

```
```
$ ./read2
Enter a command: echo Please display this message.
Please display this message.
Thanks
$ ./read2
Enter a command: who
max    pts/4    2013-06-17 07:50 (:0.0)
sam    pts/12   2013-06-17 11:54 (guava)
Thanks
```
```

If `cmd` does not expand into a valid command line, the shell issues an error message:

```
```
$ ./read2
Enter a command: xxx
./read2: line 2: xxx: command not found
Thanks
```
```