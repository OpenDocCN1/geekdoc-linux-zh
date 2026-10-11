![](bbox=[0.25, 0.1, 0.75, 0.45])

Figure 27-2 An if...then...else flowchart

If the test-command returns a true status, the if structure executes the commands between the then and else statements and then diverts control to the statement following fi. If the test-command returns a false status, the if structure executes the commands following the else statement.

When you run the next script, named out, with arguments that are filenames, it displays the files on the terminal. If the first argument is -v (called an option in this case), out uses less (page 150) to display the files one page at a time. After determining that it is -v. If the result of the test is true (if the first argument is -v), out uses the shift builtin to shift the arguments to get rid of the -v and displays the files using less. If the result of the test is false (if the first argument is not -v), the script uses cat to display the files:

```
$ cat out
if [ $# -eq 0 ]
then
echo "Usage: out [-v] filenames..."
exit 1
fi
if [ "$1" = "-v" ]
then
shift
less -- "$@"
else
cat -- "$@"
fi
```