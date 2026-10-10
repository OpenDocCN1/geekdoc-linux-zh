
## Exit Status

Most programs in FreeBSD return an exit status when they terminate. The exit status is usually 0 if successful, and some number other than 0 if something went wrong. Some programs will return a different exit status, depending on the problem. Often, this information can be found in the program's man page.

The exit status of the last program that ran is stored in the magic variable $?. Here are a couple of examples:

```
bash$ ls > /dev/null
bash$ echo $?
0
bash$

bash$ ls -2 /dev/null
ls: illegal option - - 2
usage: ls [-ABCDFGHLOPRSTWabcfgiklnopqrstux] [file ...]
bash$ echo $?
1
bash$
```

The first example will set the magic variable $? to 0, as shown (the output of the ls command was redirected to /dev/null for brevity in the example). The second example, however, supplies an illegal option to ls. The command fails with an error message, and $? is set to 1.

You can use this exit status to make automatic decisions in your shell programs. The previous logical AND/OR example already introduced this to an extent. It showed how the success or failure of one command can determine whether the next one is executed. The logical AND/OR statement used in the previous section could also have been written as an if statement, like this:

```
if tar cvfz backup.tar.gz documents/2000/*
then
rm -r documents/2000
else
echo "Archive operation failed"
fi
```

This example combines the two examples from the previous section. The if statement reads the exit status of the tar command. If the exit status is 0, the then statements are performed, and the directory that was archived is removed. If the exit status is some number other than 0, the then statements are not performed, and the else statements are performed instead.

Another useful application of this property is with the test command. You’ve already seen how to use the test command with mathematical expressions. Another useful application of test is to check for the existence of AND/OR properties of a file, as in this example:

```text
if [ -f program.conf ]
then
    ; # do nothing
else
    touch program.conf
fi
```

This example checks for the existence of the file program.conf. If the file exists, 0 is returned and the then statement is executed. In this case, the then statement does nothing. (The colon tells it to do nothing. The rest of the line is a comment.) If the file does not exist, 1 is returned and the else statement is performed, which uses the touch command to create the file.

The test command can test for more than just the existence of a file. It can also test the attributes and type of file. Table 12.3 is a list of all the options to the test command and what they mean.

TABLE 12.3 Testing File Attributes in Shell Programs

| Option | Action |
| :--- | :--- |
| -f | The file exists and is a normal file. |
| -d | The file exists and is a directory. |
| -s | The file exists, and its size is greater than zero. |
| -c | The file exists and is a character special file. |
| -b | The file exists and is a block special file. |
| -r | The file exists and is readable. |
| -w | The file exists and is writable. |
| -x | The file exists and is executable. |
| -d | The file exists and is a directory. |

## Setting Exit Status

Most of the scripts in this chapter have set the exit status, and by now you have a pretty good idea of what the exit status is used for. You have also seen that the exit statement is used to set the exit status. If you do not specifically set the exit status, your program will return the exit status of the last command that ran. When you do set the exit status, whatever you set will be stored in the $? variable, just like the exit status of any other program. Also, just like any other program, the exit status of your shell program can be read by other programs to make a decision about what to do next. This can be useful if you are calling a shell program from another shell program, for example.

Also, remember that you are not limited to just 0 and 1 for exit statuses. You can use many more exit statuses. Always use 0 for a successful exit and numbers other than 0 for an error exit. You can use several different exit statuses in the same program to handle different error conditions, and then the calling program can act accordingly. Here is an example of some code that uses multiple exit statuses:

```
if [ ! -r program.conf ]
then
    : # do nothing
else
    exit 1
fi

if [ `touch /tmp/program.lock` ]
then
    : # do nothing
else
    exit 2
fi

# main program statements here
exit 0
```

The preceding example first checks to see whether it can read the file *program.conf*. If it can, the program continues to the next *if* test. If it can't, the program exits immediately with an exit status of 1. If the program was able to read the *program.conf* file, it will then attempt to create the */tmp/program.lock* file. If it can, the program continues. If it can't, the program exits immediately with an exit status of 2. Finally, assuming that both operations succeed, the program will continue with the main part of the program and then exit with a status of 0. This program could be called from another program and then return its exit status to that program. The calling program could then make decisions based on the exit status it received from this program.

## Exit Traps

As you know, programs in FreeBSD can be terminated by sending them various “kill” signals and with various combinations of keyboard commands (Ctrl+C, for example). (See the “Terminating Misbehaving Processes” section of Chapter 13, “Performance Monitoring, Process Control, and Job Automation” for more on the *kill1* command and its signals.) The problem with this is that if, for example, a program creates temp files, and the user interrupts the program with Ctrl+C before it has finished running, the program will not clean up after itself and will leave its temp files laying around on the disk, thus wasting space.

Fortunately, the shell provides a way to trap these types of interrupts. Here is a short sample program that demonstrates the use of trapping interrupts:

```
#!/bin/sh

# Program that demonstrates trapping interrupts
trap 'echo "Interrupt received. Quitting." 1>&2' 1 2 3 15
echo -n "Enter a number: "
read num
exit 0
```

Basically, this program sets a trap for interrupts 1, 2, 3, and 15. The actions performed by the trap are located between the single quotes. If you run this program and press Ctrl+C at the prompt that asks you to enter a number, it will send signal 2 (INT) to the program, which will set off the trap and cause the message “Interrupt received” to be printed. Then, the program will exit.

You also can use the *echo* command in the task of shell output redirection. The 1>&2 in the *echo* statement redirects the output of the *echo* command to *STDERR*. This ensures that the output of the command will not accidentally be sent down a pipe to another command or redirected to another location along with the rest of the program’s output. It is a good idea any time you create error messages to send the output to *STDERR* with 1>&2.

Normally, of course, you would use the traps to do things such as clean up temp files and such. If you need to do a lot of things in a trap, it is better to make the trap a function (functions will be covered later in the chapter).

If you want to prevent the user from being able to exit the program with Ctrl+C, you can set a trap and leave the action null, like so:

```
trap '' 2
```

This line causes signal 2 to be completely ignored.

Your program can have more than one trap, and different things can be done, depending on how the program has exited. A trap for signal 0 will be set off on all exits, normal or otherwise.

A trap for other signals will be set off only when one of those signals occurs. Table 12.4 provides a list of the most common signals you might want to trap.

TABLE 12.4 Common Interrupt Signals and Their Actions

| Interrupt Signal | Action |
| :--- | :--- |
| 0 | Exit |
| 1 | HUP—Session hangup (or disconnect) |
| 2 | INT—Interrupt (Ctrl+C) |
| 3 | QUIT—Quit (Ctrl+) |
| 15 | TERM—A normal kill command |
