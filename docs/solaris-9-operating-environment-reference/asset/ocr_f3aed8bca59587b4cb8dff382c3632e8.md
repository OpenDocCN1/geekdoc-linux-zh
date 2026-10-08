# 1028

# pax

# read

When you specify -r but not -w, extract the members of the archive file from the standard input with path names matching the specified patterns. If an extracted file is of type directory; extract the file hierarchy rooted at that file as well. Create the extracted files relative to the current file hierarchy. The ownership, access and modification times, and file mode of the restored files are discussed under the -p option.

# write

When you specify -w but not -r, write the contents of the file operands to the standard output in an archive format. If you specify no file operands, read a list of files to copy, one per line, from the standard input. A file of type directoryincludes all of the files in the file hierarchy rooted at the file.

# copy

When you specify both -r and -w, copy the file operands to the destination directory.

If you specify no file operands, read a list of files to copy, one per line, from the standard input. A file of type directoryincludes all of the files in the file hierarchy rooted at the file.

The effect of the copy is as if the copied files were written to an archive file then subsequently extracted, except that there may be hard links between the original and the copied files. If the destination directoryis a subdirectory of the files to be copied, the results are unspecified. It is an error if directorydoes not exist, is not writable by the user, or is not a directory.

In read copy modes, if intermediate directories are needed to extract an archive member, pax performs actions equivalent to the mkdir(2) function, called with the following arguments:

+   * Use the intermediate directory as the path argument.

+   * Use the octal value of 777 or rwx (read, write, and execute permissions) as the mode argument (chmod(1)).

If any specified pattern file operands are not matched by least one file or archive member, pax writes a diagnostic message to standard error for each one that did not match and with a non-zero exit status.

The supported archive formats are automatically detected on input. The default output archive format is tar(1).

If the selected archive format supports the specification of linked files, it is an error if these files cannot be linked when the archive is extracted. Any of the various names in the archive that represent a file can be used to select the file for extraction.

# Options

+   -r
Read an archive file from standard input.

+   -w
Write files to the standard output in the specified archive format.