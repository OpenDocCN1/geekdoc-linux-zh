| Variable | Description |
| :--- | :--- |
| `$0` | The name of the program file. |
| `$1, $2, $n.` | The first, second, or the *n* argument from the invocation. |
| `$#` | The number of arguments supplied to the program. |
| `$@` | All the arguments passed are treated as one string. |
| `$?` | The exit status ($-1$, $0$, or a positive number) from the previous command executed. |
| `$$` | The current process ID for the script. |

Table 12.1: Special variables in a shell script.

The following code shows a *script* example using all the special variables.

```
#!/bin/sh
echo "The name of the script is $0"
echo "The number of the arguments are $#"
echo "The first argument value is $1"
echo "The second argument value is $2"
echo "The value for all arguments are: $@"
echo "The current process id is $$"
uptime
echo "The exit status for the command uptime was $?"
notexisting
echo "The exit status for the command notexisting was $?"
```

*Figure 12.4* shows an example output when three arguments are passed to the script with the name **example4.sh**: