# timemanap 1409

The following two examples show the differences between the csh version of time and the version in /usr/bin/time. These examples use the C shell.

```
castle time find / -name core -print
/export/home/winsor/core
1.0u 13.0s 1:11 9% 0+0ic 0pf+0w
castle# /usr/bin/time find -name core -print
/export/home/winsor/core

real 1:10.2
user 1.0
sys 13.5
castle#
```

See csh(1) for an explanation of the format of time output.

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of time: LC_TYPE, LC_MESSAGES, LC_NUMERIC, NLSPATH, and PATH.

# Exit Status

If command is invoked, the exit status of time is the exit status of command; otherwise, the time command exits with one of the following values.

+   - 1-125 An error occurred in the time command.
- 126 command was found but could not be invoked.
- 127 command could not be found.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwcsu |

# See Also

csh(1), shell_builtins(1), timex(1), times(2), attributes(5), environ(5).

# Bugs

Elapsed time is accurate to the second, whereas the CPU times are measured to the 100th second. Thus, the sum of the CPU times can be up to a second larger than the elapsed time.

# timemanap — Front Ends to the mp Text to PDL Pretty Print Filter

# Synopsis

```
/bin/timemanp [options] filename...
```