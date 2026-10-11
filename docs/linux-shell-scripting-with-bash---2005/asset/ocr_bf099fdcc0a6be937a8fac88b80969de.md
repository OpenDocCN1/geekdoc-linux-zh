The function `trash_tmp` moves the `TMP` file to a directory called `trash` in the user’s home directory. The function is created by the `function` command but it doesn’t execute until it is explicitly named in the program.

The `readonly` command prevents a function from being redefined. The command is discussed in detail later in this chapter.

Normally, the `DEBUG` trap is not executed by functions. `declare -t` turns on debug trap execution in functions.

Like scripts, functions can have parameters. Although parameter `$0` retains the pathname of the script, the other parameters are parameters supplied to the function, with `$#` indicating the number of parameters. When the function completes, the parameter variables are restored to their previous values.

The `FUNCNAME` variable contains the name of a function while the function is executing. Using `$SCRIPT: $FUNCNAME:` when reporting errors identifies the script and the function where the error occurred.

Because functions are not subscripts, functions return status codes and declare variables differently.

In a script, the `exit` command returns a status code. In a function, the `exit` command exits the script containing the function. To return a status code without exiting a script, functions use a `return` command instead. The `return` statement is used the same way as an `exit` statement.

# Local Variables

Variables declared inside a function exist only for the duration of the function. These are called *local variables*. When the function completes, the variables are discarded, the same way variables are discarded by subscripts. See Listing 14.11.

```
Listing 14.11 function2.sh

```bash
#!/bin/bash
#
# function2.sh: A simple function example with local variables
#
shopt -s -o nounset

declare -rx SCRIPT=$0##*/
declare -rx TMP=/tmp/temp.$$*

# TRASH FILE
#
# Move the specified file to the trash directory
# The first parameter is the file to move

function trash_file {
```
```