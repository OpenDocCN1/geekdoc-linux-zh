```
dr-xr-xr-x 2 root wheel 512 May 15 18:30 etc
dwrxr-xr-x 3 root wheel 512 May 13 15:26 pub
226 Transfer complete.
ftp> cd pub/FreeBSD/tools
ftp> get gunzip.exe
local: gunzip.exe remote: gunzip.exe
227 Entering Passive Mode (62,243,72,50,89,241)
150 Opening BINARY mode data connection for 'gunzip.exe' (37178 bytes).
100% |**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*| 37178 00:00 ETA
226 Transfer complete.
37178 bytes received in 9.55 seconds (3.80 KB/s)
ftp> bye
221 Goodbye!
bash$  
```

If you would rather work with a graphical FTP client in X-Windows, several graphical FTP client ports are available in the ftp directory.

# # E-mail Applications

E-mail was one of the first applications of the Internet, and it is still the most popular use of the Internet. There is no shortage of e-mail clients available for FreeBSD. Clients are available for text mode shell use, and also graphical clients are available for X-Windows. This section will look at some of the more popular e-mail clients available for both the shell and for X-Windows.

**TIP**

In addition to having an Internet connection configured and working properly, you will also need to have a mail transfer agent such as Sendmail configured and working properly before you can use some of these e-mail clients. In addition, if you need to retrieve your mail from a POP3 or IMAP server at your ISP, you will also need to have Fetchmail configured and working properly. Not all the clients listed here will require this because some can transfer mail on their own. It is better to use the mail transfer agent / Fetchmail setup, though. This allows much greater flexibility in dealing with e-mail because it uses FreeBSD's native mail-handling system. This will allow the shell to notify you when you have new e-mail, as well as allow mail-checking utilities for X-Windows, such as xbiiff, to notify you of new mail. These features will not work if you use the mail client's built-in mail-handling functions. See Chapter 24, “Configuring E-mail Services,” for details on how to set up and configure FreeBSD to send and receive e-mail.

# ## Pine

Pine is a text-based e-mail and news client that was designed with the nontechnical user in mind. It is menu driven and is designed to be intuitive and easy to use for the average computer user. Pine is available in the FreeBSD ports collection under the mail directory. Figure 6.12 shows the main menu of Pine.