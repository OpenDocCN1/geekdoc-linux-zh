Special built-in commands and functions are defined within the shell, and therefore are executed from within the context of the current shell, making them much faster in execution. Scripts and executable programs such as ls and date are stored on disk, and the shell, in order to execute them, must first locate them within the directory hierarchy by searching the PATH environment variable: the shell then forks a new shell that executes the script. To find out the type of command you are using—that is, a built-in command, an alias, a function, or an executable—use the built-in type command. (See Example 13.18.)

# EXAMPLE 13.18

```
$ type pwd
pwd is a shell builtin
$ type test
test is a shell builtin
$ type clear
clear is /usr/bin/clear
$ type m
m is aliased to 'more'
$ type bc
bc is /usr/bin/bc
$ type if
if is a shell keyword
$ type -path cal
/usr/bin/cal
$ type which
which is aliased to 'type -path'
$ type greetings
greetings is a function
greetings ()
{
    echo "Welcome to my world!";
}
```

# 13.3.2 Built-In Commands and the help Command

Built-in commands are commands that are part of the internal source code for the shell. They are built-in and readily available to the shell, whereas commands such as date, cal, and finger are compiled binary programs that reside on the disk. There is less overhead in executing a built-in because it involves no disk operations. Built-in commands are executed by the shell before executable programs on disk. Bash has added a new online help system so that you can see all the built-ins, or a description for a particular built-in; help itself is a built-in command. See Table 13.28 on page 857 for a complete list of built-in commands.