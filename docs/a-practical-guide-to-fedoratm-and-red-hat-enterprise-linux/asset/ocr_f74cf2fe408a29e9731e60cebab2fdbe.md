```
$ memo=max\n$ ls
max.report
max.summary
$ echo $memo
max.report max.summary
```

Above, the shell expands the `$memo` variable to `max*`, expands `max*` to `max.report` and `max.summary`, and passes these two values to `echo`. In the next example, the Bourne Again Shell does *not expand the string* because `bash` does not perform pathname expansion (page 165) when it assigns a value to a variable.

```
$ echo "$memo"
max\*
```

All shells process a command line in a specific order. Within this order `bash` expands variables before it interprets commands. In the preceding `echo` command line, the double quotation marks quote the asterisk (`*`) in the expanded value of `$memo` and prevent `bash` from performing pathname expansion on the expanded `memo` variable before passing its value to the `echo` command.

# optional
Braces around variables

The `$VARIABLE` syntax is a special case of the more general syntax `${VARIABLE}`, in which the variable name is enclosed by `{}`. The braces insulate the variable name from adjacent characters. Braces are necessary when concatenating a variable value with a string:

```
$ PREF=counter
$ WAY=$PREFclockwise
$ FAKE=$PREFfeit
$ echo $WAY $FAKE
$
```

The preceding example does not work as expected. Only a blank line is output because although `PREFclockwise` and `PREFfeit` are valid variable names, they are not initialized. By default `bash` evaluates an unset variable as an empty (null) string and displays this value. To achieve the intent of these statements, refer to the `PREF` variable using braces:

```
$ PREF=counter
$ WAY=${PREF}clockwise
$ FAKE=${PREF}feit
$ echo $WAY $FAKE
counterclockwise counterfeit
```

The Bourne Again Shell refers to command-line arguments using the positional parameters `$1`, `$2`, `$3`, and so forth up to `$9`. You must use braces to refer to arguments past the ninth argument: `${10}`. The name of the command is held in `$0` (page 1022).