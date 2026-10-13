# Simple Commands

The commands who and date are examples of simple commands. A simple command is one that can be executed just by specifying the command name at the prompt. The syntax for executing a simple command is

```
$ cmd
```

Here cmd is the name of the command to be executed.

Simple commands in UNIX can be small commands such as who and date, or they can be large commands such as a Web browser or spreadsheet program. Most commands in UNIX can be executed as simple commands.

# Complex Commands

A complex command consists of a command name followed by a list of arguments. Arguments are modifiers specified after the command name and are used to alter the behavior of the command. The syntax for a complex command is

```
$ cmd arg1 arg2 ... argN
```

Here cmd is the name of the command you want to execute, and arg1 through argN are the arguments you want to give cmd. As an example, you can use the who command to determine information about yourself by executing it as follows:

```
$ who -i
ranga pts/0 Dec 9 08:49
$
```

In this mode, who omits information about the other users and just prints information about you. This is an example of a complex command. Here, the cmd is who and the arguments, arg1 and arg2, are -i and 1. These arguments change the behavior of the who command. Most commands accept arguments that modify their behavior.

![](bbox=[0.18, 0.87, 0.26, 0.93])

> Although you can specify any arguments you want to a command, most commands only understand a handful of arguments. Some commands ignore arguments they do not understand, whereas others display error messages. The man command, discussed in Chapter 2, can help determine the arguments a command understands.

When who was executed as a simple command, it displayed information about all the users who were logged in. This is referred to as the default behavior for the who command. The default behavior of a command is the output produced by the command when it is executed as a simple command.