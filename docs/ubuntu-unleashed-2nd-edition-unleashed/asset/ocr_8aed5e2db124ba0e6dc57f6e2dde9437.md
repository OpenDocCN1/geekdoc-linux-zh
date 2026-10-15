```
200 PORT command successful.
150 Opening BINARY mode data connection for tftp-0.17-14.i386.rpm
(15798 bytes).################
226 Transfer complete.
15798 bytes received in 0.974 secs (16 Kbytes/sec)
local: tftp-server-0.17-14.i386.rpm remote: tftp-server-0.17-14.i386.rpm
200 PORT command successful.
150 Opening BINARY mode data connection for tftp-server-0.17-14.i386.rpm (26011 bytes).
"######################"
226 Transfer complete.
26011 bytes received in 2.5 secs (10 Kbytes/sec)
local: wu-ftpd-2.6.1-22.i386.rpm remote: wu-ftpd-2.6.1-22.i386.rpm
200 PORT command successful.
150 Opening BINARY mode data connection for wu-ftpd-2.6.1-22.i386.rpm (219332 bytes).
######################################
######################################
######################################
################
226 Transfer complete.
219332 bytes received in 50.3 secs (4.3 Kbytes/sec)
```

As described before, the mget command transferred all files with the .rpm extension to our local machine. Furthermore, it did not prompt us to confirm each file because we turned off prompting. The ftp client printed a # for each 1024 bytes transferred to our machine. This is helpful when transferring over a slow connection because you get a visual reminder that your connection is still active.

# TIP

After every action, the FTP server will return a status code and brief message showing the result of the command you issued. You can find a listing of all status codes and their corresponding messages in Request For Comment 959; you can access a copy of this listing at http://www.ietf.org/rfc/rfc959.txt.

Now you are finished with this session; you can issue the command quit to end the session. Additionally, the FTP server will inform you of how many bytes your session transfers, how many files, and the total transferred data (in bytes) between your local machine and the server.

```
ftp> quit
221-You have transferred 503818 bytes in 5 files.
```