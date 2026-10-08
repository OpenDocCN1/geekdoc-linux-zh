# umask

(umask 002)
nohup umask...
find . -exec umask...

it does not affect the file-mode creation mask of the caller's environment. For this reason, you cannot use /usr/bin/umask to change the umask in an ongoing session. Its usefulness is limited to checking the caller's umask. To change the umask of an ongoing session, use one of the shell built-ins.

If you do not specify the umask order, the umask command displays to standard output the value of the invoking process file-mode creation mask.

# Bourne and C Shells

Set the file-mode creation mask for ooo. The three octal digits refer to read/write/execute permissions for owner, group, and other (see chmod(1), chmod(2), and umask(2)). The value of each digit is subtracted from the corresponding digit specified by the system for the creation of a file (see create(2)). For example, umask 022 removes write permission for group and other (file created with 777 become 775; files created with 666 become 644).

+   - If you omit ooo, the current value of the mask is displayed.
- umask is recognized and executed by the shell.
- To automatically set the permissions on created files or directories, you can include umask in your .profile for the Bourne shell (see profile(4)) or in your .shrc file for the C shell. These initialization files are invoked at login.

# Korn Shell

Set the file-mode creation mask for mask. mask can either be an octal number or a symbolic value as described in chmod(1). If you omit umask, the current value of the mask is printed.

# Options

+   -S Specify umask as a symbolic argument.

The default output style is unspecified but recognized in a subsequent invocation of umask on the same system as a umask operand to restore the previous file-mode creation mask.

# Operands

mask A string specifying the new file-mode creation mask. The string is treated in the same way as the mode operand described in the chmod(1) manual page.

For a symbolic-value, the new value of the file-mode creation mask is the logical complement of the file bits bits of the file mode specified by the symbolic-string.

In a symbolic-mode value, the permissions + and - are interpreted relative to the current file-mode creation mask; + clears the indicated permissions in the mask; - sets the bits of the indicated permissions in the mask.

The interpretation of mode values that specify file bits other than the file permission bits is unspecified.

The file-mode creation mask is set to the resulting numeric value.