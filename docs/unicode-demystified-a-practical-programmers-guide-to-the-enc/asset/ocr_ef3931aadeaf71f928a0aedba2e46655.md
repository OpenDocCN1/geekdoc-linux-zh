# tar

Stores or retrieves files to/from an archive file

tar option [modifiers] [file-list]
The tar (tape archive) utility creates, adds to, lists, and retrieves files from an archive file.

# Options

Use only one of the following options to indicate what type of action you want to take. You can affect the action of the option by following it with one or more modifiers.

+   --append -r Writes the file-list to the end of the archive. This option leaves files as-already ready in the archive, so duplicate copies of files may be in the archive after tar finishes. When tar extracts the files, the last copy of file in the archive is the one that ends up

+   --create -c This option takes the file-list given on the command line and stores the named files in a new archive. If the archive already exists, it is destroyed before the new archive is created. If a file-list argument is a directory, tar recursively copies the files within the directory into the archive. The following command copies all the files on your system to the archive. Without the -f option the archive is created at /dev/rmt0:

```
$ tar -c /
```

+   --get -x Extracts the file-list from the archive and writes it to the disk. Any existing files with the same name are overwritten. Without a file-list, all the files in the archive are extracted. If the file-list includes a directory, tar extracts that directory and all the files below it. Tar utility attempts to keep the owner, modification time, and access privileges the same as those of the original file. If tar reads the file more than once, the later versions of the file overwrite previous versions.

+   --list -t table of contents Without a file-list, this option produces a table of contents of all the files in an archive. With a file-list, it displays the name of the files in the file-list each time it occurs in the archive. You can use this option with the --verbose option to display detailed information about each file in the archive.

+   --update -u Adds the files from file-list if they are not already in the archive or if they have been modified since they were last written to the archive. Because of the additional checking that this requires, tar runs more slowly when you use this option.

+   --help Displays a complete list of options and modifiers, with short descriptions of each.