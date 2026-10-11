```
Password: <Email_Address>
230-Please read the file README
230- it was last modified on Tue Jan 25 08:51:37 2000 - 369 days ago
230-Please read the file README.roughcuts
230- it was last modified on Fri Jan 21 17:32:20 2000 - 373 days ago
230 Guest login ok. access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp: cd redhat/current/i386/00
250-Please read the file README
250- it was last modified on Fri Aug 25 12:31:19 2000 - 156 days ago
250 CWD command successful.
ftp> get RPM-GPG-KEY
local: RPM-GPG-KEY remote: RPM-GPG-KEY
200 PORT command successful.
150 Opening BINARY mode data connection for RPM-GPG-KEY (1908 bytes).
226 Transfer complete.
1908 bytes received in 0.0589 secs (32 Kbytes/sec)
ftp> cd RedHat/RPMS
250 CWD command successful.
ftp: mget wget* lynx*
ftp> wget -1.5.3-10.i386.rpm? y
200 PORT command successful.
150 Opening BINARY mode data connection for wget-1.5.3-10.i386.rpm (156532 bytes).
226 Transfer complete.
156532 bytes received in 0.948 secs (1.6e+02 Kbytes/sec)
mgnet lynx-2.8.4-3.i386.rpm? y
200 PORT command successful.
150 Opening BINARY mode data connection for lynx-2.8.4-3.i386.rpm (935337 bytes).
226 Transfer complete.
935337 bytes received in 5.29 secs (1.7e+02 Kbytes/sec)
ftp> quit
221-You have transferred 1250309 bytes in 4 files.
221-Total traffic for this session was 1253244 bytes in 7 transfers.
221-Thank you for using the FTP service on pub.nyc.redhat.com.
221 Goodbye.
```

3. Import the Red Hat public key file into GnuPG by using the following command (If this is the first time running gpg, you will need to execute it twice):

```
[root@redhat /root]# gpg --import RPM-GPG-KEY
gpg: /root/.gnupg: directory created
gpg: /root/.gnupg/options: new options file created
```