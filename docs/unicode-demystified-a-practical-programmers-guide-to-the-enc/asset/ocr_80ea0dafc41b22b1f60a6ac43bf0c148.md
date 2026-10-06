# Relop

| | | |
| -gt | Greater than |
| -ge | Greater than or equal to |
| -eq | Equal to |
| -ne | Not equal to |
| -le | Less than or equal to |
| -lt | Less than |

# Note

The test command is built into bash, tsh, and zsh.

# Examples

The following examples show how to use the test utility in Bourne Again scripts. Although test works from a command line, it is more commonly used in shell scripts to test input or verify access to a file.

The first two examples show incomplete shell scripts. They are not complete because they do not test for upper- as well as lowercase input or inappropriate responses and do not acknowledge more than one response.

The first example prompts the user, reads a line of input into the user user_input, and uses test to see whether the user variable user_input matches the string:

```
$ cat user_in
echo -n "Input yes or no: "
read user_input
if [ "$user_input" = yes ]
then
echo You input yes.
```

Refer to Chapters 12 and 13 for more information on variables, read, and if.

The next example prompts for a filename and then uses test to see whether the user has read access permission (-r) for the file and (-a) whether the file contains information (-s):

fi