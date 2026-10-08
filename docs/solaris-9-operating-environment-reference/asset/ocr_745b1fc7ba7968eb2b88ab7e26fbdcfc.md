Printer-generated error messages received at any time while establishing the initial connection (or when running interactive mode) exit postio with a non-zero status. In addition to being added to the log file, printer error messages are also echoed to standard error.

# Examples

The following example runs as a single process at 9600 baud and sends file1 file2 to the printer attached to /dev/tty01.

```
castle@ postio -1 /dev/tty01 file1 file2
```

The following example is the same as the previous one that two processes are used, the internal buffer is set to 4096 bytes, and returned by the printers put in file log.

```
castle@ postio -R 2 -B 4096 -1/dev/tty01 -L log file
```

The following example establishes an interactive connection with the printer at Datakit destination my/printer.

```
castle@ postio -i -1 my/printer
```

The following example sends file program to the printer connected to /dev/tty22, recovers any data in file results, and puts messages in file log.

```
castle@ postio -t -1 /dev/tty22 -L log program >results
```

# Exit Status

+   0 Successful completion.
non-zero An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type Attribute Value |
| Availability SUNwps |

# See Also

download(1), dpost(1), postdaisy(1), postmd(1), postmd(1), postprint(1), postreverse(1), posttek(1), attributes(5)

# postmd — Matrix Display Program for PostScript Printers

# Synopsis

```
/usr/lib/lp/postmd [-b num] [-c num] [-d dimen] [-g list] [-i list]
[-m num] [-n num] [-o list] [-p mode] [-w window] [-x num] [-y num]
[file...]
/usr/lib/lp/postscript/postmd *
```