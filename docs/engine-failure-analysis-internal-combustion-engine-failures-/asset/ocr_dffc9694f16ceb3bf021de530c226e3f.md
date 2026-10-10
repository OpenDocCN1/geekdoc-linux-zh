# OPTIONS (*CONT.*)

| Use This Option | To Do This |
| :--- | :--- |
| `--v`, `--verbose` | Show messages explaining what the command is doing. |
| `--version` | Display the version number. |

# EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `rm -iv essay1.doc` | Erases **essay1.doc**. |
| `rm -iv *.doc` | Erases all the files in the current directory that have the `.doc` extension. |
| `rm -iv *` | Erases all the files in the current directory. |
| `rm -R /home/suzanne/junk` | Erases the specified directory and all of its associated subdirectories, including any files that these directories contain. |

# rmdir

*rmdir [ option ] directory*

Removes the specified directory, but only if it is empty. To remove a directory that contains files, see *rm*.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `--ignore-fail-on-non-empty` | Continue processing even if one or more of the specified directories contains files |
| `-p`, `--parents` | Remove associated parent directories if they are emptied by the current command |
| `--verbose` | Display messages concerning each directory that is processed |
| `--help` | Display available options |