# Copying Files Using tar

One choice for copying files into another location would be to use the tar command where you would create a tar file that would be piped to tar to be uncompressed in the new location. First, change to the source directory. Then, the entire command resembles

```
# tar cvf - files | (cd <target directory>; tar xpf -)
```

where files are the filenames you want to include; use * to include the entire directory.

Here's how this works. You have already changed to the source directory and executed with the cvf arguments that tell tar to

+   - c—Create an archive.
- v—Verbose; lists the files processed so we can see that it's working.
- f—The filename will be what follows. (In this case, it is -)
- A place to hold our data temporarily.

These commands can be useful for creating file copies for backup purposes:

+   - Stay in the local filesystem (so you don't include remote remotes).
- atime—preserve—Change access times on files, even though you're accessing them now, to preserve the old access information for archival purposes.

The contents of the tar file (held us temporarily) are then piped to the second expression, which would un-tar the files to the target directory. In shell programming (Chapter 22), enclosing an expression in parentheses allows it to operate in a subshell.

First we change to the target directory, and then

+   - x—Extract files from a tar archive.
- Preserve permissions.
- f—The filename will be -, the temporary buffer that holds the tar'ed files.

# Compressing, Encrypting, and Sending tar Streams

The file copy techniques using the tar command in the previous section can also be used to quickly and securely copy a directory (using the ssh command) across a LAN or the Internet. One way to use one of these techniques is to use the following command line to compress the contents of a designated directory, and then decompress compressed and encrypted archive stream into a designated directory on a remote host:

```
$ tar cvzf - data_folder | ssh remote_host ' cd /mybackup_dir; tar xzf -'
```