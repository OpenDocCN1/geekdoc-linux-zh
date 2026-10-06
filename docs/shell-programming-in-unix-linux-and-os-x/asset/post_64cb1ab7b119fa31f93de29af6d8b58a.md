
As an example, recall that executing the who command results in the display of all users that are currently logged-in. More formally, the who command writes a list of the logged-in users to standard output. This is depicted in Figure 1.10.

![](img/dc544c8aef1333b25eff1c794c2e5ec2_48_0.png)

Figure 1.10 who command

It turns out that just about every single Unix command can take the output of a previous command or file as its input too, and can even send its output to another command or program. This concept is hugely important to understanding the power of the command line and why it's so helpful to know all of these commands even when a graphical interface might be also available for your use.

Before we get there, however, consider this: if the sort command is invoked without argument, the command takes its input from standard input. With standard output, this is your terminal (or keyboard) by default.

When input is entered this, an end-of-file sequence must be specified after the last line is typed, and by Unix convention, that Ctrl+d; is the sequence produced by simultaneously pressing the Control (or Ctrl, depending on your keyboard) key and the d key.

As an example, let's use the sort command to sort the following names: Tony, Barbara, Harry, Dirk. Instead of first entering the names into a file, we'll enter them directly from the terminal:

```
$ sort
Tony
Barbara
Harry
Dirk
Ctrl+d
```

Barbara
Dirk
Harry
Tony

Because no filename was specified to the sort command, the input was taken from standard input. After the fourth name was typed, the Ctrl and d keys were pressed to signal the end of the data. At that point, the sort command sorted the four names and displayed the results on the standard output device, which is also the terminal. This is depicted in Figure 1.11.

![](img/dc544c8aef1333b25eff1c794c2e5ec2_49_0.png)

Figure 1.11 sort command

The wc is another example of a command that takes its input from standard input if no filename is specified on the command line. The following shows an example of this command used to count the number of lines entered from the terminal:

```
$ wc -l
This is text that
is is typed on the
standard input device.
Ctrl+d
```

Note that the Ctrl+d is used to terminate the input is not counted as a separate line by the wc command because it's interpreted by the shell, not handed to the command. Furthermore, because the -l flag was specified to the wc command, only the count of lines (3) is presented as the output of the command.

## Output Redirection

The output from a command normally intended for standard output can be easily “diverted” to a file. This capability is known as output redirection and is also essential to understanding the power of Unix.

## Standard Input/Output, and I/O Redirection

If notation > file is appended to any command that normally writes its output to standard output, the output of that command will be written to the file instead:

```
$ who > users
```

This command causes the who command to be executed and its output to be written into the file. Notice that no output appears. This is because the output has redirected from the default standard output device (the terminal) into the file. We can check this, of course:

```
$ cat users
tty01 Sep 12:30
tty15 Sep 12:13
tty21 Sep 12:10
tty24 Sep 12:07
tty25 Sep 12:03
```

If a command has its output redirected to a file and the file already contains some data, that data will be overwritten.

```
$ echo line 1 > users
cat users
1
```

But consider this example, remembering that users already contain the output of the earlier command:

```
$ echo line 2 >> users
cat users
line 1
line 2
```

If you're paying attention you will notice that this echo command uses a different type of output redirection, indicated by the characters >>. This character causes the standard output from the command to be appended to the contents of the file. The previous contents are not lost; the new output simply gets added to the end. By using the redirection >> you can use cat to append the contents of file onto the end of another:

```
$ cat file1
This is in file1.
$ cat file2
This is in file2.
$ cat file1 >> file2
$ cat file2
This is in file2.
This is in file1.
```

## Append file1 to file2

## Chapter 1 A Quick Review of the Basics

Recall that specifying more than one filename to cat results in the display of the first file followed immediately by the second file, and so on. This means there is a second way to accomplish the same result:

```
$ cat file1
This is in file1.
$ cat file2
This is in file2.
$ cat file1 file2
Redirect to instead
$ cat file3
This is in file1.
This is in file2.
```

In fact, that's where the command gets its name: When used with more than one file, the effect is to concatenate the files together.

## Input Redirection

Just as the output of a command can be redirected to a file, as the greater-than character > is used for output redirection, the less-than character < is used to redirect the input of a command. Of course, commands that normally take their input from standard input can have input redirected from a file in this manner.

To redirect input, use the < followed by the name of the file that the input is to be read from. To count the number of lines in the file users, for example, you already know that you can execute the command wc -l users:

```
$ wc -l users
2
```

It turns out that you can also count the number of lines in the file by redirecting standard input for the wc command:

```
$ wc -l < users
2
```

Note that there is a difference in the output produced by the two forms of the wc command. In the first case, the name of the file users is listed with the line count; in the second case, it is not. This points out a subtle distinction in the execution of the two commands. In the first case, wc knows that it is being fed input from the file users. In the second case, it only sees the raw data which is being fed to standard input. The shell redirects the input so that it comes from the file users and not the terminal (more about this in the next chapter). As far as wc is concerned, it doesn't know whether its input is coming from the terminal or from a file, so it can't report the filename!

## Pipes

As you will recall, the file users that was created previously contains a list of all the users currently logged in to the system. Because you know that there will be one line in the file for each user logged in to the system, you can easily determine the *number* of login sessions by counting the number of lines in the *users* file:

```
$ who > users
$ wc -l < users
5
```

This output indicates that currently five users are logged in or that there are five login sessions, the difference being that users, particularly administrators, often log in more than once. Once you have a command sequence you can use whenever you want to know how many users are logged in.

Another approach to determine the number of logged-in users bypasses the intermediate file. As referenced earlier, Unix lets connect two commands together. This connection is known as a pipe, and it enables you to take the output from one command and feed it directly into the input of another. A pipe is denoted by the character |, which is placed between the two commands. To create a pipe between the who and wc -l commands, you type

```
$ who | wc -l
5
```

The pipe that is created between these two commands is depicted in Figure 1.12.

![](img/dc544c8aef1333b25eff1c794c2e5ec2_52_0.png)

Figure 1.12 Pipeline process: who | wc -l

## Chapter 1. A Quick Review of the Basics

A pipe is established between two commands, the standard output from the first command is connected directly to the standard input of the second command. You know that the who command writes its list of logged-in users to standard output. Furthermore, you know that if no filename argument is specified to the wc command, it takes its input from standard input. Therefore, the list of logged-in users that is output from the who command automatically becomes the input of the wc command. Note that you never see the output of the who command at the terminal because it is piped directly into the wc command. This is depicted in Figure 1.13.

![](img/dc544c8aef1333b25eff1c794c2e5ec2_53_0.png)

Figure 1.13 Pipeline process

A pipe can be made between any two programs, provided that the first program writes its output to standard output, and the second program reads its input from standard input.

As another example, suppose you wanted to count the number of files contained in your directory. Knowledge of the fact that the ls command displays one line of output per file enables you to use the same type of approach as before:

```
$ ls | wc -l
  10
```

The output indicates that the current directory contains 10 files.

It is also possible to create a more complicated pipeline that consists of more than two programs, with the output of one program feeding into the input of the next. As you become a more sophisticated command line user, you'll find many situations where pipelines can be tremendously powerful.
