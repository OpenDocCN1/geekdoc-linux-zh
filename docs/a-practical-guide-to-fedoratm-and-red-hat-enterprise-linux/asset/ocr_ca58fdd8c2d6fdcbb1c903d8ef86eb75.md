In the next example, Sam, while working from guava, copies the same file as in the previous example to the directory named **old** in his home directory on **speedy**. For this example to work, Sam must be able to use **ssh** to log on to **speedy** from **plum** without using a password. For more information refer to “Authorized Keys: Automatic Login” on page 700.

```
```bash
[ sam@guava ~]$ scp s1s@plum:memo.txt speedy:old
s1s@plum's password:
```
```

# ## OPTIONS

This section describes some of the options you can use with **scp**.

+   - **-C** (compression) Enables compression (page 710).
+   - **-o _option_** (option) Specifies _option_ in the format used in configuration files (discussed shortly).
+   - **-P _port_** (port) Connects to port _port_ on the remote host. This option is uppercase for **scp** and in lowercase for **ssh**.
+   - **-p** (preserve) Preserves the modification and access times as well as the modes of the original file.
+   - **-q** (quiet) Does not display the progress information as **scp** copies a file.
+   - **-r** (recursive) Recursively copies a directory hierarchy (follows symbolic links).
+   - **-v** (verbose) Displays debugging messages about the connection and transfer. Useful if things are not going as expected.

# ## sftp: A Secure FTP CLIENT

As part of OpenSSH, Fedora/RHEL provides **sftp**, a secure alternative to **ftp** (page 713). Functionally the same as **ftp**, **sftp** maps **ftp** commands to OpenSSH commands. You can replace **ftp** with **sftp** when you are logging in to a server that is running the OpenSSH daemon, **sshd**. When you are connected to a system with **sftp**, enter the command **?** to display a list of commands. For secure communication, use **sftp** or **scp** to perform all file transfers requiring authentication. Refer to the **sftp man** page for more information.

**lftp** Fedora/RHEL also offers **lftp**, which is more sophisticated than **sftp** and supports **sftp**. The **lftp** utility provides a shell-like command syntax that has many features, including support for tab completion and the ability to run jobs in the background. Place the following .lftp**rc** file in your home directory to ensure **lftp** uses OpenSSH to connect to a server.

```
```bash
$ cat ~/.lftp**rc
set default-protocol sftp
```
```

You can also use /etc/lftp.conf to configure lftp; see the lftp man page for more information.