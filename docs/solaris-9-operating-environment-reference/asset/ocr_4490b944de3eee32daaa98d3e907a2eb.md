renice

1165

# Operands

ID A process ID, process group ID, or user name/user ID, depending on the option selected.

priority The value specified is taken as the actual system scheduling priority instead of as an increment to the existing system scheduling priority. Specifying a scheduling priority higher than that of the existing process can require appropriate privileges.

# Examples

The following example adjusts the system scheduling priority so that process IDs 987 and 32 have a lower scheduling priority.

```
castle% renice -n 5 -p 987 32
castle%
```

The following example adjusts the system scheduling priority so that group IDs 324 and 76 have a higher scheduling priority if the user has the appropriate privileges to raise the priority.

```
castle% renice -n 4 -g 324 76
castle%
```

The following example adjusts the system scheduling priority so that numeric ID 1002 and user ray have a lower scheduling priority.

```
castle% renice -n 4 -u 1002 ray
castle%
```

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of renice: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

+   0 Successful completion.
>0 An error occurred.

# Files

/etc/passwd  Map user names to user IDs.

# Attributes

attributes(5) for descriptions of the following attributes:

Attribute Type    Attribute Value
Availability      SUNMcs

# See Also

nice(1), passwd(1), priocntl(1), attributes(5), environ(5)