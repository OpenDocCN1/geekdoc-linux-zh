![](bbox=[0.87, 0.09, 0.97, 0.21])

# **awk - Pattern-processing language.**

awk(1)

# **NAME**

awk - pattern-directed scanning and processing language

# **SYNOPSIS**

```
awk [-Ff s] [-v var=value] [program | -f progfile ...] [file ...]
```

# **DESCRIPTION**

awk scans each input file for lines that match any of a set of patterns specified literally in program or in one or more files specified as *-f progfile*. With each pattern there can be an associated action that is to be performed when a line in a file matches the pattern. Each line is matched against the pattern portion of every pattern-action statement, and the associated action is performed for each matched pattern. The file name *- * means the standard input. Any file of the form *var=value* is treated as an assignment, not a filename. An assignment is evaluated at the time it would have been opened if it were a filename, unless the *-v* option is used.

An input line is made up of fields separated by white space, or by regular expression *FS*. The fields are denoted *$1, $2, ..., $0* refers to the entire line.

# **Options**

awk recognizes the following options and arguments:

+   * -F fs     Specify regular expression used to separate fields. The default is to recognize space and tab characters, and to discard leading spaces and tabs. If the *-F* option is used, leading input field separators are no longer discarded.
* -f progfile Specify an awk program file. Up to 100 program files can be specified. The pattern-action statements in these files are executed in the same order as the files were specified.
* -v var=value Cause *var=value* assignment to occur before the BEGIN action (if it exists) is executed.

# **Statements**

A pattern-action statement has the form:

```
pattern { action }
```

A missing { action } means print the line; a missing pattern always matches. Pattern-action statements are separated by new-lines or semicolons.

An action is a sequence of statements. A statement can be one of the