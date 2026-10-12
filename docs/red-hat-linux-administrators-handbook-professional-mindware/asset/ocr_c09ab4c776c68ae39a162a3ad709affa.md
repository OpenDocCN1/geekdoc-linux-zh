You can find out what groups you are in by using the `groups` command without any argument. Like the `chown` command, `chgrp` also uses `-R` to recursively change group names of one or more files or directories.

# ## Setting file/directory permissions using octal numbers

Although using octal numbers is my favorite method for setting file/directory permissions, I must warn you that it involves bits. If you feel you are mathematically challenged, skip to the next section, which explains the same permissions using a much simpler access string.

Because an infrequently used numbering system (the *octal number system*) is used to explain access permissions, here is a small memory refresher on octal numbers. The octal number system uses eight digits as opposed to the commonly used ten digits of the decimal system. The octal digits are 0 through 7, and each digit can be represented by three bits (in binary system). Table 3-2 shows the binary equivalent for each octal digit.

### Table 3-2 Octal to Binary Conversion
| Octal | Binary |
|-------|--------|
| 0 | 000 |
| 1 | 001 |
| 2 | 010 |
| 3 | 011 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |

This table will be useful in understanding file/directory permissions. Figure 3-1 shows how you can visualize the permissions as four octal digits. Here, the first octal digit is the leftmost or most significant one.