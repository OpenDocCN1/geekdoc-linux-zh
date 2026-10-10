+   ▪ x to assign execute permissions only if the object is a directory or if it already had execute permissions
+   ▪ s to set the SUID or SGID on execution
+   ▪ t to set the sticky bit
+   ▪ u to set the permissions to the owner's permissions
+   ▪ g to set the permissions to the group's permissions
+   ▪ o to set the permissions to the others’ permissions

Using these permissions looks like this:

```
$ chmod o+r newfile
$ ls -1 newfile
-rwxwrw-r-- 1 rich rich 0 Sep 20 19:16 newfile
$
```

The o+r entry adds the read permission to whatever permissions the everyone security level already had.

```
$ chmod u-x newfile
$ ls -1 newfile
-rw-rw-r-- 1 rich rich 0 Sep 20 19:16 newfile
$
```

The u-x entry removes the execute permission that the user already had. Note that the settings for the 1s command indicate if a file has execution permissions by adding an asterisk to the filename.

The options parameters provide a few additional features to augment the behavior of the chmod command. The -R parameter performs the file and directory changes recursively. You can use wildcard characters for the filename specified, changing the permissions on multiple files with just one command.

# ## Changing ownership

Sometimes you need to change the owner of a file, such as when someone leaves an organization or a developer creates an application that needs to be owned by a system account when it’s in production.