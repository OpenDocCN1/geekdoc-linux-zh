# 7.7 Using Variables

All operating system shells use environment and shell variables to define user environment characteristics. As part of the set-up process, your system administrator has provided default environment and shell variable values in the appropriate login scripts.

For most users, the default environment and shell variable values are sufficient. As you become more familiar with the system, however, you may want to modify some values. For example, you may want to reset the variable that defines your shell prompt so that it is more personalized. You also may want to set a shell variable that specifies a very long directory pathname so that you can save time keying commands that use the directory (see the examples in Section 7.7.1). You also may find setting variables useful when writing shell procedures. You will find that you may use variables creatively to enhance your work environment.

Some environment variables may be reset and some are read-only and cannot be reset. That is, these variables can be used, but not modified. For more information on this topic, see the appropriate shell reference page; sh(1b), sh(1p), csh(1), or ksh(1).

To reset environment variables as well as define your own shell variables, do one of the following:

+   - Edit the appropriate local login script if you want these values set for you whenever you log in. For more information, see Section 7.6.
+   - Set the environment variables on the command line if you want these values set only for the current login session.

At any time, you may reference the value of any variable as well as display its value. You also may clear the value of any variable.

# 7.7.1 Setting Variables

The following sections describe how to set, reference, display, and clear variable values.

# 7.7.1.1 Bourne, Korn, and Posix Shell Variables

In the Bourne, Korn, and POSIX shells, you set variables with an assignment statement. The general format for setting variables is the following:

```
`name = value`
```

The name entry specifies the variable name. The value entry specifies the value assigned to the variable. Be sure you do not enter spaces on the command line.