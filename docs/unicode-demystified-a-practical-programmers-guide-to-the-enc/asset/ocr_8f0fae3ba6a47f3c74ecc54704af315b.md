# # rm

Removes a file (deletes a link)
*rm [options] file-list*

The rm utility removes hard and/ symbolic links to one or more files. When you remove the last hard link to a file, the file is deleted. Refer to Chapter 4 for more information about hard and symbolic links.

> ### Use Caution When You Use rm with Wildcards
> Because you can remove a large number of files with a single command, use rm cautiously, especially when you are using an ambiguous file reference. If you are in doubt about the effect of an rm command with an ambiguous file reference, first use echo with the same file reference to evaluate the list of files the reference generates.

# ## Arguments

The file-list contains the list of files that rm deletes.

# ## Options

+   - force f Without asking for your consent, this option removes files for which you do not have write access permission. It also suppresses informative output if a file does not exist.

+   - Interactive i Asks before removing each file If you use --recursive with this option, rm also asks you before examining each directory.

+   - recursive Deletes the contents of the specified directory, including all subdirectories, and the directory itself. Use this option cautiously.

# ## Notes

To delete a file, you must execute and have access permission to the parent directory of the file, but you do not need read or write access permission to the file itself. If you are running rm interactively (that is, rm's standard input is coming from a keyboard) and you do not have access permission to the file your