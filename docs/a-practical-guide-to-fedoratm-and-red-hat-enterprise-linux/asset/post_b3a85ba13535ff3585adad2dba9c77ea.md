
## TUTORIAL SESSION

Following are two ftp sessions wherein Sam transfers files from and to a vsftpd server named plum. When Sam gives the command ftp plum, the local ftp client connects to the server, which asks for a username and password. Because he is logged in on his local system as sam, ftp suggests that Sam log in on plum as sam. To log in as sam, he could just press RETURN. Because his username on plum is sls, however, he types sls in response to the Name (plum:sam): prompt. After Sam responds to the Password: prompt with his normal system password, the vsftpd server greets him and informs him that it is Using binary mode to transfer files. With ftp in binary mode, Sam can transfer ASCII and binary data (page 720).

### Connect and log in

```
$ ftp plum
Connected to plum (192.168.206.181).
220 (vsFTPd 3.0.2)
Name (plum:sam): sls
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
```

After logging in, Sam uses the ftp ls command to see what is in his remote working directory, which is his home directory on plum. Then he cds to the memos directory and displays the files there.

### ls and cd

```
ftp> ls
227 Entering Passive Mode (192,168,206,181,246,88).
150 Here comes the directory listing.
drwxr-xr-x 2 1001 1001 4096 Jun 13 17:17 expenses
drwxr-xr-x 2 1001 1001 4096 Jun 13 17:19 memos
drwxr-xr-x 2 1001 1001 4096 Jun 13 17:17 tech
226 Directory send OK.

ftp> cd memos
250 Directory successfully changed.

ftp> ls
227 Entering Passive Mode (192,168,206,181,254,97).
150 Here comes the directory listing.
-rw-r----- 1 1001 1001 79915 Jun 13 17:19 memo.0514
-rw-r----- 1 1001 1001 74069 Jun 13 17:19 memo.0628
-rw-r----- 1 1001 1001 37489 Jun 13 17:19 memo.0905
-rw-r----- 1 1001 1001 85699 Jun 13 17:18 memo.0921
-rw-r----- 1 1001 1001 55181 Jun 13 17:18 memo.1102
226 Directory send OK.
```

Next Sam uses the ftp get command to copy memo.1102 from the server to the local system. His use of binary mode ensures that he will get a good copy of the file regardless of whether it is binary or ASCII. The server confirms that the file was copied successfully and reports on its size and the time required to copy it. Sam then copies the local file `memo.1114` to the remote system. This file is copied into his remote working directory, `memos`.

### get and put

```
ftp> get memo.1102
local: memo.1102 remote: memo.1102
227 Entering Passive Mode (192,168,206,181,122,35).
150 Opening BINARY mode data connection for memo.1102 (55181 bytes).
226 Transfer complete.
55181 bytes received in 0.000392 secs (140767.86 Kbytes/sec)

ftp> put memo.1114
local: memo.1114 remote: memo.1114
227 Entering Passive Mode (192,168,206,181,71,174).
150 Ok to send data.
226 Transfer complete.
25897 bytes sent in 0.00174 secs (14857.72 Kbytes/sec)
```

Now Sam decides he wants to copy all the files in the `memo` directory on `plum` to a new directory on his local system. He gives an `ls` command to make sure he will copy the right files, but `ftp` has timed out. Instead of exiting from `ftp` and giving another `ftp` command from the shell, he gives `ftp` an `open plum` command to reconnect to the server. After logging in, he uses the `ftp cd` command to change directories to `memos` on the server.

### Timeout and open

```
ftp> ls
No control connection for command: Success
Passive mode refused.
ftp> open plum
Connected to plum (192.168.206.181).
220 (vsFTPd 3.0.2)
Name (plum:sam): sls
...
ftp> cd memos
250 Directory successfully changed.
```

### Local cd (lcd)

At this point, Sam realizes he has not created the new directory to hold the files he wants to download. Giving an `ftp mkdir` command would create a new directory on the server, but Sam wants a new directory on the local system. He uses an exclamation point (!) followed by a `mkdir memos.hold` command to invoke a shell and run `mkdir` on the local system, thereby creating a directory named `memos.hold` in his working directory on the local system. (You can display the name of the working directory on the local system using `lpwd`.) Next, because Sam wants to copy files from the server to the `memos.hold` directory on his local system, he has to change his working directory on the local system. Giving the command `lcd memos.hold` will not accomplish what Sam wants to do because the exclamation point will spawn a new shell on the local system and the `cd` command would be effective only in the new shell, which is not the shell that `ftp` is running under. For this situation, `ftp` provides the `lcd` (local `cd`) command, which changes the working directory for `ftp` and reports on the new local working directory:

