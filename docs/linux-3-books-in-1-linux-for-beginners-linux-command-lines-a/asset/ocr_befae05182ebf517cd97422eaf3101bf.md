# The mv command

The mv Linux command performs movement and renaming of files based on how a user uses it. The original filename does not exist after you have executed the command. The mv command is used in the same way as the cp command.

```
mv file1 file2
```

Just like the cp command, the mv command comes with different options that are given as under:

+   •  The mv command option -u or --update is used when you are moving from one directory to another, and you are moving files that do not exist or newer to the files in the destination directory.

+   •  The mv command option -Y or --verbose is used to display informative messages as you perform the movement.

+   •  The mv command option -i or --interactive is used before overwriting existing files, which prompt the user for confirmation. If you have not specified the option, the mv command will overwrite the existing files, which is not good for your document records.

# Examples for mv command

+   •  the Linux command mv item1 item2 will copy the files of item1 to the files of item2. If item2 exists, it will be overwritten with the contents of item1. If it does not exist, the system will create it. The file item1 will cease to exist in either case.

+   •  the Linux command mv -i item1 item2 will move the files of item1 to the files of item2. However, the only exception is that if item2 exists, the user will be prompted before the file is overwritten.

+   •  the Linux command mv item1 item2 dir1 will move contents of item1 and item2 into dir1. The directory dir1 must exist before you execute this command.

+   •  the Linux command mv dir1* dir2 uses a wildcard. It will move