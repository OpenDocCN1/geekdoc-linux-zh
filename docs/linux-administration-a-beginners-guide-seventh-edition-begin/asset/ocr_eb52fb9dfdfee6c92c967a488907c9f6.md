# CHAPTER 3 The Command Line

If you want to change certain bits, you should use the symbolic mode of chmod. This mode turns out to be much easier to remember, and you can add, subtract, or overwrite permissions.

The symbolic form of chmod allows you to set the bits of the owner, group, and others. You can also set the bits for all three classes at the same time. For example, if you want to change a file foobar.sh so that it is executable (x) for the owner (u), you can run the following command:

```
[master@server ~$ chmod u+x foobar.sh
```

If you want to change the group's bit to execute, use the following:

```
[master@server ~$ chmod ug+x foobar.sh
```

If you need to specify different permissions for others, just add a comma and its permission symbols. For example, to make the foobar.sh file executable for the user and the group, also remove read, write, and executable permissions for all others, you could this:

```
[master@server ~$ chmod ug+x,o-rw foobar.sh
```

If you do not want to add or subtract a permission bit, you can use the equal (=) sign instead of plus (+) or minus (-) sign. This will write the specific bits of the file and erase any other bit for permission. The preceding examples used + to add the bit to User and Group fields. If you want only the execute bit, you would replace the + with =. You can also use a fourth character: a. This will apply the permission bits to all the fields.

The following list shows the most common combinations of the three permissions. Other combinations, such as -wx, also exist, but they are rarely used.

| Letter | Permission | Value |
|---|---|---|
| | No permissions | 0 |
| r- | Read only | 4 |
| rw- | Read and write | 6 |
| rwx | Read, write, and execute | 7 |
| r-x | Read and execute | 5 |
| --x | Execute only | 1 |

For each file, these of three-letter chunks are grouped together. The first chunk represents the permissions for the owner of the file, the second chunk represents the permissions for the file's group, and the last chunk represents the permissions for all users on the system. Table 3-3 shows some permission combinations, their numeric equivalents, and their descriptions.