# mkdir

Makes a directory
mdir [option] directory-list

The mkdir utility creates one or more directories.

# Arguments The directory-list contains one or more pathnames of directories that mkdir creates.

# Options

+   --mode mode -m mode Sets the permission to mode. You may use either the symbolic form or an octal number to represent the mode. Refer to page 1103 for more information on chmod.

+   --parents -p Creates any directories that do not exist in the path to the directory you wish to create.

# Notes

You must have permission to write to and search (execute permission) the parent directory of the directory you are creating. The mkdir utility creates directories that contain the standard invisible entries . and ..

# Examples The following command creates a directory named accounts as a subdirectory of the working directory and a directory named prospective as a subdirectory of accounts:

```
$ mkdir --parents accounts/prospective
Without changing working directories, the same user creates another subdirectory within the accounts directory:
$ mkdir accounts/existing
Next, the user changes the working directory to the accounts directory and creates one more subdirectory:
$ cd accounts
$ mkdir closed
The last example shows the user creating another subdirectory. This time the --mode option removes all access permissions for group and others:
$ mkdir --mode go= accounts/past_due
```