# Mathematical expressions

Besides regular expressions you can also use mathematical expressions in the matching pattern. This feature comes in handy when matching numerical values in data fields. For example, if you want to display all of the system users who belong to the root users (group number 0), you could use this script:

```
$ gawk -F '$4 == 0{print $1}' /etc/passwd
root
sync
shutdown
halt
$
```

The script checks for records where the fourth data field contains the value 0. On Linux system there are five user accounts that belong to the root user group.

You can use any of the normal mathematical comparison expressions:

+   - x = y: Value is equal to y.
- x <= y: Value is less than or equal to y.
- x < y: Value is less than y.
- x > y: Value is greater than or equal to y.
- x >= y: Value is greater than y.

You can also use expressions with text data, but you must be careful. Unlike regular expressions, expressions are an exact match. The data must match exactly with the pattern:

```
$ gawk -F, '$1 == "data"{print $1}' datal
$
$ gawk -F, '$1 == "dataall"{print $1}' datal
$
```

The first test doesn't match records as the first data field value isn't in any of the records. The second test matches one record with the root dataall.

# Structured Commands

The gawk programming language supports the usual cast of structured programming commands. This section describes each of these commands and demonstrates how to use them within a gawk environment.

# The if statement

The gawk programming language supports the standard if-then-else format of the if statement. You must define a condition for the if statement to evaluate, enclosed in