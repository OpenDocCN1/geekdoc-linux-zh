The basic structure is: find name STRING -print | cpio -o OPTIONS > DIRECTORY.

In this structure:

+   The -name option for find lets you search for a string enclosed in double quotation marks. Metacharacters can be used. See “Using Metacharacters or Wild Cards,” page 118.

+   The bar character (|) redirects the output of find to cpio.

+   The -o flag sets cpio to create an archive file for backing up.

+   The target is a directory.

+   The > redirection operator redirects files to the location for the back up. Typically, this location is on a removable device.

# ## The -o Flag in the cpio Command (Backup)

| Option | Action | Comments |
| :--- | :--- | :--- |
| -A --append | Adds files to an existing archive. | |
| -v --verbose | Displays progress on screen. | |

# ## Restoring Files Using the cpio Command

To restore files from an archive file, use cpio with a redirection pipe. Type: cpio -i OPTIONS STRING < TARGET.

In this example:

+   The -i flag sets cpio to restore files.

+   The string describes the files to restore. Metacharacters can be used. See “Using Metacharacters or Wild Cards,” page 86.