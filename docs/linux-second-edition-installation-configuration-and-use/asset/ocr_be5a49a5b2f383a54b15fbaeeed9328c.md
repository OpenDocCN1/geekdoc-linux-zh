# COMMAND REFERENCE

```
write linux.file dos.file
```

write copies the specified file from the Linux file system onto an MS-DOS diskette. command is a restricted variation of mcopy, which allows copying in both directions.

# nice [options] program

nice starts the specified program with reduced or increased priority. the command is normally used to start programs that are not too time-critical (background programs) with a low priority in order not to affect the rest of the system too.

+   - sets the nice value. as standard (that is, without nice) programs are started with a value of 0. a value of -20 means highest priority, a value of +19 lowest priority. values less than 0 can only be specified by root, that is, most users can only use nice to start programs with reduced priority. without option, nice starts the program with a nice value of +10.

# nl [options] file

nl numbers all non-empty lines of the specified text file. by setting the various options, numbering can be obtained page by page, for headers and footers.

# passwd [user_name]

passwd without parameters allows the password of the current user to be changed. first the old password must be entered, then the new password in succession. the new password is registered in encrypted form the /etc/passwd file. each user has the right to modify his/her own password. however, the password must be at least six characters long and it must contain either digits or both upper and lower case letters.

when passwd is called with a user name, that user's password can be altered. the old password does not have to be specified, that root can change the password even if the user has forgotten his/her password. the above restrictions do not apply to root, that root can define a password consisting of a single character. however, not even root is allowed to specify no password at all (that is, to enter nothing but --).

if you want the password to be skipped altogether for specific users (for example, as root) you can delete the password data from the text file /etc/passwd. the data is located between the first and second colons, that is, immediately after the user name.

# paste file1 file2 ...

paste combines the lines of the specified files into new (longer) lines and displays the result on screen. thus, the first line of the resulting text is composed of the first