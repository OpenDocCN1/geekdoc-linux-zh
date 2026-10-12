where file* are the filenames you want to include; use * to include the entire current directory.

Here is how the command shown works: You have already changed to the source directory and executed tar with the cvf - arguments that tell tar to:

+   - `c` —Create an archive.
+   - `v` —Verbose; lists the files processed so we can see that it is working.
+   - `f` —The filename of the archive will be what follows. (In this case, it is `-`)
+   - `-` —A buffer, a place to hold our data temporarily.

The following `tar` commands can be useful for creating file copies for backup purposes:

+   1. Stay in the local file system (so that you do not include remote volumes).
+   
+      > `tar tvf -` —List but not tar files.
+      > `tar xvf -` —Do not care about access times on files, even though you are accessing them now, to preserve the old access information for archival purposes.

The contents of the tar file (held for us temporarily in the buffer, which is named `-`) are then piped to the second expression, which extracts the files to the target directory. In shell programming (refer to Chapter 14, “Managing Users”), enclosing an expression in parentheses causes it to operate in a subshell and be executed first.

First we change to the target directory, and then

+   - `x` —Extract files from a tar archive.
+   - `p` —Preserve permissions.
+   - `f` —The filename will be `-`, the temporary buffer that holds the tarred files.

# ### Compressing, Encrypting, and Sending tar Streams

The file copy techniques using the tar command in the previous section can also be used to quickly and securely copy a directory structure across a LAN or the Internet (using the `ssh` command). One way to make use of these techniques is to use the following command line to first compress the contents of a designated directory, and then decompress the compressed and encrypted archive stream into a designated directory on a remote host:

```
```
$ tar cvzf . data_folder ; ssh remote_host '( cd ~/mybackup_dir ; tar xvzf - )'
```
```

The `tar` command is used to create, list, and compress the files in the directory named `data_folder`. The output is piped through the `ssh` (secure shell) command and sent to the remote computer named `remote_host`. On the remote computer, the stream is then extracted and saved in the directory named `/mybackup_dir`. You will be prompted for a password in order to send the stream.