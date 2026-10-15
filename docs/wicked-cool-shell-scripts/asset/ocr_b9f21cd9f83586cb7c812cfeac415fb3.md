# Hacking the Script

The Apache htpasswd program offers a nice command line interface for appending the new account and encrypted password information to the account database. But only one of the two commonly distributed versions of htpasswd supports batch use for scripts—that is, feeding the script both an account and password from the command line. It’s easy to tell whether your version does: if htpasswd doesn’t complain when you try to use the -b flag, you’ve got the better, more recent version. Chances are you will be good, though.

Be warned that if this script is incorrectly installed, anyone who gains knowledge of the URL can then add themselves to the access file and delete everyone else. That’s not good. One solution is to only allow this script to be run if the user is already signed in as admin (as the commented code in the top of the script mentions). Another way to secure the script is to place it in a directory that itself is password protected.

# #72 Syncing Files with SFTP

Though the ftp program is still available on most systems, it’s being replaced more and more by new file transfer protocols such as rsync and ssh (secure shell). There are a few reasons for this. Since the first edition of this book, FTP has begun to show some weaknesses with scaling and securing data in this new world of “big data,” and more efficient protocols for transferring data have become more mainstream. By default, FTP also transmits data in plaintext, which is generally fine for home or corporate networking on trusted networks, but not if you’re doing an FTP transfer from an open network at, for example, the library or Starbucks, where a lot of people are sharing the same network as you.

All modern servers should support the considerably more secure ssh package supporting end-to-end encryption. The file transfer element of the encrypted transfer is sftp, and while it’s even more primitive than ftp, we can still work with it. Listing 9-9 shows how we can utilize sftp to securely sync our files.

# NOTE

> If you don’t have ssh on your system, complain to your vendor and administrative team. There’s no excuse. If you have access rights, you can also obtain the package at http://www.openssh.com/ and install it yourself.

# The Code

```
#!/bin/bash
# sftpsync--Given a target directory on an sftp server, makes sure that
# all new or modified files are uploaded to the remote system. Uses
# a timestamp file ingeniously called .timestamp to keep track.
```