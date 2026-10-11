combinations are often expressed in octal, particularly for the `chmod` and `umask` commands. For example, file permissions `rw-r--r--` is equivalent to octal 0644 and `-rwxr-xr-x` is equivalent to octal 0755. (The leading 0 is C's notation for octal values.)

When you create a file, you must know the protections to be given to the new file. You can do this as a raw octal number if you choose, and indeed it's not uncommon to see such numbers in older code. However, it is better to use a bitwise OR of one or more of the symbolic constants from `<sys/stat.h>`, described in Table 4.5.

# TABLE 4.5
POSIX symbolic constants for file modes

| Symbolic constant | Value | Meaning |
| :--- | :--- | :--- |
| `S_IRWXU` | 00700 | User read, write, and execute permission. |
| `S_IRUSR` | 00400 | User read permission. |
| `S_IREAD` | Same as `S_IRUSR`. | |
| `S_IWUSR` | 00200 | User write permission. |
| `S_IWRITE` | Same as `S_IWUSR`. | |
| `S_IXUSR` | 00100 | User execute permission. |
| `S_IEXEC` | Same as `S_IXUSR`. | |
| `S_IRWXG` | 00070 | Group read, write, and execute permission. |
| `S_IRGRP` | 00040 | Group read permission. |
| `S_IWGRP` | 00020 | Group write permission. |
| `S_IXGRP` | 00010 | Group execute permission. |
| `S_IRWXO` | 00007 | Other read, write, and execute permission. |
| `S_IROTH` | 00004 | Other read permission. |
| `S_IWOTH` | 00002 | Other write permission. |
| `S_IXOTH` | 00001 | Other execute permission. |

The following fragment shows how to create variables representing permissions `-rw-r--` and `-rwxr-x-x` (0644 and 0755 respectively):

```
```
mode_t rw_mode, rwx_mode;

rw_mode  = S_IRUSR | S_IWUSR | S_IRGRP | S_IROTH;   /* 0644 */
rwx_mode = S_IRWXU | S_IRGRP | S_IXGRP | S_IXOTH;   /* 0755 */
```
```