```
ftp> !mkdir memos.hold

ftp> lcd memos.hold
Local directory now /home/sam/memos.hold
```

Sam uses the ftp mget (multiple get) command followed by the asterisk (*) wildcard to copy all files from the remote memos directory to the memos.hold directory on the local system. When ftp prompts him for the first file, Sam realizes that he forgot to turn off the prompts, so he responds with n and presses CONTROL-C to stop copying files in response to the second prompt. The server checks whether he wants to continue with his mget command.

Next Sam gives the ftp prompt command, which toggles the prompt action (turns it off if it is on and turns it on if it is off). Now when he gives a mget * command, ftp copies the files without prompting him. After getting the desired files, Sam gives a quit command to close the connection with the server, exit from ftp, and return to the local shell prompt.

### mget and prompt

```
ftp> mget *
  mget memo.0514? n
  mget memo.0628? CONTROL-C
Continue with mget? n

ftp> prompt
Interactive mode off.

ftp> mget *
local: memo.0514  remote: memo.0514
227 Entering Passive Mode (192,168,206,181,216,120).
150 Opening BINARY mode data connection for memo.0514 (79915 bytes).
226 Transfer complete.
79915 bytes received in 0.00188 secs (42485.38 Kbytes/sec)
local: memo.0628  remote: memo.0628
227 Entering Passive Mode (192,168,206,181,24,77).
150 Opening BINARY mode data connection for memo.0628 (74069 bytes).
226 Transfer complete.
74069 bytes received in 0.0114 secs (6518.44 Kbytes/sec)
...
150 Opening BINARY mode data connection for memo.1114 (25897 bytes).
226 Transfer complete.
25897 bytes received in 0.00107 secs (24293.62 Kbytes/sec)
ftp> quit
221 Goodbye.
```

## ANONYMOUS FTP

Many systems—most notably those from which you can download free software—allow you to log in as anonymous. Most systems that support anonymous logins accept the name ftp as an easier-to-spell and quicker-to-enter synonym for anonymous. An anonymous user is usually restricted to a portion of a filesystem set aside to hold files that are to be shared with remote users. When you log in as an anonymous user, the server prompts you to enter a password. Although the system accepts any password, by convention you are expected to supply your email address. Do not use an important address if you are logging into a public site because that address could receive spam based on this login. Many systems that permit anonymous access store interesting files in the pub directory. Most browsers, such as Firefox, log in on an anonymous FTP site and transfer a file when you click on the filename.

## AUTOMATIC LOGIN

.netrc You can store server-specific FTP username and password information so you do not have to enter it each time you visit an FTP site. Each line of ~/.netrc identifies a server. When you connect to an FTP server, ftp reads the ~/.netrc file to determine whether you have an automatic login set up for that server. The format of a line in ~/.netrc is

```
machine server login username password password
```

where server is the name of the server, username is your username, and password is your password on server. Replace machine with default on the last line of the file to specify a username and password for systems not listed in ~/.netrc. The default line is useful for logging in on anonymous servers. A sample ~/.netrc file follows:

```
$ cat ~/.netrc
machine plum login sls password mypassword
default login anonymous password sam@example.com
```

To protect the account information in .netrc, make it readable only by the user whose home directory it appears in. Refer to the netrc man page for more information.

## BINARY VERSUS ASCII TRANSFER MODE

The vsftpd FTP server can but does not always provide two modes to transfer files. Binary mode transfers always copy an exact, byte-for-byte image of a file and never change line endings. Transfer all binary files using binary mode. Unless you need to convert line endings, use binary mode to transfer ASCII files as well. These descriptions do not apply to files created by word processors such as Word or LibreOffice because those programs generate binary files. The vsftpd server can map Linux line endings to Windows line endings as you upload files and Windows line endings to Linux line endings as you download files.

To use ASCII mode on an FTP server that allows it, give an ascii command (page 722) after you log in and set cr to ON (the default; page 723). If the server does not allow you to change line endings as you transfer a file, you can use the unix2dos (page 260) utility before or after you transfer a file in binary mode.

Security To enhance security, by default vsftpd transfers every file in binary mode, even when it appears to be using ASCII mode. On the server side, you can enable real ASCII mode transfers by setting the ascii_upload_enable and ascii_download_enable parameters
