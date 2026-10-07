In this case, *var* is initialized when the *for* loop starts. The expression is evaluated, and if true, the loop runs. Then the value of *var* is incremented and the expression is tested again.

The format of the *for* loop may look strange if you haven’t encountered programming languages before, but it is the same as the *for* loop used in C, for example.

# next and exit

The *next* instruction tells *gawk* to process the next record in the file, regardless of what it is doing. For example, consider this script:

```
`{ command1
    command2
    command3
    next
    command4
}`
```

As soon as the *next* statement is read, *gawk* moves to the next record in the file and starts at the top of the current script block (given by the curly brace). In this example, *command4* will never be executed because the *next* statement moves back up to *command1* each time.

The *next* statement is usually used inside an *if* loop, where you may want execution to return to the start of the script if some condition is met.

The *exit* statement makes *gawk* behave as though it has reached the end of the file, and it then executes any *END* patterns (if any exist). This is a useful method of aborting processing if there is an error in the file.

# Arrays

The *gawk* language supports arrays and enables you to access any element in the array easily. No special initialization is necessary with an array, because *gawk* treats it like any other variable. The general format for declaring arrays is as follows:

```
`var[num]=value`
```

As an example, consider the following script, which reads an input file and generates an output file with the lines reversed in order:

```
`# reverse lines in a file
{line[NR] = $0 }  # remember each line
END {var=NR          # output lines in reverse order`
```