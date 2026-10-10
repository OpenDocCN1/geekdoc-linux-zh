# # umask

**Purpose:** Display/set a user's default file creation mask.

**Usage syntax:** `umask [OPTIONS] [MODE]`

```
$ umask
022

Displaying the current user's umask
```

**umask** controls a user's default file creation mask. This determines the permissions that will be assigned to newly created files and directories. To determine the file/directory creation mode the umask value is subtracted from 777 for directories and 666 for files. For example, a umask of 022 would create effective permissions of 644 (rw-r-x--) for files and 755 (rwxr-xr-x) for directories.

On some systems the `-S` option can be used to display a more user friendly symbolic output of the umask value, as shown in the next example.

```
$ umask -S
u=rwx,g=rx,o=rx

Displaying the umask in symbolic notation
```

The **umask** command can also be used to change the umask value as displayed in the next example.

```
$ umask 077

Setting the umask value
```

In this example, a umask value of 077 would create effective permissions of 600 (rw-------) for files and 700 (rwx------) for directories.

> **Note**  *A umask value specified on the command line is reset when you log out. To make the umask permanent you must add it to the `.*profile` file in the user's home directory or `/etc/profile` (for all users).*

**Common usage examples:**

|  |  |
| :--- | :--- |
| `umask` | Display the umask in octal format |
| `umask -S` | Display the umask in symbolic format |
| `umask [MODE]` | Set the umask to the specified value |