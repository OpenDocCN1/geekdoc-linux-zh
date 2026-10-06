# # scp

scp copies one or more files to or from a remote computer
scp [[user@]@from-host:]source-file [[user@]@to-host:]destination-file]

The scp (secure copy) utility copies an ordinary or directory file from one computer to another on a network. This utility uses ssh to transfer files and the same authentication mechanism as ssh; therefore, it provides the same security. The scp utility asks you for a password when it is needed for security.

# Arguments

The from-host is the name of the machine you are copying files from, and to-host is the machine you are copying to. When you do not specify a host, scp assumes the local machine. The user on either host defaults to the user on the local machine who is giving the command; specify a different user with user@ The scp utility permits you to copy between two remote machines.

The source-file is the file you are making a copy of, and the destination-file is the resulting copy. You can specify plain or directory files as relative or absolute pathnames. A relative pathname is relative to the specified or implicit user's home directory. When the source-file is a directory, you must use the -r option to copy its contents. When the destination-file is a directory, each of the source files maintains its simple filename.

# Options

+   -p preserve Sets the modification times, access times, and file access permissions of each copy to match those of the source-file. When you do not use -p, scp uses the file-creation mask (umask, page 1366) on the remote system to modify the access permissions.

+   -r recursive When a file in the source-file-list is a directory, this option copies the contents of that directory and any subdirectories into the destination-file.

# Notes

You can copy from or to your local machine or between two remote machines. Make sure that you have read permission for the file you are copying and write permission for the directory you are copying into it.