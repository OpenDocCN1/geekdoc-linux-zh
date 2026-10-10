# 23.5 Input Using the read Statement

Suppose you run the script by typing the command line

```
$ echo.args We like UNIX. (Return)
```

The shell stores the name of the command ("echo.args") in the parameter $0; it puts the argument "We" in the parameter $1; it puts "like" in the parameter $2, and "UNIX." in parameter $3. Since that takes care of all the arguments, the rest of the parameters are left empty. Then the script prints the contents of the variables:

```
echo.args We like UNIX.
```

What if the user types in more than nine arguments? The positional parameter $* contains all of the arguments $1, $2, $3, ..., $9, and any arguments beyond these nine. Thus, we can rewrite echo.args to handle any number of arguments:

```
#!/bin/sh
# Illustrate the use of positional parameters
echo $*
```

The parameter $# contains the number of arguments that the user typed. We can modify the script echo.args once again to use this parameter:

```
#!/bin/sh
# Illustrate the use of positional parameters
echo You typed $# arguments: $*
```

Suppose we were then to type the command line

```
$ echo.args To be or not to be (Return)
```

The computer would respond with

```
You typed 6 arguments: To be or not to be
```

> $* does not contain $0, so echo.args is neither counted nor printed.

# 23.5 Input Using the read Statement

The positional parameters are useful for capturing command-line arguments but they have a limitation: once the script begins running, the positional parameters can-not be used for obtaining more input from the standard input. For this you have to use the read statement. Let's modify the previous program to make use of read:

```
#!/bin/sh
# Illustrate the use of positional parameters, user-defined
# variables and the read command.
echo 'What is your name?'
read name
echo "Well, $name, you typed $# arguments:"
echo "$*"
```