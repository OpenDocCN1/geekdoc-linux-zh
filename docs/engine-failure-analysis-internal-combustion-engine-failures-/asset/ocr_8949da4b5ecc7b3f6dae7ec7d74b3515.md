# chgrp

```
chgrp [ option ] group file
```

Change the ownership of the specified file to the specified group. To specify the group owner, you can supply group names or ID numbers. This command requires superuser status (see su, in Chapter 1).

See also chown.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -c, --changes | Display messages only when changes are made |
| -f, --silent, --quiet | Hide messages |
| -h, --no-dereference | Change symbolic links, not the file to which the symbolic links point |
| --help | Display available options |
| -R, --recursive | Change ownership in the current directory and all associated subdirectories |
| --reference=filename | Use the group of the specified reference filename |
| -v, --verbose | Display messages concerning all processed files |
| --version | Display the version number |

# EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| chgrp games puzzle | Makes the specified group (games) the owner of puzzle. |
| chgrp -R authors *.doc | Makes the specified group (authors) the group owner of all files with the .doc extension located in the current directory and all of its associated directories. |