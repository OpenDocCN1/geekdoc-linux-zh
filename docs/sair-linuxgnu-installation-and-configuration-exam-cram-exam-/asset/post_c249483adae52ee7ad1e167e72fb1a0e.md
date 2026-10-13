
This chapter covers the basics of the shell, which is the Linux command-line interpreter for managing your computer. Although there are several shells available for Linux, today's standard default is the Bourne Again SHell, also known as bash. There are a number of files and commands that you can use to customize bash. This shell includes a number of useful features that help you as you work from the command line. And yes, bash also includes a number of key commands.

This chapter is closely related to Chapter 8. In this chapter, you learn the mechanics of the shell, and in Chapter 8, you learn about various commands to use with bash.

## Managing the Shell

The Bourne Again SHell (bash) is a user interface to the Linux operating system. You use bash commands to run programs, manage your files, and interact with your hardware through the Linux kernel. You can configure bash with a number of local and systemwide files and variables.

The bash shell is sometimes known as a command-line interpreter, which is a user interface that responds to specific commands, such as ls, cd, or cp. It also responds to programs or scripts that you create.

As you move around the command line, keep in mind that Linux is case sensitive. In other words, the ls command lists the files in your current directory, whereas the LS, Ls, or IS commands are meaningless in any current Linux shell.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_147_0.png)

Two advantages of the bash shell are its capability of retaining a history of previous commands and the ease with which you can complete a longer command. These characteristics are known as interactivity and command completion.

## Interactivity

You can interact with a history of Linux commands. Open a command-line interface and type the history command. If you've previously used the command-line interface, you'll see a result similar to the one shown in Figure 7.1.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_148_0.png)

Figure 7.1 Output from the history command.

By default, you can repeat previous commands in several ways: The easiest way is to use the up and down arrow keys on your keyboard. Go to your command-line interface. When you press the up arrow key, you'll see the previous commands that you used, in order. The list may even include commands that you used during previous sessions. You can reverse the process with the down arrow key.

Alternately, if you remember the first letter of a command that you recently used, you can use an exclamation point (!) to recall that earlier command. For example, if you type "!l", Linux recalls the last time you used a command that started with the letter l and runs that command. If you used more than one command that started with l you can type more letters to distinguish between commands.

## Command Completion

Linux shells allow you to use the Tab key to complete commands. With bash, you only need to type part of a command. For example, if you wanted to use the uncompress command on a compressed file, type the following letters:

```
unc
```

When you press the Tab key, bash completes the command for you. If there is more than one command in your shell that starts with unc, press the Tab key again, and you'll see a list of these commands.

## Configuring the Shell

There are two sets of configuration files for any shell. Some are systemwide; in other words, they affect all users on your Linux computer. Others are user specific and are stored in a user's home directory. Chapter 6 covered the user-specific configuration files known as .bashrc and .profile.

Depending on your distribution, there are up to four systemwide configuration files for bash: /etc/environment, /etc/profile, /etc/login, and /etc/bashrc. Within these files are two different kinds of variables: environment variables, which stay with you even if you change shells, and shell variables, which remain constant only as you navigate within a specific shell.

You can create your own shell variable; for example, you can assign the ls command to the name test, as follows:

```
test=ls
```

You can then run the ls command with the following command (note the back quotes around `$test`):

```
echo ` $test `
```

An example of an environment variable is HISTORY. The value determines the number of previous commands that are saved. For example, if you were to run the following command, your shell would remember the last 400 commands that you used:

```
HISTORY=400
```

As an environment variable, HISTORY stays with you from shell to shell.

> Environment variables are generally in uppercase letters. Shell variables may have a combination of uppercase and lowercase letters as well as numbers.

You can move to a different shell at any time. If you've installed the Korn, C, or Bourne shell on your Linux computer, you can start it with the ksh, csh, or sh command, respectively.

> You can export a shell variable. For example, if you have a shell variable named test, you can export it for use with other shells with the export test command.

## Making the Shell Work for You

There are a number of techniques that you can use with your shell. You can direct the output of one command to a file or even another command. You can set up aliases to define the commands of your choice. You can also move a running program to a background, which saves you the trouble of opening up another virtual terminal or console.

You have flexibility in the commands that you use. There are two different kinds of "wildcard" characters that help you represent more than one file. Linux allows you to use three different kinds of quote characters to manage the input to a command.

## Standard Input, Standard Output, and Standard Error

Linux consists of three data streams: data goes in, data comes out, and errors go out a different direction. These concepts are also known as standard input, standard output, and standard error.

> There are three input/output (I/O) channels: standard input (stdin), standard output (stdout), and standard error (stderr).

Standard input (stdin) comes from the keyboard to a command. For example, with the ls c* command the c* is standard input to the ls command.

Standard output (stdout) is the result of a command. For example, the files that you see after typing the ls command are standard output, which is normally directed to your monitor.

If there is no stdout, there may be a standard error (stderr) message. This is also normally directed to your monitor.

There are two basic ways to redirect stdin, stdout, and stderr. You can pipe one of these data streams to another command, or you can redirect one of these streams to or from a file.

## Redirecting Input and Output

One example of redirecting stdin is running a file full of data through a program. Let's assume you have a program called majorprogram, and your program data is typed into the program_data file. To combine these components, you would use the following command:

```
./majorprogram < program_data
```

This command directs each file name in the program_data file to majorprogram.

> The left arrow can work as well with regular commands; for example, the less < /etc/passwd command is equivalent to the less /etc/passwd command.

Similarly, you can redirect stdout. If you want to save your current list of files in a text file named currentfiles, you can use the following command:

```
ls > currentfiles
```

Alternately, if you want to save the error messages from your script named majorprogram in a file named errorlog, you can redirect the output from your script with the following command:

```
./majorprogram 2> errorlog
```

The 2> redirects stderr output. The only problem with this redirection is that every time you have a new error, it overwrites your old error in the file named errorlog. So, if you want a full list of errors, use the following command:

```
./majorprogram 2>> errorlog
```

The double arrow writes output to the end of the noted file. You can use double arrows for stdout as well. For example, every time you run the following command, your current files are added to the end of the currentfiles text file:

```
ls >> currentfiles
```

## Input and Output Pipes

As you can redirect stdin, stdout, and stderr to and from specific files, you can also pipe these data streams to other commands. If you want to review permissions on a large number of files, you might use two different commands:

```
ls -l > tempfiles
more tempfiles
```

The first command takes your current file listing and stores the result in a file named tempfiles. The second command allows you to read the tempfiles file, one screen at a time. Because your file list probably changes frequently, you should delete the tempfiles file as it becomes out of date.

Piping is convenient because it allows you to combine commands. For example, the following command does the work of the previous two:

```
ls -l | more
```

The pipe (|) takes the stdout from the ls -l command and sends the results as stdin to the more command. You don't need to create or delete any files, like tempfiles.
