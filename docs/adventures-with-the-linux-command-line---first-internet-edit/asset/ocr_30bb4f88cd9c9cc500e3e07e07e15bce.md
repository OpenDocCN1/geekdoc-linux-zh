Virtual file systems can also treat remote file systems as local directories. In most versions of Midnight Commander, both FTP and FISH (Files transferred over SHell) protocols are supported and, in some versions, SMB/CIFS as well.

As an example, let's look at the software library FTP at Georgia Tech, a popular repository for Linux software. Its name is ftp.glib.gatech.edu. To connect with /pub directory on this site and browse its files, we enter the \ cd command:

```
me@linuxbox ~ $ cd ftp://ftp.glib.gatech.edu/pub
```

Since we don't have permission on this site, we cannot modify any files there, but we can copy files from the remote server to our local file system.

The FISH protocol is simple. It can be used to communicate with any Unix-like system that runs a secure shell (SSH). If we have write permissions on the remote server, we can operate on the remote system's files as if they were local. This is extremely handy for performing remote administration. The cd command for FISH protocol looks like:

```
me@linuxbox ~ $ cd sh://user@remotehost/dir
```

# Finding Files

Midnight Commander has a useful file search feature. When invoked by pressing Alt-?, the following dialog will appear:

| | File | Command | Options | Right |
|---|---|---|---|---|
| | | | | [] |
| | | | | 13:24 |
| /.ac | | | | 13:30 |
| /.com | Start at: | Find File | { Tree } | 13:30 |
| | [X] Enable ignore directories: | | 13:30 |
| /Docu | | | | 13:32 |
| /Pict | | | | 13:32 |
| /bin | File name: | Content: | | 13:32 |
| .bas | [X] Find recursively | [X] Search for content | 02:48 |
| | [X] using shell patterns | [X] Regular expression | 13:24 |
| | [X] Case sensitive | [X] Case sensitive | 13:54 |
| | [ ] All characters | | 13:44 |
| | [ ] whole words | | 13:24 |
| | [ ] Skip hidden | [ ] First hit | 13:54 |
| | < OK > | | [ Cancel ] |

.bas
Hint: Can you do anonymous FTP with mac by typing `ftp://machine.edu`

```
1File 2Menu 3View 4Edit 5Copy 6Name 7Mkdir 8Delete 9Quit 10Help
```

Finding dialog

Midnight Commander 19