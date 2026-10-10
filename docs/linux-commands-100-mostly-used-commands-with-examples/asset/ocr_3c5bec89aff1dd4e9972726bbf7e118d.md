# 3. Copy an entire directory from local to remote host:

```
scp -r my_directory username@remote_server_ip:/path/to/destination/
```

The `-r` option is used to copy directories recursively.

# 4. Copy from remote to local with a specific port:

```
scp -P 2222 username@remote_server_ip:/path/to/file.txt /local/path/
```

Here, the `-P` option specifies the port number (2222 in this example).

# 5. Copy with compression:

```
scp -C file.txt username@remote_server_ip:/path/to/destination/
```

The `-C` option enables compression during the transfer.

# 23. find: Search for files in a directory hierarchy.

The `find` command in Linux is a powerful and versatile tool used to search for files and directories in a directory hierarchy based on various criteria.

**Examples:**