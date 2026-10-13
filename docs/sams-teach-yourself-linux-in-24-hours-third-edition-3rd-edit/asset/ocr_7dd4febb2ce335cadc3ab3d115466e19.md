> You'll learn how to use these shell shortcuts when you begin working with commands in Hour 6.

![](bbox=[0.18, 0.16, 0.24, 0.23])

# Telling the Command Where to Go

When you use the command line to start a program in Linux, the shell interprets your command, sends it to the kernel, and the output of your program goes to the standard output (usually the screen). The program's output to the standard output can be redirected to a file. Remember that Linux sees everything as a file, so the standard output can be redirected to a file, a printer, an additional monitor, another terminal, or any other output device that you might have connected to the system. The output can also be redirected to be the input for another command or program.

![](bbox=[0.18, 0.52, 0.25, 0.6])

> Be careful when redirecting command outputs. Redirecting the output to a file will create the named file and put the output in it. If you redirect the output to an existing file, the contents of that file will be overwritten and gone forever.

You'll use redirection when you learn more about typing at the command line in Hour 6, "Looking at the Command Line," and in Hour 7, "Moving Around the Filesystem."

# Creating Shortcuts for Long Commands

You might find that you type a number of commands on a regular basis. For example, if you use the online Linux help system, you might find yourself going to some obscure directory such as /usr/doc/HOWTO/HTML/en/mini. Let's do the math...add the cd command to the directory path and you get 31 keystrokes (and that doesn't count holding down the Shift key). To reduce the number of keystrokes, create an alias.

> **New Term** A command alias is a unique, short name that is assigned to a command. Command aliases make it easier to remember long commands by assigning a nickname to them. Instead of typing the complete command, you can just type the alias. Aliases can also help you reduce fatal mistakes when working with files. You can assign aliases to commands so that you are asked whether you really want to delete a file.