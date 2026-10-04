**Table 8-4 Bourne Shell Built-ins (continued)**

| Built-in | Description |
|---|---|
| read | Read a line from standard input |
| readonly | Change a variable to read only |
| set | Set shell options |
| test | Evaluate conditional expressions |
| times | Display execution times |
| trap | Manage execution signals |
| umask | Set default security for files and directories |
| unset | Unset a local variable |
| wait | Wait for a background process to complete |

**Table 8-5 Bourne Shell Conditionals**

| Conditional | Description |
|---|---|
| if-then-else-if | Tests a condition and selects an action based on the results of the test |
| case-esac | Selects an action based on the value of the variable |
| for-do-done | Repeats a sequence of commands until a predetermined condition is met |
| while-do-done | Repeats a sequence of commands until a test condition is no longer true |
| until-do-done | Repeats a sequence of commands until a test condition results in a successful status |

# Shell Conditionals

In addition to the built-ins listed in Tables 8-4 and 8-5, the Bourne shell also contains some simple conditionals. A conditional command makes a choice depending on the outcome of some condition. Examples of conditionals are &&, ||, if, and case.

# && and ||

The simplest conditional in the Bourne shell is the double ampersand (&&). When two commands are separated by a double ampersand, the second command executes only if the first command returns a zero exit status (an indication of successful completion).

```
Example:
ls -ld /usr/bin > /dev/null && echo "Directory Found"
```