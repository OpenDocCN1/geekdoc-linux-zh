
# RUNNING the ftp and sftp Clients

the server in passive (PASV) mode, which asks for a username and password. Because he is logged in on his local system as sam, ftp responds to Sam login dog as sam. To log in as sam, he could just press RETURN. Because username on dog is on sls, he responds to prompt with the Name (dog): prompt. After Sam responds to the Password: prompt with his normal system password, the vsftpd server gives him and informs him that it is Using binary mode to transfer files. In ftp binary mode, sam can transfer ASCII and binary files (page 64).

## Connect and log in

```
sam@opt:~$ ftp dog
Connected to dog.bogus.com.
220 (vsFtpd 2.2.2)
Name (dog:sam): sls
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

After logging in, Sam uses the ftp ls to see what is in his remote working directory, which is his home directory on dog. Then he cds to the memos directory and displays the files there.

## ls and cd

```
ftp ls
227 Entering Passive Mode (192,168,0,12,130,201)
150 Here comes the directory listing.
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51 expenses
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:53 memos
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51 tech
226 Directory send OK.
```

## ftp memos

```
ftp ls
227 Entering Passive Mode (192,168,0,12,48,84)
150 Here comes the directory listing.
-rw-r--r-- 1 1001 1001 3430 Jan 25 04:52 memo.0514
-rw-r--r-- 1 1001 1001 6581 Jan 25 04:52 memo.0628
-rw-r--r-- 1 1001 1001 2801 Jan 25 04:52 memo.0905
-rw-r--r-- 1 1001 1001 7351 Jan 25 04:53 memo.0921
-rw-r--r-- 1 1001 1001 14703 Jan 25 04:53 memo.1102
226 Directory send OK.
ftp>
```

Next Sam uses the ftp get to copy memo.1102 from the server to the local system. His use of binary mode ensures he will get a good copy of the file regardless of whether it is binary or ASCII. The server confirms that the file was copied successfully and reports on its size and the time required to copy it. Sam then copies the local file memo.1114 to the remote system. This file is copied into his working directory, memos.

## get and put

```
ftp> get memo.1102
local: memo.1102 remote: memo.1102
227 Entering Passive Mode (192,168,0,12,53,74)
150 Opening BINARY mode connection for memo.1102 (14703 bytes).
226 File sent OK.
14703 bytes received in 0.00 secs (11692.5 kB/s)

ftp> put memo.1114
local: memo.1114 remote: memo.1114
227 Entering Passive Mode (192,168,0,12,182,184)
150 OK to send data.
226 File receive OK.
11503 bytes sent in 0.00 secs (23294.6 kB/s)
ftp>
```

Now Sam decides to copy all the files in the memo directory to a new directory on his local system. He gives an ls command to make sure he copy the right files, but ftp has timed out. Instead of exiting from ftp and giving another ftp command from the shell, he gives an open dog command to connect to the server. After logging in, he uses the ftp cd command to change directories to memos on the server.

## Timeout and open

```
ftp> ls
No control connection for command: Success
Passive mode refused.

ftp> open dog
Connected to dog.bogus.com.
220 (vsFptd 2.2.2)
Name (dog:sam): s1s
..

