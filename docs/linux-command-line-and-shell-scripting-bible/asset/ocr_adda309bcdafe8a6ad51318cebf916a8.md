# Part IV Alternative Linux Shells

| TABLE 23-3 |
| Parameter | Description |
| -a | Create a numerical array variable. |
| -A | Create an associative array variable. |
| -E | Create a double-precision floating-point variable and display using scientific notation. |
| -f | Define a function name instead of a variable. |
| -F | Create a double-precision floating-point variable and display using fixed-point decimal notation. |
| -h | Create a hidden special variable. |
| -H | Don't display the value of the variable. |
| -i | Create an integer data type variable. |
| -l | Convert the variable value to lower case. |
| -L | Left-justify by removing leading blanks from a variable. |
| -r | Make the specified variables read-only. |
| -R | Right-justify by adding blanks on the left. |
| -t | Tag the specified variables. |
| -u | Convert the variable value to upper case. |
| -U | Keep only the first occurrence for each duplicated value in a numerical array. |
| -x | Mark the specified variable for automatic export. |
| -Z | Right-justify using leading zeroes. |

As you can see from the typeset command parameters, the zsh supports arrays, both numeric and associative. If you're used to using numeric arrays in the bash and k shells, you'll have to be a little careful when using them in the zsh. The zsh starts arrays with an index value of 1 instead of 0:

```
% mytest=(one two three four)
echo ${mytest[1]}
one
echo ${mytest[2]}
two
%
```

624