# Part IV: Working with Alternative Shells

The right prompt displays the defined prompt (set to the current working directory in this example) on the far right if the space isn't needed to display text. If the shell needs to display text, it doesn't display the right prompt.

The zsh shell supports the `type`*set* command, which allows you to declare attributes for a variable before using it. Table 23.3 shows the options available for the zsh `type`*set* command.

# **TABLE 23.3** **The type*set* Command Parameters**

| Parameter | Description |
| :--- | :--- |
| -a | Creates a numerical array variable. |
| -A | Creates an associative array variable. |
| -E | Creates a double-precision floating-point variable and displays it using scientific notation. |
| -F | Defines a function name instead of a variable. |
| -F | Create a double-precision floating-point variable and displays it using fixed-point decimal notation. |
| -h | Creates a hidden special variable. |
| -H | Doesn't display the value of the variable. |
| -I | Creates an integer data type variable. |
| -L | Converts the variable value to lowercase. |
| -L | Left-justifies by removing leading blanks from a variable. |
| -r | Makes the specified variables read-only. |
| -R | Right-justifies by adding blanks on the left. |
| -t | Tags the specified variables. |
| -u | Converts the variable value to uppercase. |
| -U | Keeps only the first occurrence for each duplicated value in a numerical array. |
| -x | Marks the specified variable for automatic export. |
| -Z | Right-justifies using leading zeros. |

As you can see from the `type`*set* command parameters, the zsh shell supports arrays, both numeric and associative. If you're used to using numeric arrays in the Bash and ksh shells, you'll have to be a little careful when using them in the zsh shell. The zsh shell starts arrays with an index value of 1 instead of 0:

```
% mytest=(one two three four)
% echo ${mytest[1]}
one
% echo ${mytest[2]}
two
% 
```