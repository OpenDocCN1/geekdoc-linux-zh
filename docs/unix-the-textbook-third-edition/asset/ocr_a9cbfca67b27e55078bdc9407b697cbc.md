# TABLE 5.1 Summary of File Permissions in UNIX

| User Type | Permission Type |  |  |
|---|---|---|---|
|  | Read (r) | Write (w) | Execute (x) |
| User (u) | X | X | X |
| Group (g) | X | X | X |
| Others (o) | X | X | X |

shell scripts, as setting it for any other type of file does not make any sense. We discuss the purpose of execute permission on a directory in Section 5.4.3.

With three categories of file users and three types of permissions for each user type, a UNIX file has nine types of permissions associated with it, as shown in Table 5.1. Note that permissions are read across row by row. As stated in Chapter 4, access privileges are stored in a file's inode.

The value of X can be 1 (permission granted) or 0 (permission not granted). Thus, one bit is needed to represent a permission type and a total of three bits are needed to indicate file permissions for one type of user. In other words, a user of a file can have one of the eight (2³) possible types of permissions for a file at a given time. Octal numbers can represent these eight three-bit access permission values from 0 to 7, as shown in Table 5.2. Access permissions 0 (binary 000) and 7 (binary 111) mean no access permissions and all permissions, respectively.

The nine bits needed to express permissions for the three types of file users result in the possible access permission values of three-digit octal numbers 000–777 for file permissions. The first octal digit specifies permissions for the owner of the file, the second digit specifies permissions for the group that the owner of the file belongs to, and the third digit specifies permissions for everyone else. In the output of the ls -l command, a bit value of 0 for a permission is displayed as a dash (-), and a value of 1 is displayed as r, w, or x, depending on the position of the bit according to the table. Thus a permission value of 0 in octal (no permissions granted) for a user of a file can be written as --- and a permission of 7 (all three permissions granted) can be denoted as rwx. The outputs of the ls -l commands in the following session show that the /etc/passwd file is read-only for everyone on the system

# TABLE 5.2 Possible Access Permission Values for a File for a User, Their Octal Equivalents, and Their Meanings

| r | w | x | Octal Digit for Permission | Meaning |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | No permission |
| 0 | 0 | 1 | 1 | Execute-only permission |
| 0 | 1 | 0 | 2 | Write-only permission |
| 0 | 1 | 1 | 3 | Write and execute permissions |
| 1 | 0 | 0 | 4 | Read-only permission |
| 1 | 0 | 1 | 5 | Read and execute permissions |
| 1 | 1 | 0 | 6 | Read and write permissions |
| 1 | 1 | 1 | 7 | Read, write, and execute permissions |