# 1264

# sftp

-o ssh_option

Specify an option to be directly passed to ssh(1).

-v

Raise logging level. This option is also passed to ssh(1).

# Operands

hostname | user@hostname

The name of the host sftp connects to and logs in to.

# Interactive Commands

In interactive mode, sftp understands a set of commands similar to those of ftp(1), Commands are case insensitive and you must enclose paths in quotes if they contain spaces.

cd path Change remote directory to path.

lcd path Change local directory to path.

chgrp grp path

Change group of file path to grp grp must be a numeric GID.

chmod mode path Change permissions of file path to mode.

chown own path Change owner of file path to own own must be a numeric UID.

help Display help text.

get [flags] remote-path [local-path]

Retrieve the remote-path, and store it on the local machine. If you do not specify the local path name, the default is the same name it has on the remote machine. If you specify the -P option, sftp also copies the file's full permission and access time.

ls [ls-options [path]] Display local directory listing of either path or current directory if you do not specify path.

lmdir path Create local directory specified by path.

lpwd Print local working directory.

ls [path] Display remote directory listing of either path or current directory if you do not specify path.

lumask umask Set local umask to umask.

mkdir path Create remote directory specified by path.