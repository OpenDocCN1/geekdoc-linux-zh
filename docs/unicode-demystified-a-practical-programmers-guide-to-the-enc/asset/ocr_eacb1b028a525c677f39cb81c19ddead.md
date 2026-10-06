# umask

Establishes the file-creation permissions mask

```
umask [mask]
```

The umask builtin specifies a mask that the system uses to set up access permissions when you create a file. This builtin works slightly differently in each of the shells.

# Arguments

The mask can be a three-digit octal number or a symbolic value such as you would use with chmod (page 1103). The mask specifies the permissions that are not allowed.

When mask is an octal number, the digits correspond to permissions for the owner of the file, members of the group the file is associated with, and everyone else. Because the mask specifies the permissions that are not allowed, the system subtracts each of these digits from 7 when you create a file. The result is three octal numbers that specify the access permissions for the file (the numbers you would use with chmod). A mask that you specify as a symbolic value also specifies the permissions that are not allowed. See "Notes."

Without any arguments, umask displays the file-creation permissions mask.

# Notes

Most utilities and applications do not attempt to create files with execute permissions, regardless of the value of mask; they assume that you do not want an executable file. The effective result is that when a utility or application, such as touch, creates a file, the system subtracts each of the digits in mask from 6. An exception is mkdir, which assumes that you want the execute (access in the case of a directory) bit set. See the "Examples" section.

The umask program is a builtin in bash, tsh, and zsh and generally goes in the initialization file for your shell (.profile, .zprofile, or .login).

Under bash and zsh the argument g=r,o turns off the write bit in the mask for groups and other users (the mask is 0033), causing those bits to be off in file permissions (744 or 644). Refer to chmod on page 1103 for more information about symbolic permissions.