# Chapter 20: Basic Shell Scripting

# Introduction

The *previous chapter* discussed administering your computer via shell commands. You will find that frequently multiple commands are used together to accomplish some tasks. For example, if you really want to get a picture of your computer's performance, you might use several different shell commands to get a complete view of your system. Normally, shells are interactive. This means that a shell will accept a command from you via your keyboard and execute that command. If you use certain commands on a routine basis, it can be tedious to retype the same series of commands each time you need them. You can store this sequence of commands to a text file and instruct the shell to execute this text file instead of entering the commands. This is what is known as a *shell script*.

Windows has something quite similar to this, although it is not used much anymore. In Windows you can use a standard text editor to create what is called a *batch file* and execute that file from the command prompt. Batch files were very popular when DOS and Windows 3.1 were the current operating systems, but they have fallen out of use in recent years. So that you understand the concept, let's examine how to write a simple batch file in Windows.

The first step is to open Notepad and enter the following lines:

```
```
cd\windows
dir *.log
cd\
```
```

These are the commands to change directories to the `windows` directory, list all files that end with `.log`, and then change back to the root directory (`c:\`). Then choose *File* and *Save As*, and save the file to the root directory with the name `test.bat`. Make certain that you change the file type to *All Files*, rather than *Text*, as you see in **Figure 20.1**.

![](bbox=[0.045, 0.51, 0.42, 0.74])

Now open a command prompt and change to the `c:\` directory (you can do this by typing in `cd\` and pressing the Enter key). Then enter `test.bat` and then press the Enter key. You should see something very much like what is shown in **Figure 20.2**.