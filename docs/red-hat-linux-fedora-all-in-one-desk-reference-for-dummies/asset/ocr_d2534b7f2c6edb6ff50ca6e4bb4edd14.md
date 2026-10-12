The best way to learn the command-line FTP client is to try it out. The command is called ftp, and you can try the ftp commands from your Red Hat Linux system. You don't even need any Internet connection because you can use the ftp command to connect to your own system — I show you how.

In the following sample FTP session, I use the command-line FTP client to log in using my user name (naba) and browse the directories on my system. When you try a similar operation, replace the name with your user name and provide your password. Here's the listing showing the commands (my comments appear in italics):

```
```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTPd 1.2.0)
Name (localhost:naba): (I press Enter.)
331 Please specify the password.
Password: (I type my password.)
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> help (I type help to see a list of FTP commands.)
Commands may be abbreviated. Commands are:
! debug mdir sendport site
$ dir mget put size
account disconnect mkdir pwd status
append exit mls quit struct
ascii form mode quote system
bell get modtime recv sunique
binary glob mput rget tenex
bye hash newer rstatus tick
case help nmap rhelp trace
cd idle nlist rename type
cdup image ntrans reset user
chmod lcd open prompt restart umask
close ls passive rmdir runique verbose
cr macdef mdelete proxy send
delete mdelete proxy send
ftp> help mget (I can get help on a specific command.)
mget get multiple files
ftp> cd /var/ftp (This changes directory to /var/ftp.)
250 Directory successfully changed.
ftp> ls (This command lists the contents of the directory.)
227 Entering Passive Mode (127,0,0,1,248,180)
150 Here comes the directory listing.
drwxr-xr-x 2 0 0 4096 Jun 26 05:10 pub
226 Directory send OK.
ftp> bye (This command ends the session.)
221 Goodbye.
```
```