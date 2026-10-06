![](bbox=[0.365, 0.065, 0.803, 0.298])

# Figure 13-5 A while flowchart

As long as the **test-command** returns a *true* exit status, the structure continues to execute the series of *commands* delimited by the **do** and **done** statements. Before each loop through the *commands*, the structure executes the *test-command*. When the exit status of the **test-command** is *false*, the structure passes control to the state-after the **done** statement.

The following shell script first initializes the **number** variable to a value of zero. The **test** builtin then determines whether the value of **number** is less than 10. The script uses test with the -lt argument to perform a numerical test. For numerical comparisons, you must use -ne (not equal), -eq (equal), -gt (greater than), -ge (greater than or equal to), -lt (less than), or -le (less than or equal to); for string comparisons, = (equal) or != (not equal) when you are working with **test**. The **test** builtin has an exit status of 0 (*true*) as long as *number* is less than 10. As long as test returns true, the structure executes the commands between the **do** and **done** statements:

```
$ count
!/bin/bash
number=0
while [ "$number" -lt 10 ];
  do
    echo -n "$number"
    number=$( expr $number + 1)
  done
echo
$ count
0123456789
$ 
```