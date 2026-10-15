# su—become superuser or another user

```
su [ - ] [ username [ arg ... ] ]
```

su allows one to become another user without logging off. The default username is root (superuser). To use su, the appropriate password must be supplied (unless the invoker is already root). If the password is correct, su creates a new shell process that has the real and effective user ID, group IDs, and supplementary group list set to those of the specified username. The new shell will be the shell specified in the shell field of user name's password file entry. If no shell is specified, sh (Bourne shell) is used. To return to normal user ID privileges, type Ctrl-D to exit the new shell. The - option specifies a complete login.

# sum—calculates a checksum for a file

# sync—updates the superblock and sends changed blocks to disk

# tabs—sets tab stops on a terminal

# tail—displays the tail end of a file

```
tail +[-number [ lbc ] [ f ] ] [ filename ]
tail +[-number [ l ] [ rf ] ] [ filename ]
```

When a plus sign precedes the number, tail displays blocks, characters, or lines counting from the beginning of the file. If a hyphen precedes the number, tail counts from the end of the file.

# EXAMPLE A.35

+   1. tail +50 filex
+   2. tail -20 filex
+   3. tail filex

# EXPLANATION

+   1. Displays contents of filex starting at line 50.
+   2. Displays the last 20 lines of filex.
+   3. Displays the last 10 lines of filex.

# talk—allows you to talk to another user

```
talk username [ ttyname ]
```

talk is a visual communications program that copies lines from your terminal to that of another user.