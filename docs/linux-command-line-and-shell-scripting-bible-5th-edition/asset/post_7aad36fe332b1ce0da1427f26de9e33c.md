
## Looking at local environment variables

Local environment variables, as their name implies, can be seen only in the local process in which they are defined. Even though they are local, they are just as important as global environment variables. In fact, the Linux system also defines standard local environment variables for you by default. However, you can also define your own local variables. These, as you would assume, are called user-defined local variables.

Trying to see the local variables list is a little tricky at the CLI. Unfortunately, there isn't a command that displays only these variables. The `set` command displays all variables defined for a specific process, including both local and global environment variables as well as user-defined variables:

```bash
$ set
BASH=/bin/bash
[...]
HOME=/home/christine
[...]
PWD=/home/christine
[...]
SHELL=/bin/bash
[...]
TERM=xterm
[...]
USER=christine
[...]
colors=/home/christine/.dircolors
my_variable='Hello World'
[...]
_command ()
{
[...]
}
$
```

All the global environment variables displayed using the `env` or `printenv` command appear in the `set` command's output. The additional environment variables are the local environment and user-defined variables. Also included in the `set` command's output are local shell functions, such as the `_command` function listed in the previous display. Shell functions are covered in Chapter 17, "Creating Functions."

> **NOTE**
> The differences between the `env`, `printenv`, and `set` commands are subtle. The `set` command displays global and local environment variables, user-defined variables, and local functions. It also sorts the display alphabetically. The `env` and `printenv` are different from `set` in that they do not sort the variables, nor do they include local environment variables, local user-defined variables, or local shell functions. Used in this context, `env` and `printenv` produce duplicate listings. However, the `env` command has additional functionality that `printenv` does not have, making it the slightly more powerful command.

## Setting User-Defined Variables

You can set your own variables directly from the Bash shell. This section shows you how to create your own variables and reference them from an interactive shell or shell script program.

### Setting local user-defined variables

After you start a Bash shell (or spawn a shell script), you’re allowed to create local user-defined variables that are visible within your shell process. You can assign either a numeric or a string value to an environment variable by assigning the variable to a value using the equals sign:

```bash
$ my_variable=Hello
$ echo $my_variable
Hello
$
```

That was simple! Now, any time you need to reference the `my_variable` user-defined variable’s value, just reference it by the name `$my_variable`.

If you need to assign a string value that contains spaces, you must use a single or double quotation mark to delimit the beginning and the end of the string:

```bash
$ my_variable=Hello World
bash: World: command not found...
$
$ my_variable="Hello World"
$ echo $my_variable
Hello World
$
```

Without the quotation marks, the Bash shell assumes that the next word (World) is another command to process. Notice that for the local variable you defined, you use lowercase letters, whereas the system environment variables you’ve seen so far have all used uppercase letters.

> **CAUTION**
> The standard Bash shell convention is for all environment variables to use uppercase letters. If you are creating a local variable for yourself and your own shell scripts, use lowercase letters. Variables are case sensitive. By keeping your user-defined local variables lowercase, you avoid the potential disaster of redefining a system environment variable.

It’s extremely important that you not use spaces between the variable name, the equals sign, and the value. If you put any spaces in the assignment, the Bash shell interprets the value as a separate command:

```bash
$ my_variable = "Hello World"
bash: my_variable: command not found...
$
```

After you set a local variable, it’s available for use anywhere within your shell process. However, if you spawn another shell, it’s not available in the child shell:

```bash
$ my_variable="Hello World"
$ bash
$ echo $my_variable

$ exit
exit
$ echo $my_variable
Hello World
$
```

In this example, a child shell was spawned via the bash command. The user-defined my_variable was not available in the child shell. This is demonstrated by the blank line returned after the echo $my_variable command. After the child shell was exited and returned to the original shell, the local variable was available.

Similarly, if you set a local variable in a child process, after you leave the child process, the local variable is no longer available:

```bash
$ echo $my_child_variable

$ bash
$ my_child_variable="Hello Little World"
$ echo $my_child_variable
Hello Little World
$ exit
exit
$ echo $my_child_variable
$
```

The local variable set within the child shell doesn’t exist after a return to the parent shell. You can change this behavior by turning your local user-defined variable into a global variable.

### Setting global environment variables

Global environment variables are visible from any child process created by the parent process that sets the variable. The method used to create a global environment variable is to first create a local variable and then export it to the global environment.

This is done by using the export command and the variable name (minus the dollar sign):

```bash
$ my_variable="I am Global now"
$
$ export my_variable
$
$ echo $my_variable
I am Global now
```

```bash
$ bash
$ echo $my_variable
I am Global now
$ exit
exit
$ echo $my_variable
I am Global now
$
```

After defining and exporting the local variable `my_variable`, a child shell was started by the `bash` command. The child shell was able to properly display the `my_variable` variable's value. The variable kept its value, because the `export` command made it global.

> **Tip**
> To keep typing to a minimum, you can set the variable and export it all in one command. Using the previous example, you would type `export my_variable="I am Global Now"` and press `Enter` at the command line.

Changing a global environment variable within a child shell does not affect the variable's value in the parent shell:

```bash
$ export my_variable="I am Global now"
$ echo $my_variable
I am Global now
$
$ bash
$ echo $my_variable
I am Global now
$ my_variable="Null"
$ echo $my_variable
Null
$ exit
exit
$
$ echo $my_variable
I am Global now
$
```

After defining and exporting the `my_variable` variable, a subshell was started by the `bash` command. The subshell properly displayed the value of the `my_variable` global environment variable. The variable's value was then changed by the child shell. However, the variable's value was modified only within the child shell, and not in the parent's shell environment.

A child shell cannot even use the `export` command to change the parent shell's global variable's value:

```bash
$ echo $my_variable
I am Global now
```

```bash
$ bash
$ export my_variable="Null"
$ echo $my_variable
Null
$ exit
exit
$
$ echo $my_variable
I am Global now
$
```

Even though the child shell redefined and exported the `my_variable` variable, the parent shell's `my_variable` variable kept its original value.

### Removing Environment Variables

Of course, if you create a new environment variable, it makes sense that you can also remove an existing environment variable. You can do this with the `unset` command. When referencing the environment variable in the `unset` command, remember not to use the dollar sign:

```bash
$ my_variable="I am going to be removed"
$ echo $my_variable
I am going to be removed
$
$ unset my_variable
$ echo $my_variable
$
```

> **Tip**
> It can be confusing to remember when to use and when not to use the dollar sign with environment variables. Just remember this: If you are doing anything with the variable, use the dollar sign. If you are doing anything to the variable, don't use the dollar sign. The exception to this rule is using `printenv` to display a variable's value, which does not require the dollar sign.

When dealing with global environment variables, things get a little tricky. If you're in a child process and unset a global environment variable, it applies only to the child process. The global environment variable is still available in the parent process:

```bash
$ export my_variable="I am Global now"
$ echo $my_variable
I am Global now
$
```
