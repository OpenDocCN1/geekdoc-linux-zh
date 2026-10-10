Standard Error - 2: STDERR

The first is standard input, the next are standard output and standard error. The numerical values are file descriptors.

In addition to these techniques, pipes are extensively used in scripts.

# Pipes

Piping is useful when an output of a command is required as an input of another. This is something we have learned so far. The operator used is '|'.

Example:

```
#!/bin/bash
cat employee.txt | sort -nr -k 2
```

#Here we redirect the file entry we obtain to the sort function. It sorts by numeric #values, in reverse order and sort by column id (2nd column).

![](bbox=[0.13, 0.46, 0.65, 0.56])

# Mathematical Operations in Script Building

Any script can be used to perform certain calculations. There are some built-in commands in Linux. We are looking into the command expr. This stands for the expression. These are the operators for expr command.