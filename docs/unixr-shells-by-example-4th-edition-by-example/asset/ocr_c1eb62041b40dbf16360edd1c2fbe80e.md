# Table 2.4 Bash Shell Syntax and Constructs (continued)

| Global variables | Global variables are called environment variables and are created with the export built-in command. They are set for the currently running shell and any process spawned from that shell. They go out of scope when the script ends.

The built-in declare function with the -x option also sets an environment variable and marks it for export.

**EXAMPLE**
```
export VARIABLE_NAME=value
declare -x VARIABLE_NAME=value
export PATH=/bin:/usr/bin:.
``` |
| Extracting values from variables | To extract the value from variables, a dollar sign is used.

**EXAMPLE**
```
echo $variable_name
echo $name
echo $PATH
``` |
| Reading user input | The user will be asked to enter input. The read command is used to accept a line of input. Multiple arguments to read will cause a line to be broken into words, and each word will be assigned to the named variable.

**EXAMPLE**
```
echo "what is your name?"
read name
read name1 name2 ...
``` |
| Arguments | Arguments can be passed to a script from the command line. Positional parameters are used to receive their values from within the script.

**EXAMPLE**

At the command line:
$ scriptname arg1 arg2 arg3 ...

In a script:
```
echo $1 $2 $3        Positional parameters
echo $@             All the positional paramters
echo $#             The number of positional parameters
``` |
| Arrays | The Bourne shell utilizes positional parameters to create a word list. In addition to positional parameters, the Bash shell supports an array syntax whereby the elements are accessed with a subscript, starting at 0. Bash shell arrays are created with the declare -a command |