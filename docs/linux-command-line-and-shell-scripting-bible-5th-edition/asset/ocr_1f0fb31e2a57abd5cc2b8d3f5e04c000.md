# ## Creating functions on the command line

Because the shell interprets commands as you type them, you can define a function directly on the command line. You can do that in two ways.

The first method defines the function all on one line:

```
$ function divem { echo -n $1 / $2 ; }
$ divem 100 5
20
$
```

When you define the function on the command line, you must remember to include a semicolon at the end of each command so that the shell knows where to separate commands:

```
$ function doubleit { read -p "Enter value: " value; echo -n
$ $value * 2 ; }
$
$ doubleit
Enter value: 20
40
$
```

The other method is to use multiple lines to define the function. When you do that, the Bash shell uses the secondary prompt to ask you for more commands. Using this method, you don’t need to place a semicolon at the end of each command; just press the Enter key.

```
$ function multem {
> echo $[ $1 * $2 ]
>}
$ multem 2 5
10
$
```

When you use the brace at the end of the function, the shell knows that you’re finished defining the function.

> **WARNING**
> Be extremely careful when creating functions on the command line. If you use a function with the same name as a built-in command or another command, the function overrides the original command.

# ## Defining functions in the .bashrc file

The obvious downside to defining shell functions directly on the command line is that when you exit the shell, your function disappears. For complex functions, this can become a problem. A much simpler method is to define the function in a place where it is reloaded by the shell each time you start a new shell.