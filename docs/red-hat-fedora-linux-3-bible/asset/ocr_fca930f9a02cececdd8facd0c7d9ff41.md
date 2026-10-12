By default, the ftp user is given ownership of uploaded files from anonymous users. If you want to indicate that anonymous uploads be owned by a different user (of your choice), you can use the `chown_uploads` and `chown_username` options. For example, if you have a user account named mynewuser, you can set these options as follows:

```
chown_uploads=YES
chown_username=mynewuser
```

Of course, you can create and use any user name you want. However, for security reasons you should not use the root login or any other administrative login for this purpose.

# ### Adding message files

Although vsFTpd doesn't support the arrangement of README and welcome files that FTP servers such as WU-FTP support, you can add .message files to any accessible directory on your vsFTpd server. Then, if you use the `dir_message_enable` option as follows, the text from the .message file will be displayed when the user enters the directory:

```
dir_message_enable=YES
```

You will probably at least want to add a .message file to the root directory of the FTP server for anonymous users. By default, that location is `/var/ftp/ .message`. If you want to use files other than .message files, you can set the `message_file` option. For example, to have text from the .my_message file displayed when you enter a directory, you can add the following line:

```
message_file=.my_message
```

You can also set a one-line message to appear before the login prompt. You can do this by entering the following line, replacing the text with anything you want to say:

```
ftpd_banner=Welcome to my FTP service.
```

# ### Logging vsFTpd activities

Logging is enabled in vsFTpd by default, and the activities of your vsFTpd site are written to the `/var/log/xferlog` file. The following options enable logging and change the log file to `/var/log/vsftpd.log`:

```
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log
```

You can turn off logging if you like by changing YES to NO. (Note, however, that logging enables you to watch for potential break-ins, so turning it off is not recommended.) Or you can change the location of the log file by changing the value of the `xferlog_file` option.