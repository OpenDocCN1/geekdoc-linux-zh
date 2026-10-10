# TABLE 12.6 The *scp* command's commonly used copy options

| Short | Description |
| :---- | :---- |
| -C | Compresses the file data during transfer |
| -p | Preserves file access and modification times as well as file permissions |
| -r | Copies files from the directory's contents, and for any subdirectory within the original directory tree, consecutively copies their contents as well (recursively) |
| -v | Displays verbose information concerning the command's execution |

Performing a secure copy of files from a local system to a remote system is rather simple. You do need the OpenSSH service up and running on the remote system. An example is shown in Listing 12.17.

# Listing 12.17 Using *scp* to copy files securely to a remote system

```
$ scp Project42.txt user1@192.168.0.104:~
user1@192.168.0.104's password:
Project42.txt 100% 29kB 20.5MB/s 00:00
$
```

Notice that to accomplish this task, no *scp* command options are employed. The -v option gives a great deal of information that is not needed in this case.

> WARNING The *scp* utility will overwrite any remote files with the same name as the one being transferred without asking or even displaying a message stating that fact. You need to be careful when copying files using *scp* that you don't tromp on any existing files.

A handy way to use *scp* is to copy files from one remote machine to another remote machine. An example is shown in Listing 12.18.

# Listing 12.18 Using *scp* to copy files securely from/to a remote system

```
$ ip addr show | grep 192 | cut -d" " -f6
192.168.0.101/24
$

$ scp user1@192.168.0.104:Project42.txt user1@192.168.0.103:~
user1@192.168.0.104's password:
user1@192.168.0.103's password:
```