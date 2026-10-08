is copied into a file named *dest_file* in the current directory on the local system. If *dest_file* already exists and is writable, the existing file is overwritten. Destination file names are constructed the same way as source files except that file name expansion characters cannot be used.

dest_dir The name of the destination directory. If host name and path name are not specified, the existing file is copied into a directory named *dest_dir* in the current directory on the local system. If *dest_dir* already exists in the specified directory path (or current directory if not specified), a new directory named *dest_dir* is created underneath the existing directory named *dest_dir*. Destination directory names are constructed the same way as source directory tree names except that file name expansion characters cannot be used.

file_or_dir If a combination of files and directories are specified for copying (either explicitly or by file name expansion), only files are copied unless the *-r* option is specified. If the *-r* option is present, all files and directory subtrees whose names match the specified *file_or_dir* name are copied.

-P Preserve (duplicate) modification times and modes (permissions) of source files, ignoring the current setting of the *umask* file creation mode mask. If this option is specified, *rcp* preserves the sticky bit only if the target user is superuser.

If the *-p* option is not specified, *rcp* preserves the mode and owner of *dest_file* if it already exists; otherwise *rcp* uses the mode of the source file modified by the *umask* on the destination host. Modification and access times of the destination file are set to the time when the copy was made.

-R Recursively copy directory subtrees rooted at the source directory name. If any directory subtrees are to be copied, *rcp* recursively copies each subtree rooted at the specified source directory name to directory *dest_dir*. If *source_dir* is being copied to an existing directory of the same name, *rcp* creates a new directory *source_dir* within *dest_dir* and copies the subtree rooted at *source_dir* to *dest_dir/source_dir*. If *dest_dir* does not exist, *rcp* creates it and copies the subtree rooted at *source_dir* to *dest_dir*.

# Constructing File and Directory Names
As indicated above, file and directory names contain one, two, or four component parts:

user_name Login name to be used for accessing directories and files on remote system.

hostname Hostname of remote system where directories and files are located.