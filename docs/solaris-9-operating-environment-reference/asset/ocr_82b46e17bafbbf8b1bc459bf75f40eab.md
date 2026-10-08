# priocntl 1109

If an argument operand cannot be completely converted into an internal value appropriate to the corresponding conversion specification, a diagnostic message is written to standard error and the command returns a 0 exit status, continues processing any remaining operands, and writes to standard output the value accumulated at the time the error was detected.

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of printf: LC_COLLATE, LC_CTYPE, LC_MESSAGES, LC_TIME, TZ, and NLSPATH.

# Exit Status

+   * 0 Successful completion.
* >0 An error occurred.

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability CSI | SUNWloc Enabled |

# See Also

awk(1), bc(1), echo(1), strtod(3C), strtol(3C), strt(3C), printf(3S), attributes(5), environ(5), formats(5)

# priocntl — Display or Set Scheduling Parameters of Specified Process(es)

# Synopsis

```
/usr/bin/priocntl -l
/usr/bin/priocntl -d [-i itype] [idlist]
/usr/bin/priocntl -s [-c class] [class-specific options] [-i itype]
  [idlist]
/usr/bin/priocntl -e [-c class] [class-specific options] command
  [argument]
```

# Description

priocntl (priority control) command to assign processes to a priority class and to manage priorities within a class. You can also use priocntl to display the current configuration information for the system process or to execute a command with specified scheduling parameters.

Processes fall into distinct classes with a separate scheduling policy applied to each class. The process classes currently supported are:

+   * Real-time.
* Timesharing.