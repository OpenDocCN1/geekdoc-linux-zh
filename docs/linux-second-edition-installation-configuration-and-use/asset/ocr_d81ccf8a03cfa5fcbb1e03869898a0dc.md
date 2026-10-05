# BASH PROGRAMMING

Another interesting command in connection with parameter evaluation isash command shift. This command shifts the passed parameters through the nine
variables $1 to $. When you execute shift 9, the first nine parameters passed to
the program are lost; in exchange, the next nine parameters can now be easily accessed,
shift without further shifts shifts parameter list by one.

$? can be used to construct conditions in order to make the further course of
the program depend on the result of the last command processed. In principle, it is
also possible to specify a command directly as a condition in if. The variable $ has
t advantage that it prevents instructions from becoming too long and unclear (see
page 416).
The variable $ss contains the PID (process identification number). This numerical
value is used internally by Linux for process management. The PID is unique,
that, in the whole system, there exists no other process with the same number. For
this reason, the PID is particularly useful for the creation of a temporary file.
example, you could use ls > tmp.$ss to store a list of all files in the file $tmp.nn.
Even if the same batch file runs simultaneously in another terminal, there will neverbe name conflict between the temporary files because the two shells have different
PIDs.

# Parameter substitution

Under the heading parameter substitution, the bash provides several commands for
processing character strings in variables. The syntax of this substitution mechanism
is ${var_pattern}, where _ stands for one or two special characters which
sspecify the type of substitution command. Please note that the variable name is specified
without a preceding $. However, if the pattern is to be read from a
variable, the $ character must precede that variable.

```
${var=default}
```

if the variable is empty, the construction yields the default setting as a,
otherwise it yields the contents of the variable. The variable is not changed.

```
${var:=default}
```

as above, but at the same time contents of the variable are changed if it has
been empty up to now.

```
${var:+new}
```

if the variable is empty, it is not changed. If it is already occupied, the current
contents are replaced with a new setting. The construction returns the new
contents of the variable.

```
${var?error_message}
```

if the variable is empty, the variable name and the error message are displayed,
then the shell program is terminated. Otherwise, the construction returns the
contents of the variable.

```
${#var}
```

returns the number of characters stored in the variable (0, if the variable is
empty). The variable is not changed.