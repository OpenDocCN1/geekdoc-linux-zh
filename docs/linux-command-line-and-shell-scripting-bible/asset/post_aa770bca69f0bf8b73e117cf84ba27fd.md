
in the output file. The bash shell automatically gives error messages a higher priority than the standard output. This allows you to view the error messages together, rather than scattered throughout the output file.

## Redirecting Output in Scripts

You can use the STDOUT and STDERR file descriptors to produce output in multiple locations by redirecting the appropriate file descriptors. There are two methods for redirecting output in the script:

- Temporarily redirecting each line
- Permanently redirecting all commands in the script

The following sections describe how each of these methods work.

## Temporary redirections

If you want to purposely generate error messages in your script, you can redirect an individual output line to STDERR. All you need to do is use the output redirection symbol to redirect the output to the STDERR file descriptor. When you redirect to a file descriptor, you must precede the file descriptor number with an ampersand sign (&):

```bash
echo "This is an error message" >&2
```

This line displays the text wherever the STDERR file descriptor for the script is pointing, instead of the normal STDOUT. Here's an example of a script that uses this feature:

```bash
$ cat test8
#!/bin/bash
# testing STDERR messages
echo "This is an error" >&2
echo "This is normal output"
$
```

If you run the script as normal, you won't notice any difference:

```bash
$ ./test8
This is an error
This is normal output
$
```

Remember, by default Linux directs the STDERR output to STDOUT. However, if you redirect STDERR, any text directed to STDERR in the script will be redirected:

```bash
$ ./test8 2> test9
This is normal output
```

```bash
$ cat test9
This is an error
$
```

Perfect! The text that's displayed using STDOUT appears on the monitor, while the echo statement text to STDERR is redirected to the output file.

This method is great for generating error messages in your scripts. If someone uses your scripts, they can easily redirect the error messages using the STDERR file descriptor, as shown.

## Permanent redirections

If you have lots of data that you are redirecting in your script, it can get tedious having to redirect every echo statement. Instead, you can tell the shell to redirect a specific file descriptor for the duration of the script by using the exec command:

```bash
$ cat test10
#!/bin/bash
# redirecting all output to a file
exec 1>testout
```

```bash
echo "This is a test of redirecting all output"
echo "from a script to another file."
echo "without having to redirect every individual line"
../test10
```

```bash
$ cat testout
This is a test of redirecting all output
from a script to another file.
without having to redirect every individual line
$
```

The exec command starts a new shell, and redirects the STDOUT file descriptor to a file. All output in the script that goes to STDOUT is instead redirected to the file.

You can also redirect the STDOUT in the middle of a script:

```bash
$ cat test11
#!/bin/bash
# redirecting output to different locations
exec 2>tesror
```

```bash
echo "This is the start of the script"
echo "now redirecting all output to another location"
```

```bash
exec 1>testout
```

```bash
echo "This output should go to the testout file"
echo "but this should go to the tester file" >&2
../test11
```

## Part II Shell Scripting Basics

This is the start of the script
now redirecting all output to another location
$ cat testout
This output should go to the testout file
$ cat testerror
but this should go to the testerror file
$

The script uses the exec command to redirect any output going to STDERR. Next, the script uses the echo statement to display a few lines to STDOUT. After that, the exec command is used again to redirect STDOUT to the testout file. Notice that when STDOUT is redirected, you can still specify the output from an echo statement to go to STDERR, which in this case is still redirected to the testerror file.

This feature can come in handy when you want to redirect the output of just parts of a script to an alternative location, such as an error log. There's just one problem you'll run into when using this.

Once you redirect STDOUT or STDERR, you cannot easily redirect them back to their original location. If you need to switch back and forth with your redirection, there's a trick you'll need to learn. The "Creating Your Own Redirection" section later in this chapter discusses what this trick is and how to use it in your shell scripts.

## Redirecting Input in Scripts

You can use the same technique to redirect STDOUT and STDERR in your scripts to redirect STDIN from the keyboard. The exec command allows you to redirect STDIN to a file on the Linux system:

```bash
exec 0< testfile
```

This command informs the shell that it should retrieve input from the file testfile instead of STDIN. This redirection applies anytime the script requests input. Here's an example of this in:

```bash
$ test12
#!/bin/bash
# redirecting file input

exec 0< testfile
count=1

while read line
do
  echo "Line #$count: $line"
  count=$[$ count + 1 ]
done
```

320

```bash
$ ./test12
Line #1: This is the first line
Line #2: This is the second line
Line #3: This is the third line
$
```

This example shows how to use file input in a script. The `while` loop reads the file line by line and processes each one. The `count` variable is used to keep track of the line number.

This technique is useful when you need to process data stored in a file instead of typing it manually. It's a common requirement in shell scripting.

## Creating Your Own Redirection

As mentioned earlier, there is a trick to redirect a file descriptor back to its original location. This is done using the process substitution feature. Here is an example of how it works:

```bash
$ cat test13
#!/bin/bash
# redirecting STDOUT to a file and then back
exec 1>testout
echo "This goes to the file"
exec 1>&1
echo "This goes back to the monitor"
```

```bash
$ cat testout
This goes to the file
$
This goes back to the monitor
$
```

The `1>&1` command tells the shell to point file descriptor 1 to the current location of file descriptor 1. This is the key to reversing the redirection.
