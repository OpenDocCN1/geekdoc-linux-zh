
## Chapter 3: Writing Shell Scripts

### In This Chapter
- Trying out simple shell scripts
- Learning the basics of shell scripting
- Exploring Bash's built-in commands

Red Hat Linux gives you many small and specialized commands, along with the plumbing necessary to connect these commands. By *plumbing*, I mean the way in which one command's output can be used as a second command's input. Bash (short for Bourne Again SHell) — the default shell in Linux — provides this plumbing in the form of I/O redirection and pipes. Bash also includes features such as the *if* statement that you can use to run commands only when a specific condition is true and the *for* statement that repeats commands a specified number of times. You can use these features of Bash when writing programs called *shell scripts*.

In this chapter, I show you how to write simple *shell scripts* — task-oriented collections of shell commands stored in a file. Shell scripts are used to automate various tasks. For example, when your Red Hat Linux boots, many shell scripts that are stored in various subdirectories in the */etc* directory (for example, */etc/init.d*) perform many initialization tasks.

### Trying Out Simple Shell Scripts

If you are not a programmer, you may feel apprehensive about programming. But shell *scripting* (or programming) can be as simple as storing a few commands in a file. In fact, you can have a useful shell program that has a single command.

While writing this book, for example, I captured screens from the X Window System and used the screen shots in figures. I used the X screen-capture program, *xwd*, to store the screen images in the X Window Dump (XWD) format. The book's production team, however, wanted the screen shots in TIFF format. Therefore, I've used the Portable Bitmap (PBM) toolkit to convert the XWD images to TIFF format. To convert each file, I've run two programs and deleted a temporary file, as follows:

```
xwdtopnm < file.xwd > file.pnm
pnmtotiff < file.pnm > file.tif
rm file.pnm
```

These commands assume that the xwdtopnm and pnmtotiff programs are in the /usr/bin directory — one of the directories listed in the PATH environment variable. By the way, xwdtopnm and pnmtotiff are two programs in the PBM toolkit.

After converting a few XWD files to TIFF format, I get tired of typing the same sequence of commands for each file, so I prepare a file named totif and save the following lines in it:

```
#!/bin/sh
xwdtopnm < $1.xwd > $1.pnm
pnmtotiff < $1.pnm > $1.tif
rm $1.pnm
```

Then I make the file executable by using this command:

```
chmod +x totif
```

The chmod command enables you to change the permission settings of a file. One of those settings determines whether the file is executable. The +x option means you want to mark the file as executable. You do have to mark it that way because Bash runs only executable files.

Now when I want to convert the file figure1.xwd to figure1.tif, I can do so by typing the following command:

```
./totif figure1
```

The ./ prefix indicates that the totif file is in the current directory — you don’t need the ./ prefix if the PATH environment variable includes the current directory. The totif file is a shell script (also called a shell program). When you run this shell program with the command totif figure1, the shell substitutes figure1 for each occurrence of $1. (Note that $1 refers to the first option that the user types on the command used to execute the script.)

Shell scripts are popular among system administrators. If you are a system administrator, you can build a collection of custom shell scripts that help you automate tasks you perform often. If a disk seems to be getting full, for example, you may want to find all files that exceed some size (say, 1MB) and that have not been accessed in the past 30 days. In addition, you may want to send an e-mail message to all users who have large files, requesting that they archive and clean up those files. You can perform all these tasks with a shell script. You might start with the following find command to identify large files:

```
find / -type f -atime +30 -size +100k -exec ls -l {} \; > /tmp/largefiles
```

This command creates a file named /tmp/largefiles, which contains detailed information about old files taking up too much space. After you get a list of the files, you can use a few other Linux commands — such as sort, cut, and sed — to prepare and send mail messages to users who have large files they should clean up. Instead of typing all these commands manually, place them in a file and create a shell script. That, in a nutshell, is the essence of shell scripts — to gather shell commands in a file so that you can easily perform repetitive system administration tasks.

Just as most Linux commands accept command-line options, a Bash script also accepts command-line options. Inside the script, you can refer to the options as $1, $2, and so on. The special name $0 refers to the name of the script itself.

Here's a typical Bash script that accepts arguments:

```
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

The first line runs the /bin/sh program, which subsequently processes the rest of the lines in the script. The name /bin/sh traditionally refers to the Bourne shell — the first UNIX shell. In Red Hat Linux, /bin/sh is a symbolic link to /bin/bash, which is the executable program for Bash.

Save this simple script in a file named simple, and make that file executable with the following command:

```
chmod +x simple
```

Now run the script as follows:

```
./simple
```

It displays the following output:

```
This script's name is: ./simple
Argument 1:
Argument 2:
```

The first line shows the script's name. Because you have run the script without arguments, the script displays no values for the arguments.

Now try running the script with a few arguments, like this:

```
./simple "This is one argument" second-argument third
```

This time the script displays more output:

```
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

As the output shows, the shell treats the entire string within the double quotation marks as a single argument. Otherwise, the shell uses spaces as separators between arguments on the command line.

This sample script ignores the third argument because the script is designed to print only the first two arguments. The script ignores all arguments after the first two.

## Learning the Basics of Shell Scripting

Like any programming language, the Bash shell supports the following features:

- Variables that store values, including special built-in variables for accessing command-line arguments passed to a shell script and other special values.
- The capability to evaluate expressions.
- Control structures that enable you to loop over several shell commands or to execute some commands conditionally.
- The capability to define functions that can be called in many places within a script. Bash also includes many built-in commands that you can use in any script.

In the next few sections, I illustrate some of these programming features through simple examples. (I'm assuming that you're already running Bash, in which case you can try the examples by typing them at the shell prompt in a terminal window.)

### Storing stuff

You define variables in Bash just as you define environment variables. Thus, you may define a variable as follows:

```
count=12  # note no embedded spaces allowed
```

To use a variable's value, prefix the variable's name with a dollar sign ($). For example, $PATH is the value of the variable PATH (this is the famous PATH environment variable that lists all the directories that Bash searches when trying to locate an executable file). To display the value of the variable count, use the following command:

```
echo $count
```

Bash has some special variables for accessing command-line arguments. In a shell script, $0 refers to the name of the shell script. The variables $1, $2, and so on refer to the command-line arguments. The variable $* stores all the command-line arguments as a single variable, and $? contains the exit status of the last command the shell executes.

From a Bash script, you can prompt the user for input and use the read command to read the input into a variable. Here is an example:

```
echo -n "Enter value: "
read value
echo "You entered: $value"
```

When this script runs, the read value command causes Bash to read whatever you type at the keyboard.

Note that the -n option prevents the echo command from automatically adding a new line at the end of the string that it displays.

### Calling shell functions

You can group a number of shell commands that you use consistently into a function and assign it a name. Later, you can execute that group of commands by using the single name assigned to the function. Here is a simple script that illustrates the syntax of shell functions:

```
#!/bin/sh

hello() {
    echo -n "Hello, "
    echo $1 $2
}

hello Jane Doe
```

When you run this script, it displays the following output:

```
Hello, Jane Doe
```

This script defines a shell function named hello. The function expects two arguments. In the body of the function, these arguments are referenced by $1 and $2. The function definition begins with hello() — the name of the function, followed by parentheses. The body of the function is enclosed in curly braces: { ... }. In this case, the body uses the echo command to display a line of text.
