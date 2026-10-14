If you create a mail alias of wombats (See Section 11.6.1) for these five members of a team called Wombats, you can send the file to that alias, as shown:

```
% mailx -s "games" wombats < schedule
```

# 12.1.4 Using write to Copy Files Between Local and Remote Hosts

The write command copies files to a local or remote host, although write is most often used to write messages to other users as tasks described in Section 11.8. After you type write, enter the user name of the recipient, a left-angle bracket redirection symbol (<), and the name of the file you want to send. For example, to send a file named letter in your current directory to user maria, enter the following command at the host prompt:

```
% write maria < letter
```

# 12.2 Copying Directories of Files Between a Local and a Remote Host

The -r option of the rcp command enables you to copy entire directories of files recursively (that is, including files and directories within any subdirectories) between a local and a remote host.

To copy a directory recursively from your local host to a remote host, use the following syntax:

```
rcp -r localdirectory hostname:directory
```

The localdirectory variable identifies the local directory that you want to copy recursively. The hostname:directory variable identifies the remote host (hostname) followed by a colon (:) and the name of the remote directory (directory) to which the local directory is copied.

The following example uses rcp -r to copy recursively the directory /usr/reports from the local host to the directory /user/status/newdata on remote host moon:

```
% rcp -r /usr/reports moon:/user/status/newdata
```

You can also copy recursively a directory on your local host to a user at a remote host. The following example shows how to copy the directory /usr/reports on the local host to the directory /user/status/newdata in the home directory of user smith on the remote host moon. This example also uses the -p option, as explained in Section 12.1.1, to preserve the original creation date and access permission mode of the directory and files that are copied in the new directory:

```
% rcp -p -r /usr/reports smith@moon:/user/status/newdata
```