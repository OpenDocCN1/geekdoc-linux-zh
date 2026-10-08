# compress, uncompress, zcat 159

cautious because it assumes implementation extensions may be present that would allow user functions to exist when it is invoked; this capability is not specified by this document, but it is not prohibited as an extension. For example, the ENV variable precedes the invocation of the script with a user startup script. Such a script could define functions to spoof the application.

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of command: LC_CTYPE, LC_MESSAGES, and NLSPATH.

PATH Determine the search path, used during the command search, except as described under the -p option.

# Exit Status

When you use the -v or -V options, the following exit values are returned:

+   - 0 Successful completion.

+   - >0 The command-name could not be found, or an error occurred.

Otherwise, the following exit values are returned:

+   - 126 The command specified by command-name was found but could not be invoked.

+   - 126 An error occurred in the command command, or the command specified by command-name could not be found.

Otherwise, the exit status of command is that of the simple command specified by the arguments to command.

# Attributes

attributes(5) for descriptions of the following attributes

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcsu |

# See Also

sh(1), type(1), attributes(5)

# compress, uncompress, zcat — Compress, Uncompress Files or Display Expanded Files

# Synopsis

```
/usr/bin/compress [-fv] [-b bits] [file...]
/usr/bin/compress [-cfv] [-b bits] [file]
/usr/bin/uncompress [-cfv] [file...]
/usr/bin/zcat *
```