ftp> cd memos
250 Directory successfully changed.
ftp>
```

## Local cd (lcd)

At this point, Sam realizes he has not created the new directory to hold the files he wants to download. Giving in an ftp mkdir command would create a new directory on the server, but Sam wants a new directory on his local system. He uses an exclamation point (!) followed by mkdir memos.hold to invoke a shell and run mkdir on the local system, creating a directory memos.hold in his working directory. (You can display the name of the working directory on local system with pwd.). Next, because Sam wants to copy files from the server to the memos.hold directory on local system, he has to change his working directory. Giving the command cd memos.hold will not accomplish what Sam wants because the exclamation point will spawn a new shell on the local system, which is not the shell that ftp is running under. For this situation, ftp provides the lcd (local cd) command, which changes the working directory for ftp and reports on the new:

```
ftp > !mkdir memos.hold
ftp > lcd memos.hold
Local directory now /home/sam/memos.hold
ftp >
```

Sam uses the ftp mget (multiple get) command followed by an asterisk (*) to copy all files from the remote memos to local system. If ftp prompts for the first file, Sam realizes he forgot to turn off the prompts, he responds with n and presses CONTROL-C to stop copying files in response to the second prompt. Next Sam gives the prompt command, which toggles prompt (turns off if on and turns on if off). Now when he gives mget * ftp copies the files without prompting. After getting the desired files, Sam gives a quit command to close the connection with the server, exit from ftp, and return to the local shell.

```
ftp> mget *
mget memo.0514? n
mget memo.0628? n
ftp > prompt
Interactive mode off.
ftp > mget *
local: memo.0514 memo.0514
227 Entering Passive Mode (192,168,0,12,216,239)
150 Opening BINARY data connection for memo.0514 (3430 bytes).
226 File OK.
3430 bytes received in 0.00 secs (94.0 k/s)
local: memo.0628 remote: memo.0628
227 Entering Passive Mode (192,168,0,12,134,49)
150 Opening BINARY data connection for memo.0628 (6581 bytes).
226 File OK.
...
150 Opening BINARY data connection for memo.1114 (11903 bytes).
226 File OK.
11903 bytes received in 0.00 secs (1296.4 k/s)
ftp > quit
221 Goodbye.
sam@$-
```

A Linux system running ftp can exchange files with any of the systems that support FTP. Many sites offer archives of free information on an FTP server, although for many it is just an alternative to an easier-to-access Web site (see, for example, ftp://ftp.org/pub/Linux and http://www.ftp.org/pub/Linux). Most browsers can connect to and download files from FTP servers. The ftp utility makes no assumptions about filesystem nomenclature or structure because you use ftp to exchange files with non-UNIX/Linux systems (which may use different naming conventions).

## FTP: TRANSFERRING FILES ACROSS A NETWORK

This section explains how to use the ftp FTP client. Although it describes ftp, many other command-line FTP clients are based on ftp and use the same commands.

## ANONYMOUS FTP

Many systems—most notably those from which you can download free software—allow you to log in as anonymous. Most systems that support anonymous logins accept the name ftp as an easier-to-spell and quicker-to-enter synonym for anonymous. An anonymous user is usually restricted to a portion of a filesystem set files that are to be shared with remote users. When you log in as anonymous user, the server prompts you to enter a password. Although any password may be accepted, by convention you are expected to supply your email address.

Many systems permit anonymous access store files in the public directory. Most browsers, such as Firefox, log in on an anonymous FTP site and transfer a file when you click on filename.

## AUTOMATIC LOGIN

You can store server-specific FTP username and password information so you do not have to enter it each time you visit an FTP site. Each line of ~/.netrc identifies a server. When you connect to an FTP server, ftp reads the ~/.netrc to determine whether you have an automatic login set up for that server. The format of a line in ~/.netrc

```
machine server login username password password
```

where server is the name of the server, username is your username, and password is your password on server. Replace machine with default on the last line of the file to specify a username and password for systems not listed in ~/.netrc. The default line is useful for logging in anonymous servers. A sample ~/.netrc file follows:

```
$ cat ~/.netrc
machine dog login sam password mypassword
default login anonymous password sam@example.com
```

To protect the account information in ~/.netrc, make it readable only by the user home directory it appears in. Refer to the netrc man page for more information.

## BINARY VERSUS ASCII TRANSFER

The vsftp FTP server—can not always—provide two modes to transfer files. Binary mode always copies an exact, byte-for-byte image of a file and never change line endings. Transfer all binary files using binary mode. Unless you need to convert line endings, use binary mode to transfer ASCII files as well.
