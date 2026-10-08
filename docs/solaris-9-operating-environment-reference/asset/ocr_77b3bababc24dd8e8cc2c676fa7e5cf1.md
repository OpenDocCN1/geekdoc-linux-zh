# 1376

List the table of contents of the specified files each time they occur in tarfile. If you specify no file argument, list the names of all files in tarfile. With the v function modifier, display additional information for the specified files.

Update writing the named files at the end of tarfile if they are not already in tarfile or if they have been modified since last written to that tarfile. An update can be rather slow. You cannot update a tarfile created on a 5.x system on a 4.x system.

Extract or restore the named files from the archive and write them to the directory specified in tarfile relative to the current directory. Use the relative path names of files and directories to be extracted.

Absolute paths contained in the tar archive are unpacked with the absolute path names; that is, the leading slash (/) is not stripped.

If a name file matches a directory whose contents have been written to tarfile, extract this directory recursively. If possible, restore the owner, modification time, and mode; otherwise, you must be superuser

Only superuser can extract special character block devices (created by mknod). If you specify no file argument, extract the entire contents of tarfile If tarfile contains several files with the same name, write each file to the appropriate directory, overwriting the previous one. You cannot use file-name substitution wild-cards for extracting files from the archive; instead, use a command of the following form.

```
tar xvf... /dev/rmt/0 `tar tf... /dev/rmt/0 | grep 'pat-'`
```

When tapes created with the r or u functions are extracted, directory modification may not be set correctly. These same functions cannot be used with many drives because of tape drive limits such as the absence of backspace or append capabilities.

When you use the r, u, or x function modifier, the named files must exactly match the corresponding files in tarfile For example, to extract ./thisfile, you must specify ./thisfile, and not thisfile. The t function displays how each file was archived.

# Function Modifiers

You can use the characters below in conjunction with the letter that selects the desired function.

Blocking factor. When reading or writing to raw magnetic archives (see f). The block argument specifies the number of 512-byte blocks to be included in each read or write operation performed on tarfile. The minimum is 1, the default is 20. The maximum value is a function of the amount of memory available and the blocking