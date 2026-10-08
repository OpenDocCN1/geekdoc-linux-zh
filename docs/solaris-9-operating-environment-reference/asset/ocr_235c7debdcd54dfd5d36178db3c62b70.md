# 1378

# tar

+   h Follow symbolic links as if they were normal files or directories.

+   i Normally, tar does not follow symbolic links.

+   k size Ignore directory checksum errors.

+   Use the size argument as the size of an archive in kilobytes. The option is useful when the archive is intended for a fixed-size medium such as a diskette. Large files are split across volumes if they do not fit in the specified size.

+   l Output error message if unable to resolve all links to the files being archived. If you do not specify 1, print no error messages.

+   m Modify the modification time of the file as the time of extraction. This function modifier is valid only with the x function

+   n Specify that the file being is not a tape device. Reading of the archive is faster because tar can randomly seek around the archive.

+   o Ownership. Assign to extracted files the user and group identifiers of the user running the program instead of those on tarfile. This behavior is the default for users other than root. If you do not set the o function modifier and if the user is root, the extracted files on the group and user identifiers of the files tarfile(showcmd1) for more information). The o function modifier is valid only with the x function

+   p Restore the files to their original mode and ACLs if applicable, ignoring the present umask(1). This is the behavior if you invoke p as superuser with the x function. If superuser, also extract and stick bit information and restore files with original owners and permissions instead of being owned by root. When you use this modifier with the c function, create ACLs in tarfile along with other information. Errors occur when a tarfile with ACLs is extracted from previous versions of tar.

+   q Suppress the addition of a trailing / on directory entries in the archive. Stop after extracting the first occurrence of the named file. tar normally continues reading the archive after finding an occurrence of a file.

+   v Verbose. Output the name of each file preceded by the function letter. With the t function, v provides additional information about the tarfile entries. The listing is similar to the format produced by the -l option of ls(1) command.

+   w What. Output the action to be taken and name of the file, then wait confirmation. If the response is affirmative, perform the action; otherwise, do not perform the action. You cannot use this function modifier with the t function.

+   X Use the exclude-file argument as a file containing a list of relative path names for files (or directories) to be excluded from tarfile when using the functions c, x, or t. Be careful of trailing white spaces. You can use multiple x arguments with one exclude-file