about the filesystem, including the maximum number of characters allowed in a filename (Namlen in the following example). See the stat man page for more information.

```
$ stat -f /dev/sda
  File: "/dev/sda"
  ID: 0          Namlen: 255   Type: tmpfs
  Block size: 4096   Fundamental block size: 4096
  Blocks: Total: 127271   Free: 127207   Available: 127207
  Inodes: Total: 127271   Free: 126600
```

# ## umask: SPECIFIES THE FILE PERMISSION MASK

The umask shell builtin specifies the mask the system uses to set up access permissions when it creates a file. A umask command has the following format:

    umask [mask]

where mask is a three- or four-digit octal number or a symbolic value such as you would use with chmod (page 193). A mask value that you specify using octal numbers specifies the permissions that are not allowed; the digits correspond to the permissions for the owner of the file, members of the group the file is associated with, and every-one else. Because mask specifies the permissions that are not allowed, the system uses binary arithmetic to subtract each of the three digits from 7 when you create a file. If the file is an ordinary file (and not a directory), the system then removes execute permissions from the file. The result is three or four octal numbers that specify the access permissions for the file (the numbers you would use with chmod).

You must use binary or octal arithmetic when performing permissions calculations. To calculate file permissions given a umask value, subtract the umask value from octal 777. For example, assume a umask value of 003:

```
777       starting permissions for calculation
–003      subtract umask value
774       resulting permissions for a directory
111       remove execute permissions
664       resulting permissions for an ordinary file
```

To calculate permissions for a directory, umask subtracts the umask value from 777: In the example where umask has a value of 003, octal 7 minus octal 0 equals octal 7 (for two positions). Octal 7 minus octal 3 equals octal 4. Or using binary arithmetic, $111 - 011 = 100$. The result is that the system gives permissions of 774 (rwxrwxr-- →) to a directory.

To calculate permissions for an ordinary file, the system changes the execute bit (001 binary) to 0 for each position. If the execute bit is not set, the system does not change the execute bit. In the example, removing the execute bit from octal 7 yields octal 6 (removing 001 from 111 yields 110; two positions). Octal 4 remains octal 4 because the execute bit is not set (the 001 bit is not set in 100, so it remains 100). The result is that the system gives permissions of 664 (rw-rw-r-- →) to an ordinary file.