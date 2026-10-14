Another useful command option for ls is -a, which causes all files to be listed—even hidden ones.

Command options can be combined together. To do so, simply list them one after the other. To see all details about files, and also any hidden files, we would type ls -la.

ls -la is a very common command used by many Linux users daily.

Command options are usually letters, but sometimes words are used too. In fact, to view a quick list of options, you can use the --help command option (that's two hyphens, rather than one). For example, ls --help, or cp --help. This option works with virtually all commands.

# Complex filenames

Filenames with spaces in them present problems because a space between items on a command-line is taken as an indication that command arguments or options follow.

For example, the rm command is used to delete files. If we wanted to delete a file called third_quarter_report.doc, and typed rm third quarter_report.doc, we'd see the following series of error messages:

```
rm: cannot remove 'third': No such file or directory
rm: cannot remove 'quarter': No such file or directory
rm: cannot remove 'report.doc': No such file or directory
```

In other words, the rm command interprets each word in the filename as a separate argument—it thinks you want to delete a file called third, a file called quarter, and a file called report.doc.

The solution is simple—just wrap any file or folder name containing spaces in quotation marks:

```
rm "third quarter report.doc"
```

This should be done for file/folder names that include symbols too.

> TIP Another method of dealing with spaces or symbols is to escape them. This involves typing a backslash (\ ) before each space or symbol. To delete the above file, you could type rm third\ quarter\ report.doc. Most times quotation marks work fine.

# Relative and absolute paths

A path is simply the part of a file or folder listing describing where it is located in the filesystem—/home/keir/Documents/report.doc, for example. Paths can be expressed in two ways: relative and absolute.