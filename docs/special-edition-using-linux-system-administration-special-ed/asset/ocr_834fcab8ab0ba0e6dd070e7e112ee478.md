Table 14.3 — smbclient Commands

| Command | Description |
|---|---|
| `cd <directory>` | Change directory on the remote system. |
| `del <file>` | Delete a file on the remote system. |
| `dir` | Display the contents of the current directory on the remote system. |
| `exit` | Quit smbclient. |
| `get <file>` | Copy a file from the current directory on the remote system to the current directory on the local system. |
| `lcd <directory>` | Change directory on the local system. |
| `ls` | Display the contents of the current directory on the remote system. |
| `md <directory>` | Create a directory on the remote system. |
| `mkdir <directory>` | Create a directory on the remote system. |
| `mget <file list>` | Copy multiple files from the current directory on the remote system to the current directory on the local system. |
| `mput <file list>` | Copy multiple files from the current directory on the local system to the current directory on the remote system. |
| `put <file>` | Copy a file from the current directory on the local system to the current directory on the remote system. |
| `quit` | Quit smbclient. |
| `rd <directory>` | Remove a directory on the remote system. |
| `rmdir <directory>` | Remove a directory on the remote system. |

An alternative approach to accessing files on an SMB-shared remote directory is using the smbmount command. With smbmount, you can mount a remote SMB directory to a mount point on your local system.

The syntax of the smbmount command is simple:

```
```text
# smbmount '<resource name>' -c 'mount <mount point>' \\
-u <local user> -g <local group>
```
```

For instance, if you want to mount the SMB resource \\somesserver\somedir in your Linux system at the directory /sambamount (which must exist as an empty directory), you could use a command of the following form:

```
```text
# smbmount \\somesserver\somedir -c 'mount /sambamount' \\
-u <local user> -f <local group>
```
```

This command tells smbmount to mount the specified directory using the specified mount command. In Linux, however, all files and directories must have an associated local user and local group. This is the role of the -u and -g flags. They specify the local user and group to be