```
```
ftop hash
Hash mark printing on (1024 bytes/hash mark).
ftop prompt
Interactive mode off.
ftop bin
200 Type set to I.
```
```

In this example, you have told ftp to print a hash (#) character for every 1024 bytes that are transferred, turn off prompting, and set the transfer type to binary (which should be on by default). The hash character display provides a visual indicator of the progress of your downloads and uploads. Turning off prompting will allow you to send and retrieve multiple files without the need to confirm each transfer. Setting the transfer type to binary will ensure that binary files are transferred in the proper format instead of text, which means that executable files and pictures will transfer correctly.

Next, you ask the server to show a listing of what directories and files are available on the server:

```
```
ftop 1s
200 PORT command successful.
150 Opening ASCII mode data connection for directory listing.
total 32
d--x---x---x   2 root     root       4096 Aug 31  07:15 bind--x---x---x   2 root     root       4096 Aug 31  07:15 etcd--x---x---x   2 root     root       4096 Aug 31  04:44 lib
d--x---x---x   2 root      50       4096 Sep  3  07:34 pub
226 Transfer complete.
```
```

If directory permissions in the FTP repository are set correctly, the pub directory should be the only directory that shows any files under it. To verify this, change directories to etc and list the contents:

```
```
ftop cd etc
250 CWD command successful.
ftop 1s
200 PORT command successful.
150 Opening ASCII mode data connection for directory listing.
total 0
226 Transfer complete.
```
```

By setting the permissions to execute only on the directories bin, lib, and etc, a system administrator can restrict users from seeing any files in that directory. Good security dictates that remote users be denied information about a system, as any information could aid in hacking attempts.

Now that you see the server is relatively secure, change directories to pub and list the contents of that directory: