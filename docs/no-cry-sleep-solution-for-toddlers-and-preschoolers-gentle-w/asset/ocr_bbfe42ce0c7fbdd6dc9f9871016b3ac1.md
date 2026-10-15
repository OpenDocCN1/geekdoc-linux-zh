# Shell Scripts: User-Defined Commands

You can place shell commands within a file and then have the shell read and execute the commands in the file. In this sense, the file functions as a shell program, executing shell commands as if they were statements in a program. A file that contains shell commands is called a shell script.

You enter shell commands into a script file using a standard text editor such as the Vi editor. The sh or . command used with the script's filename will read the script file and execute the commands. In the next example, the text file called lsc contains an ls command that displays only files with the extension .c:

```
lsc
ls *.c
$ sh lsc
main.c calc.c
$ . lsc
main.c calc.c
```

# Executing Scripts

You can dispense with the sh and . commands by setting the executable permission of a script file. When the script file is first created by your text editor, it is given only read and write permission. The chmod command with the +x option will give the script file executable permission. (Permissions are discussed in Chapter 28) Once it is executable, entering the name of the script file at the shell prompt and pressing ENTER will execute the script file and the shell commands in it. In effect, the script's filename becomes a new shell command. In this way, you can use shell scripts to design and create your own Linux commands. You need to set the permission only once. In the next example, the lsc file's executable permission for the owner is set to on. Then the lsc shell script is directly executed like any Linux command.

```
$ chmod u+x lsc
$ lsc
main.c calc.c
```

You may have to specify that the script you are using is in your current working directory. You do this by prefixing the script name with a period and slash combination, ./, as in ./lsc. The period is a special character representing the name of your current working directory. The slash is a directory pathname separator, as explained more fully in Chapter 28 (you could also add the current directory to your PATH variable as discussed in Chapter 10). The following example would show how you would execute the hello script:

```
$ ./lsc
main.c calc.c
```

# Script Arguments

Just as any Linux command can take arguments, so also can a shell script. Arguments on the command line are referenced sequentially starting with 1. An argument is referenced using the $ operator and the number of its position. The first argument is referenced with