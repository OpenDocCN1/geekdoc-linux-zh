# Listing 3.6 Downloading the Sendmail RPM File

```
[craig]$ ftp rpmfind.net
Connected to rpmfind.net.
220 rpmfind.net FTP server ready.
User(rpmfind.net:(craig)): anonymous
331 Anonymous login, use your complete e-mail address as password.
Password:
230 Anonymous access granted, restrictions apply.
ftp> cd linux/contrib/libc6/i386
250 CWD command successful.
ftp> bin
200 Type set to I.
ftp> mget sendmail*8.11.0-1*
200 Type set to I.
mget sendmail-8.11.0-1.i386.rpm? y
200 PORT command successful.
150 Opening BINARY connection for sendmail-8.11.0-1.i386.rpm (259698 bytes)
226 Transfer complete.
ftp: 259698 bytes received in 2.63Seconds 98.74Kbytes/sec.
mget sendmail-cf-8.11.0-1.i386.rpm? y
200 PORT command successful.
150 Opening BINARY connection for sendmail-cf-8.11.0-1.i386.rpm
(221066 bytes)
226 Transfer complete.
ftp: 221066 bytes received in 1.76Seconds 125.61Kbytes/sec.
mget sendmail-doc-8.11.0-1.i386.rpm? y
200 PORT command successful.
150 Opening BINARY connection for sendmail-doc-8.11.0-1.i386.rpm
(482213 bytes)
226 Transfer complete.
ftp: 482213 bytes received in 4.56Seconds 105.75Kbytes/sec.
ftp> quit
220 Goodbye.
```

In this example, user input is shown in bold. The example has been edited to fit on a book page, but is essentially what you would see if you performed this download.

In Listing 3.6 we log on to rpmfind.net with FTP. In this particular case, the files we want are in the linux/contrib/libc6/i386 directory. The mget command is used to retrieve all three files relating to Sendmail 8.11. Quick and easy—but only if you know where the files are located and exactly what RPM files you're looking for.