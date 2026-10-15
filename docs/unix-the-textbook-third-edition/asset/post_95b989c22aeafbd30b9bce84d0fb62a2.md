
## TABLE 11.5 A Summary of Useful ftp Commands

| Command | Meaning |
|---|---|
| ! [cmd] | Runs cmd on the local machine; without the cmd argument, invokes an interactive shell |
| Help [cmd] | Displays a summary of cmd; without the cmd argument, displays a summary of all ftp commands |
| ascii | Puts the ftp channel into ASCII mode; used for transferring ASCII-type files such as text files |
| binary | Puts the ftp channel into binary mode; used for transferring non-ASCII files such as files containing executable codes or pictures |
| cd | Changes directory; similar to the UNIX cd command |
| close | Closes the ftp connection with the remote host, but stays inside ftp |
| dir remotedir localfile | Saves the listing of remotedir into localfile on the local host; useful for long directory listings, as pipes cannot be used with the ftp commands |
| get remotefile [localfile] | Transfer remotefile to localfile in the present working directory on the local machine; if localfile is not specified, remotefile is used as the name of the local file |
| ls [dname] | Shows contents of the designated directory dname; current directory if none specified |
| mget remotefiles | Transfers multiple files from the remote host to the local host |
| mput localfiles | Transfers multiple files from the local host to the remote host |
| open [hostname] | Attempts to open a connection with the remote host; prompts if hostname not specified as parameter |
| put localfile [remotefile] | Transfers localfile to remotefile on the remote host; if remotefile is not specified, use localfile as name of remote file |
| quit | Terminates the ftp session |
| user [login_name] | If unable to log on as a user on the remote host by specifying the user_name as the command argument; prompt appears if user_name is not specified |

we demonstrate the use of the ftp commands cd, get, ls, and pwd. We also demonstrate execution of the ls command on the local host. Finally, we terminate the ftp session with the quit command. This site does not require any password for anonymous ftp. Thus, you hit <Enter> when prompted for a password.

```
% ftp ftp.FreeBSD.org
Trying 149.20.53.23:21 ...
Connected to ftp.geo.FreeBSD.org.
220 This is ftp0.isc.freebsd.org - hosted at ISC.org
Name (ftp.FreeBSD.org:sarwar): anonymous
331 Please specify the password.
Password: <Enter>
230-
230-This is ftp0.isc.FreeBSD.org, graciously hosted by
230-Internet Systems Consortium - ISC.org.
230-
230-FreeBSD files can be found in the /pub/FreeBSD directory.
230-
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd pub/FreeBSD
250-ISO images of FreeBSD releases may be found in the releases/
ISO-IMAGES
250-directory. For independent files and tarballs, see individual
250-releases/${machine}/${machine_arch} directories. For example,
250-releases/amd64/amd64 and releases/powerpc/powerpc64.
250 Directory successfully changed.
ftp> pwd
Remote directory: /pub/FreeBSD
ftp> cd releases/i386
250 Directory successfully changed.
ftp> pwd
Remote directory: /pub/FreeBSD/releases/i386
ftp> ls
229 Entering Extended Passive Mode (|||55844||).
150 Here comes the directory listing.
lrwxr-xr-x  1 ftp  ftp  17 Jan 17  2014 10.0-RELEASE ->
i386/10.0-RELEASE
lrwxr-xr-x  1 ftp  ftp  13 Oct 22 15:43 10.1-RC3 ->
i386/10.1-RC3
drwxrwxr-x 13 ftp  ftp  25 Jun 20  2013 8.4-RELEASE
lrwxr-xr-x  1 ftp  ftp  16 Jan 16  2013 9.1-RELEASE ->
i386/9.1-RELEASE
lrwxr-xr-x  1 ftp  ftp  16 Sep 30  2013 9.2-RELEASE ->
i386/9.2-RELEASE
lrwxr-xr-x  1 ftp  ftp  16 Jul 11 14:21 9.3-RELEASE ->
i386/9.3-RELEASE
drwxrwxr-x  3 ftp  ftp   5 Jul 02 16:26 ISO-IMAGES
-rw-r--r--  1 ftp  ftp  637 Nov 23  2005 README.TXT
drwxrwxr-x  8 ftp  ftp   9 Oct 23 17:21 i386
226 Directory send OK.
ftp> cd 10.1-RC3
250 Directory successfully changed.
ftp> ls
229 Entering Extended Passive Mode (|||64206||).
150 Here comes the directory listing.
-rw-r--r--  1 ftp  ftp    661 Oct 22 01:41 MANIFEST
-rw-r--r--  1 ftp  ftp 62269164 Oct 22 01:41 base.txz
-rw-r--r--  1 ftp  ftp  1428452 Oct 22 01:41 doc.txz
-rw-r--r--  1 ftp  ftp   883080 Oct 22 01:41 games.txz
-rw-r--r--  1 ftp  ftp 77467572 Oct 22 01:41 kernel.txz
-rw-r--r--  1 ftp  ftp 33221748 Oct 22 01:41 ports.txz
-rw-r--r--  1 ftp  ftp 115163384 Oct 22 01:41 src.txz
```
