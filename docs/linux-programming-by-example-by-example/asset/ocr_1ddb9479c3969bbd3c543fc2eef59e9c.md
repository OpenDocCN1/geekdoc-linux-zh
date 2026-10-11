execute privileges; a value of 2 corresponds to read privileges; and a value of 4 corresponds to write privileges. The file in Figure 7.2 is readable and executable for the group and other, and readable/writable/executable for the owner, root.

# The Modifer Bit

The fourth bit in the file mode is the file mode modifier; it indicates whether the file is setuid, setgid, or sticky. As discussed in Chapter 4, "Processes," when a process executes a setuid or setgid file, its effective UID or GID is set to the file's owner or group, respectively. When a file's sticky bit is set (indicated by an uppercase S in the fourth bit), it forces the kernel to try to keep the file in memory as long as possible (hence the name, sticky), even if it is not being executed, because this reduces execution time. The modifier bit of the file in Figure 7.2 is not set, so the file is neither setuid, setgid, nor sticky.

> **NOTE**
> A file's modifer and permission bits are bitmasks, or integers that are manipulated and evaluated at the bit level using C's bit manipulation functions, such as << (left-shift) ~ and (bitwise complement). Fortunately, Linux provides a set of macros and symbolic constants (see Table 7.1) that make it easy to decode a file's mode.

*Table 7.1: File Access and Modifer Bitmask Macros*
| Name | Mask | Description | POSIX |
| :--- | :--- | :--- | :--- |
| S_ISUID | 0004000 | Set UID bit | Yes |
| S_ISGID | 0002000 | Set GID bit | Yes |
| S_ISVTX | 0001000 | Sticky bit | No |
| S_IRWXU | 00700 | User (owner) has read/write/execute permission | Yes |
| S_IRUSR | 00400 | User has read permission | Yes |
| S_IWUSR | 00200 | User has write permission | Yes |
| S_IXUSR | 00100 | User has execute permission | Yes |
| S_IRWXG | 00070 | Group has read/write/execute permission | Yes |
| S_IRGRP | 00040 | Group has read permission | Yes |
| S_IWGRP | 00020 | Group has write permission | Yes |
| S_IXGRP | 00010 | Group has execute permission | Yes |
| S_IRWXO | 00007 | Others have read/write/execute permission | Yes |

*continues*