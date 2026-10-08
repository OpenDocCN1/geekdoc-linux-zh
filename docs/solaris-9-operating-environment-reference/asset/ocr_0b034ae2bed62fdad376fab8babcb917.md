# tar

# 1375

You cannot use the -r or -u option with quarter-inch archive tapes because these tape drives cannot backspace.

# Options

+   -I include-file

include include-file containing a list of files, one per line, and treat as if each file appeared separately on the command line. Be careful of trailing white spaces. When you also specify excluded files (see the X function modifier), they take precedence over all included files. If a file is specified in both the exclude-file and the include-file(or on the command line), exclude it.

+   -C directory file

Perform a change directory (see cd(1)) operation on directory and perform the c (create) or r (replace) operation on file Use short relative path names for file. If file is dot (.), archive all files in directory. This option enables archiving from multiple directories not related by a close parent.

# Operands

+   file

A path of a regular file or directory to be archived (when you specify the c, r, or u functions), extracted (x), or listed (t). When file is the path name of a directory, apply the action to all of the files and (recursively) subdirectories of that directory. The directory portion of file (see basename(1)) cannot exceed 155 characters. The file-name portion (see basename(1)) cannot exceed 100 characters.

When you archive a file and do not specify the E function modifier, the file name cannot exceed 256 characters. In addition, it may be possible to split the name between parent directory names so it is no longer than 155 characters and the name is no longer than 100 characters. With the E function modifier, you can specify a name of to PATH_MAX characters.

For example, you cannot archive a file whose basename is longer than 100 characters without using the E function modifier. You could archive a file directory portion is 200 characters and whose basename is 50 characters without using the E function modifier if the directory name contains a slash somewhere in character positions 151–156.

# Function Letters

Specify the function of the key with one of the following letters. Create by writing at the beginning of tarfile instead of at the end.

+   c

+   Replace by writing the named files at the end of tarfile.