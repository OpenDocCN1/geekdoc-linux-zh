# cd

cd stands for change directory. You will find this command extremely useful. The three typical ways of using this command are

+   * cd .. Moves one directory up the directory tree.
+   * cd - Moves to your home directory from wherever you currently are. This is the same as issuing cd by itself.
+   * cd directory name Changes to a specific directory. This can be a directory relative to your current location or can be based on the root directory by placing a forward slash (/) before the directory name.

These examples can be combined. For example, suppose you are in the directory /home/dsp1234 and want to go to tng4321's home account. You can perform the following command to move back up the directory one level and then down into the tng4321 directory:

```
cd ../tng4321
```

# chfn

The chfn command changes finger information. You can use this command to enter or update information used by the finger networking tool from the /etc/passwd entry for your Linux system. You can enter full names, offices, and office and home phone numbers. Follow chfn by a user's name:

```
# chfn Willie
```

# chgrp

The chgrp command is used to change the group associated with the permissions of the file or directory. The file's owner (and, of course, root) has the authority to change the group associated with the file. The format for the command is simply this:

```
chgrp <new group> <file>
```

# chmod

The chmod command is used to change the permissions associated with the object (typically a file or directory). What you are really doing is changing the file mode. You can specify the permissions of the object in two ways: by the numeric coding system or by the letter coding system. If you recall, three sets of users are associated with every object: the owner of the object, the group for the object, and everybody else. Using the