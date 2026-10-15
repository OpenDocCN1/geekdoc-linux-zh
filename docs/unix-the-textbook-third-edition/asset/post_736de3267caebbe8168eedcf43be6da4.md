
## SYNTAX

```
umask [-S] [mask]
```

Purpose: Set access permission bits for newly created files and directories to 0, if the corresponding bit in the mask is set to 1. Other permission bits are determined by using a Boolean logic expression involving the values of the mask and default permissions. Without any argument, the command displays the current value of the mask. With the -S option, the command displays the mask value in a symbolic form (see the following paragraphs).

When the command is executed without an argument, it displays the current value of the bit mask in octal, as shown in the first command of the following session. The rightmost nine bits (i.e., the rightmost three octal digits) are for user, group, and others, and the leftmost three bits (i.e., the leftmost octal digit) are for special access bits described in Section 5.6 below. The umask -S command displays the symbolic value of the mask, showing the access privileges that will be set for a newly created directory or executable file for user, group, and others.

```
$ umask
0022
$ umask -S
u=rwx,g=rx,o=rx
$
```

When used with a mask as an argument, the umask command can be used to set the mask value. The mask value may be specified as a three-digit or four-digit octal number. In the following session, we show how the umask command can be used without and with the -S option.

```
$ umask 077
$ umask
0077
$ umask -S u=rwx,g=,o=
$ umask
0077
$
```

The umask command is normally placed in the system startup file ~/.profile in System V UNIX and the ~/.login or ~/.cshrc file in BSD UNIX, so that it executes every time you log on to the system.

The argument of umask is a bit mask, specified in octal, that identifies the permission bits that are to be turned off when a new file is created. The values of other access permission bits are computed by the Boolean expression

```
A = B AND C' = BC'
```

Here, A is the file access permissions assigned to a newly created file or directory, B is the default access permission (777 for a directory or executable file and 666 for a text file), and C is the current mask value. C' (pronounced "NOT C" or "C prime") is called negation, or 1's complement of C. The 1's complement of a binary number is obtained by replacing 1s with 0s and vice versa. For example, the 1's complement of the four-bit binary number 1011 is 0100. The bitwise Boolean function AND of two binary variables returns 1 if and only if both the bits are 1; it returns 0 otherwise. While computing A in the above equation, the AND function compares the respective bits in B and C' and returns a 1 if and only if both bits are 1; otherwise it returns 0.

We now show a few examples how UNIX assigns file access permissions to newly created files and directories for a given mask. We determine the access permissions for a newly created directory or executable file for the mask value 022 by using the above Boolean expression.

```
C = 022      = 000 010 010
C'           = 111 101 101
B = 777      = 111 111 111
A = B AND C' = 111 101 101 = 755 (octal) = 111101101 (binary)
                    rwxr-xr-x (symbolic)
```

Thus, file access permissions are 755 (read, write, execute for user, read and execute for group and others). For a text file, B is 666. Thus, access permissions for a newly created text file would be 644, as follows:

```
C'           = 111 101 101
B = 666      = 110 110 110
A = B AND C' = 110 100 100 = 644 (octal) = 110100100 (binary)
                    rw-r--r-- (symbolic)
```

The access permissions for a newly created text file for the mask value 077 would be 600, as follows:

```
C = 077      = 000 111 111
C'           = 111 000 000
B = 666      = 110 110 110
A = B AND C' = 110 000 000 = 600 (octal)
                    rw------ (symbolic)
```

We now do a Bourne shell session to verify the above results. Note that with the mask set to 022, the permissions for the newly created directory (labs) and executable file (hello) are 755 (rwxr-xr-x), and are 644 (rw-r--r--) for the newly created text file, tempfile, as calculated above. With the mask set to 077, the permissions for the directory (lectures) and executable file (greeting) are 700 (rwx------), and are 600 (rw------) for the text file (textfile).
