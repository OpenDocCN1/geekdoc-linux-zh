some older clients, such as Windows 9x/Me, lack support for the protocols required by the cifs driver. Therefore, if you want to mount shares from such systems, you *must* use smbfs rather than cifs.

# ## Accessing NFS Exports

Like SMB/CIFS, Sun's NFS is a file sharing protocol, but it was designed with the needs of Unix systems in mind. NFS includes Unix features, such as support for owners, groups, and permission strings that aren't well supported by SMB/CIFS. (The Unix CIFS extensions narrow this gap, but NFS tends to handle these features better.) Because Linux conforms closely to the Unix model, NFS is the preferred method for file sharing between Linux systems.

In Linux, client access to NFS exports is tightly integrated into normal Linux file-access utilities. Specifically, you use the *mount* command to mount the NFS exports, and you can then access files stored on the NFS server as if they were ordinary files. To do so, you provide *mount* with a server hostname or IP address and a path to the directory on the server you want to access, rather than a device filename. For instance, you might issue commands like the following:

```
# mount apollo:/home/hschmidt /mnt/al7
# ls -l /mnt/al7
total 152
-rwxr-x--x 1 rdsmith users 152576 Mar 29 13:01 drock.wpd
drwxr-xr-x 1 rdsmith users 512 Apr  2  2000 geology
# cp /mnt/al7/drock.wpd ./
# umount /mnt/al7
```

It's important to note that you aren't required to enter a password when you access NFS exports. An NFS server allows a specified set of clients to access the exported directories in a more-or-less unrestricted manner; the server relies on the client's security policies to prevent abuses.

# ## Using df

If you need information on disk space used on an entire partition, the *df* command does the job. This command summarizes total, used, and available disk space. You can provide options to *df* to vary the data it produces, as summarized in Table 6.9.

**TABLE 6.9**
df Options

| Option | Option Abbreviation | Description |
| :--- | :--- | :--- |
| --human-readable | -h | Normally, df provides output in 1024-byte blocks. This option makes it provide listings in labeled units of kilobytes (k), megabytes (M), or gigabytes (G) instead.