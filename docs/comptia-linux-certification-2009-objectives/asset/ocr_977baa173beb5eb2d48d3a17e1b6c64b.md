# The tail Command

The `tail` command is used to retrieve data from a file. By default, it displays the last ten lines of the file. The `tail` command has various options. Some of the frequently used options are listed in the table.

![](bbox=[0.77, 0.1, 0.88, 0.16])

| Option | Enables You To |
| :--- | :--- |
| `--retry` | Force the `tail` command to open a file that cannot be opened. |
| `-c` _(Total no. of bytes)_ | Print the specified number of bytes from the end of a file. |
| `-f` | Update the output of the `tail` command if any changes are made to a file. |

![](bbox=[0.12, 0.35, 0.71, 0.66])

# Syntax

The syntax of the `tail` command is `tail [options] {file name}`.

# The awk Command

The `awk` command is a command that performs pattern matching. The GNU's version of `awk` is called `gawk`. The `awk` keyword is followed by the pattern, the action to be performed, and the file name. The action to be performed is given within curly braces. The pattern and the action to be performed should be specified within single quotes. If the pattern is not specified, the action is performed on all input data; however, if the action is not specified, the entire line is printed. The `awk` command can be executed from the command line or from within an `awk` script file.

![](bbox=[0.77, 0.77, 0.88, 0.82])