# **22. scp: Securely copy files between local and remote machines.**

`scp` stands for Secure Copy Protocol, and it is a command-line tool used in Linux and Unix-like operating systems to securely copy files and directories between hosts. It uses SSH (Secure Shell) for data transfer and provides encryption and authentication.

# **Examples:**

+   1. **Copy a file from local to remote host:**

```
```
scp file.txt username@remote_server_ip/path/to/destination/
```
```

Replace `file.txt` with the name of the file you want to copy, `username` with the username on the remote server, `remote_server_ip` with the IP address of the remote server, and `/path/to/destination/` with the destination path on the remote server.

+   2. **Copy a file from remote to local host:**

```
```
scp username@remote_server_ip/path/to/file.txt /local/path/
```
```

This command copies the `file.txt` from the remote server to the local machine. Adjust the paths and username accordingly.