
The `ssh` command is fast and easy, offering a simple way to jump onto a remote system and use the command line, including screen-oriented programs like `emacs` or the `vi` editor. It’s the functional equivalent of using `VLC` or `RDP` to get a remote GUI session to a Windows machine or Mac; but because Unix is command-line driven, a textual terminal gives you all the functionality of being on the machine locally with none of the need for heavyweight telepresence servers to be installed on the remote machine. I use it quite frequently.

Sure, you could still use `telnet` or its partner program `rlogin`, but both of those have security problems that make them poor choices in this modern era of widescale computer hacking and system break-ins. It’s best to ensure that they’re disabled on the server itself and just learn `ssh`!

## Task 21.2: Third-Party SSH Connections

I’ve already pointed out the security problems with `telnet` and its ilk. There are important considerations, not the least of which is that the information between the client and the server is “in the clear.” That is, if you could somehow interpose a network packet sniffer that could filter out just the `telnet` traffic, you could read the account/password pair and everything that’s displayed on the remote user’s display.

Although a number of possible solutions exist for this problem, Tatu Ylönen at Helsinki University of Technology in Finland came up with the best one: `SSH`. `SSH` is essentially a point-to-point encrypted `telnet` protocol. If your server supports `SSH`, and odds are excellent that it does, you should unquestionably use it. There are no downsides that I’ve found, and the additional security is a definite boon.

On the PC side, the `SSH` client of choice is unquestionably `PuTTY`, which includes `SSH` support and can be found at `http://www.putty.org`. Better yet, it’s free. You can’t go wrong with that price.

For Macintosh users, an `SSH` client is included with Mac OS X, so you need merely open up the Terminal (it’s in Applications -> Utilities) and type `ssh` to get started.

If you’re on a Unix or Linux system, you already have an `SSH` client. Just type `ssh` and

computer account to connect and copy files from their archives. To use these systems, enter `ftp` as the account name and then enter your own email address as the password. (For example, I’d enter `ftp` as the account and then [taylor@intuitive.com](taylor@intuitive.com) as my password.) The most important commands available in `sftp` once you’re connected to a remote server are summarized in [Table 21.1](Table 21.1). The most important one to remember is `quit`, which you use when you’re done.

| Command | Meaning |
|---|---|
| bye | Quit sftp. |
| cd path | Change remote directory to path. |
| chgrp grp path | Change group of file path to grp. |
| chmod mode path | Change permissions of file path to mode. |
| chown own path | Change owner of file path to own. |
| df [-hi] [path] | Display statistics for current directory or file system containing path. |
| exit | Quit sftp. |
| get [-Ppr] remote [local] | Download file. |
| reget remote [local] | Resume file download. |
| help | Display this help text. |
| lcd path | Change local directory to path. |
| lls [ls-options [path]] | Display local directory listing. |
| lmkdir path | Create local directory. |
| ln [-s] oldpath newpath | Link remote file (-s for symlink). |
| lpwd | Print local working directory. |
| ls [-1afhlnrSt] [path] | Display remote directory listing. |
| lumask umask | Set local umask to umask. |
| mkdir path | Create remote directory. |
| progress | Toggle display of progress meter. |
| put [-Ppr] local [remote] | Upload file. |
| pwd | Display remote working directory. |
| quit | Quit sftp. |
| rename oldpath newpath | Rename remote file. |
| rm path | Delete remote file. |
| rmdir path | Remove remote directory. |
| symlink oldpath newpath | Symlink remote file. |
| version | Show SFTP version. |
| !command | Execute command in local shell. |
| ! | Escape to local shell. |
| ? | Synonym for help. |

## TABLE 21.1 Valuable sftp Commands

1. I want to pick up a file from intuitive that I saw earlier, when I used `ssh` to look at the remote system. To start `sftp`, I specify the account and host at the command line:

Click here to view code image

```
```
