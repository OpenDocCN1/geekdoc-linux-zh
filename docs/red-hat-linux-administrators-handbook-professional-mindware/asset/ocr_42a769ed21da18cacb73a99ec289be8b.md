Using cat, you can append a file to another existing file. For instance, if you had forgotten to add names4 in the previous command, you could still produce the same results by executing

```
cat names4 >> allnames
```

to append names4 to allnames.

# chmod

Syntax: chmod [ -R ] *permission-mode*  *file or directory*

The chmod command is used to change the permission mode of a file or directory. The permission mode is specified as a three- or four-digit octal number. For example,

```
chmod 755 myscript.pl
```

changes the permission of myscript.pl script to 755 (rwxr-xr-x), which allows the file owner to read, write, and execute and allows only read and execute privileges for everyone else. As another example,

```
chmod -R 744 public_html
```

changes the permissions of the public_html directory and all of its contents (files and subdirectories) to 744 (rwxr-r--), which is a typical permission setting for personal Web directories that are accessed using http://server/~username URLs under Apache server. The -R option tells chmod to recursively change permissions for all the files and directories under the named directory.

# chown

Syntax: chown [ -fhr ] *Owner* [ : *Group* ] [ *File* . . . ] [ *Directory* . . . ]

The chown command changes the owner of the file specified by the File parameter to the user specified by the Owner parameter. The value of the Owner parameter can be a user ID or a login name found in the /etc/ passwd file. Optionally, a group can also be specified. The value of the Group parameter can be a group ID or a group name found in the /etc/ group file.