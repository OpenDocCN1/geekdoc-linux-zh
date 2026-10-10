# ## EXIT STATUS

The command uses `sysexits.h` return values for everything, except when using either of the options `-n` or `-w` which report a failure to acquire the lock with a return value given by the `-E` option, or 1 by default.

When using the `command` variant, and executing the child worked, then the exit status is that of the child command.