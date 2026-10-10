## TABLE 16.1 continued

| Command | Meaning |
| :--- | :--- |
| print | Print a local file. Only valid if the share is a printer share. |
| help | List available commands. |
| help *cmd* | Get help about the command *cmd*. |
| quit | Log off from the SMB server. |

As you see, **smbclient** is very similar to the command-line FTP client. For details about other commands, type **help** at the **smbclient** prompt. For details about invoking **smbclient**, see the man page **smbclient(1).**

# # Backing Up SMB Shares

**smbclient** has a very useful command called **tar**. This command creates a *tar* file of the remote directory. You can use **smbclient** to back up or restore SMB shares from a Linux machine.

To back up an SMB share, use the **c** option:

```
```
smb:\> tar c backup.tar
```

5166 ( 280.3 kb/s) \SUSLOG.DAT
28553 ( 386.0 kb/s) \BOOTLOG.TXT
20553 ( 378.7 kb/s) \BOOTLOG.PR
93812 ( 424.1 kb/s) \COMMAND.COM
...
```

**smbclient** backs up the entire share in **backup.tar**. The **x** option is the opposite; it causes **smbclient** to extract files from local *tar* file and place them on the SMB share.

You can invoke **smbclient** with the **-T** option to automatically invoke the *tar* command. This lets you write shell scripts to back up SMB shares from Linux. See **smbclient(1)** for details.

# # Mounting SMB Shares

Not only can Linux act as an SMB server, it can also mount SMB file systems. You can put SMB shares in your Linux directory tree, just as you can put NFS volumes in the tree.

To mount an SMB share, use the **smbmount** command:

```
```
# smbmount //server/share password -c 'mount mountp'
```
```