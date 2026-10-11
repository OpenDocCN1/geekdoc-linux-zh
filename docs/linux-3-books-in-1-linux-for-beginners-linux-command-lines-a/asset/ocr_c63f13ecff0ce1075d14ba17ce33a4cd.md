# Chapter Five

# Redirection Commands &
Keyboard Tricks with Linux Commands

In this chapter, we will talk about the coolest feature of the command line, which is called I/O redirection. The I/O stands for input/output. With this facility, you may redirect the input and output of commands and connect multiple commands to make a powerful command known as pipelines.

The output of a program is of two types. First, you have the result of the program which contains the data program produces. Secondly, there are status and error messages that instruct you how the program is getting along. If you look at the command ls, you will see that it delivers results and error messages on your screen.

This program sends the output to another file called standard error. Both standard error and output are connected to the screen, and they are saved into a disk file. Many programs take input from a facility known as standard input stdin, which is attached to a keyboard.

I/O redirection allows you to change where the output goes and where the input flows in from. Usually, output goes to the screen, and the input flows in from the keyboard in Linux; I/O has the power to change that.

# Redirection

I/O redirection helps you in redefining the direction of the output. To redirect the standard output to a file instead of the screen, you have to use the redirection operator that is followed by the name of the file. It is useful more often to store the output of a certain command inside a file. You may tell the shell to direct the ls command's output to a file namedls-output.txt instead of the screen.

```
[gha@localhost ~]$ ls -l /usr/bin > ls-pt.txt
```