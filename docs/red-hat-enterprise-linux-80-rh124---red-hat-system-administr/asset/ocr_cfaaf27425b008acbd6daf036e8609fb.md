# SYNCHRONIZING FILES BETWEEN SYSTEMS SECURELY

# OBJECTIVES

After completing this section, you should be able to efficiently and securely synchronize the contents of a local file or directory with a copy on a remote server.

# SYNCHRONIZE FILES AND DIRECTORIES with rsync

The rsync command is another way to securely copy files from one system to another. The tool uses an algorithm that minimizes the amount of data copied by synchronizing the portions of files that have changed. It differs from scp if two files or directories are similar between two servers, rsync copies the differences between the file systems on the two servers, scp would need to copy everything.

One of the advantages of rsync is that it can copy files between a local system and a remote system securely and efficiently. The initial synchronization of a directory takes about the same time as copying it, any subsequent synchronization only requires the differences to be copied over the network, speeding updates substantially.

One of the most important options of rsync is the -n option to perform a dry run. A dry run is a simulation of what happens when the command executes. The dry run shows the changes rsync would perform when the command is run without the dry run option. You should perform a dry run before performing any rsync operation to ensure no files get overwritten or deleted.

The two common options when synchronizing files and directories with rsync are the -v and -a options.

The -v or --verbose option provides more detailed output as the synchronization runs. This is useful for troubleshooting and to help see progress.

The -a or --archive option enables "archive mode". This is a quick way to enable recursive copying and turn a large number of useful options to preserve most characteristics of the files. Archive mode is the same as the following options:

Options Enabled with rsync -a (Archive Mode)

| OPTION | DESCRIPTION |
| --- | --- |
| -r, --recursive | synchronize recursively the whole directory tree |
| -l, --links | synchronize symbolic links |
| -p, --perms | preserve permissions |
| -t, --times | preserve time stamps |
| -g, --group | preserve group ownership |
| -o, --owner | preserve the owner of the files |