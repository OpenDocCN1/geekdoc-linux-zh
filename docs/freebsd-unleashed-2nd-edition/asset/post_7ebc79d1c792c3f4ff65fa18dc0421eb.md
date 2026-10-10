
## Functions

Functions are basically groups of statements that can be called with a single command. They can almost be thought of as “mini-programs inside other programs.” Using functions in your shell programs can make your life a lot easier—for two reasons. First of all, if you need to perform the operation in multiple places in your program, you can simply type the name of the function rather than having to retype all the code each time you need to perform the operation. Second, if you later decide you need to make the operation work differently, you only have to change the function rather than go through the code and change it every place it is used. The following example demonstrates how a function is created; it shows a simple function that cleans up temp files, and so on, after a shell program exits. It then shows how to call the function:

```bash
#!/bin/sh
on_exit() {
    rm -rf /tmp/myprogram.*
    mv logfile logfile.old
    mail foo@bar.com < report.txt
}
trap on_exit 0 1 2 3 15
```

This function is given a name, followed by parentheses and a left bracket. Everything between the two brackets is the body of the function. The function can then be called as if it were a program, simply by using its name. As stated previously, functions can almost be thought of as “mini-programs inside other programs.” Any time you type the name of this function, the statements between its brackets will be performed.

There is one important difference between calling a function and calling another program, though. The function is run in the current shell, whereas a separate program starts in a subshell. This means that a function can modify the variables and environment variables in the program that calls it. But a separate program called from inside a shell program cannot modify any of the variables or environment variables in the calling program.

## File Descriptors

File descriptors are numbered IDs that are set up each time the kernel starts a process. These numbers are what the process uses to write output and read input. Three file descriptors are opened by default:

> **NOTE**
> You can trap signal 15 (the default signal sent by the kill command). You can also trap most other signals that can be sent by the kill command. However, you cannot trap signal 9 (SIGKILL). SIGKILL is used as a last resort to terminate a program when all other methods have failed. Therefore, it cannot be trapped and cannot be ignored.

| File Descriptor | Meaning |
| :--- | :--- |
| F.D. 0 | STDIN. This is where standard input comes from. This is normally the keyboard, but it can be redirected to read from a file or some other source. |
| F.D. 1 | STDOUT. This is where standard output goes. It is normally the screen, but as you have seen it can be redirected. |
| F.D. 2 | STDERR. This is where standard error messages go. Once again, this is normally the screen, but it can also be redirected. |

File descriptors can be used in shell programs to make your programs both more efficient and easier to write. The exec command can be used to open a file descriptor. Here is an example of how file descriptors can make your programs both easier to write and more efficient:

```bash
#!/bin/sh
# open a file descriptor on F.D. 1 (STDOUT)
exec > testfile.txt
# echo some stuff to STDOUT which will now go to the file testfile.txt
echo "Line 1 of the file"
echo "Line 2 of the file"
echo "Line 3 of the file"
echo "Line 4 of the file"
echo "Line 5 of the file"
exit 0
```

The exec statement in the second line of the preceding code example causes testfile.txt to be opened as STDOUT. As a result, all the echo lines are set to the file testfile.txt instead of to the screen, even though the output is not redirected in the echo statements. If you have a lot of things that need to be written to a file, this is more efficient than using shell redirection each time. It is also easier to code because you don't have to redirect the output each time.

This is also very useful when opening a file descriptor for STDIN and using read. Here is an example:

```bash
#!/bin/sh
# open a file descriptor on F.D. 0 (STDIN)
exec < testfile.txt
while read string
do
    echo $string
done
```

Assuming that you still have the file *testfile.txt* from the previous example, this example will output the following:

```text
Line 1 of the file
Line 2 of the file
Line 3 of the file
Line 4 of the file
Line 5 of the file
```

So, what is so great about this? It demonstrates the important concept of using a file descriptor with *read*. Because the file is not closed between each call to *read*, *read* remembers the last line it read and moves the pointer to the next line in the file. This way, *read* will read each line of the file in sequence automatically.

## Debugging Shell Scripts

If you write shell scripts of any complexity at all, sooner or later bugs are going to creep in. Although there is no full-fledged debugger for the shell, it does provide some primitive debugging capabilities in the form of being able to trace each action that is performed. You turn on the tracing by adding *-xv* to the end of the `#!/bin/sh` line in your script, so it looks like this:

```bash
#!/bin/sh -xv
```

The *-x* switch means for the shell to print every command, preceded by a plus sign (+), to *STDERR*. The *-v* switch puts the shell in verbose mode. This has the effect of causing the script to write out everything it does to the error file descriptor so that you can debug more easily.

This works best if you pipe the output to *more* or *less* so that it doesn’t scroll off the screen faster than you can read it—and also if you redirect both *STDOUT* and *STDERR* to the same place so that you can see both the output of the script and the errors. Enter this simple example into a file called *xvtest* and set it executable:

```bash
#!/bin/sh -xv
# Demonstrate the use of tracing in shell script debugging
result=`echo "2 * 12 / (2 + 2)" | bc`
echo $result
exit 0
```

To execute this program so that you will see both *STDOUT* and *STDERR* and pipe the output to *more*, use the following command:

```bash
./xvtest 2>&1 | more
```

The program will produce the following output:

```text
1. ./xvtest 2>&1 | more
2. #!/bin/sh -xv
3. # Demonstrate the use of tracing in shell script debugging
4. result=`echo "2 * 12 / (2 + 3)" | bc`
5. + echo 2 * 12 / (2 + 3)
6. + bc
7. + result=4
8. echo $result
9. + echo 4
10. 4
11. exit 0
12. + exit 0
```

You can now see everything that this program did. The lines with plus signs (+) in front of them are the results of actions in the program. For example, line 3 in the preceding example assigns the results of a calculation to the variable `result`. Lines 4, 5, and 6 show the actions that were taken. Line 4 shows the `echo` command, line 5 shows the execution of `bc`, and line 6 shows the variable assignment, where 4 is assigned to the variable `result`.

This example also shows how variable expansion works. Notice lines 8, 9, and 10. In line 8, the `echo` statement is read. In line 9, the variable is expanded so that the `echo` statement becomes "echo 4". Then, in line 10, the actual output of the `echo` statement is produced.

## Advanced Features of Korn Shell Scripting

The Korn shell contains some advanced features that can make shell programming easier and more powerful, such as built-in arithmetic and arrays. You should think carefully before using these features in a script, however, because virtually every Unix system can run a Bourne shell script, but some will not be able to run a Korn shell script. If such a script is highly specialized—requiring the advanced features of the Korn shell—and will be run only on your local system or on systems that have the Korn shell available, using this script won't present any problems. If you are writing a shell script for public consumption, however, or if this script will run on multiple systems within your organization and you cannot be sure which shells will be available on those systems, you are better off sticking to plain-old Bourne script.

That being said, this section will cover some of the advanced features of Korn shell scripting.
