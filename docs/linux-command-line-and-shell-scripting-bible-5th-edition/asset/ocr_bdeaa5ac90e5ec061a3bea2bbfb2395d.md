# Chapter 25: The Korn Shell

The subscript is a text value, similar to the key in the associative array. The values can be any text or numerical value:

```
$ test3=(fruit=banana vegetable=carrot age=18) 
$
$
```

Once you assign the subscripts and values, you can reference an individual subscript value with this format:

```
variable.subscript
```

Here's how this looks:

```
$ echo ${test3.fruit}
banana
$ echo ${test3.age}
18
$
$
```

Each individual subscript value can be extracted just by referencing the subscript name along with the variable.

# Special variable subscripts

There are several special subscripts that are available in the ksh93 shell. These subscripts define current information about the shell, as well as current information about the currently running process in the shell. Table 25.4 lists the ksh93 shell subscript variables.

# TABLE 25.4   The ksh93 Subscript Variables

| Variable | Description |
| :--- | :--- |
| .sh.command | The current command line about to run. |
| .sh.edchar | The value of the keyboard character entered for the last KEYBD trap detected by the shell. |
| .sh.ecdol | The character position of the cursor at the last KEYBD trap. |
| .sh.edmode | Set to ESC when processing a key in vi editor mode, otherwise set to null. |
| .sh.edtext | The characters in the keyboard buffer when processing the last KEYBD trap. |
| .sh.file | The pathname of the file that contains the current command. |
| .sh.fun | The name of the function currently being executed. |
| .sh.match | An indexed array that stores the most recent match and subpattern matches. |
| .sh.name | The name of the variable at the time a discipline function is executed. |
| .sh.subscript | Set to the name subscript of the variable at the time a discipline function is executed. |
| .sh.subshell | The current depth of subshells and command substitution. |
| .sh.value | The value of the variable at the time a discipline function is executed. |
| .sh.version | The version of the shell. |

25

621