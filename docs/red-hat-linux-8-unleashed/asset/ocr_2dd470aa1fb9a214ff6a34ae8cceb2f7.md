Using FTP

69

331 Guest login ok, send your complete e-mail address as password.
Password:
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.

```
ftp>
```

Now that a connection has been established and authenticated to the server, you can then set up the FTP session to work the way you'd like by using internal client commands. As mentioned in the previous section, the ftp command has many different built-in commands, which you can view by typing a question mark at the ftp> prompt. These commands can affect the session display, set the type of file transfer, or obtain information about the remote server.

```
ftp hash
Hash mark printing on (1024 bytes/hash mark)
ftp prompt
Interactive mode off.
ftp bin
200 Type set to I.
```

In this example, you have told ftp to print a hash (#) character for every 1024 bytes that are transferred, turn off prompting, and set the transfer type to binary (which should be by default). The hash character provides a visual indicator of the progress of your download. Turning off prompting will allow you to retrieve multiple files without the need to confirm each transfer. Setting the transfer type to binary will ensure that binary files are transferred in the proper format instead of text.

Next, you need to verify that the configuration you've applied to the FTP server has adequately secured it from malicious entry and by hackers (or accidental damage by an uninformed user). Ask the server to show a list of what directories and files are available on the server.

```
ftp ls
200 PORT command successful.
150 Opening ASCII mode data connection for directory listing.
total 32
d--x-x--x 2 root      root        4096 Aug 31 07:15 bin
d--x-x--x 2 root      root        4096 Aug 31 07:15 etc
d--x-x--x 2 root      root        4096 Aug 31 04:44 lib
d--x-x--x 2 root      50        4096 Sep 3 07:34 pub
226 Transfer complete.
```

![](bbox=[0.931, 0.663, 0.996, 0.713])