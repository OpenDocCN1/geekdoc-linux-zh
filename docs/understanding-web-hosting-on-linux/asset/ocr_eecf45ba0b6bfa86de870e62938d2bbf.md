# Linux and the Internet • 165

Although modern browsers can communicate with FTP, earlier computer users became familiar with the FTP client called, amazingly enough, ftp. You can get a taste of FTP by issuing the command ftp from a command line. At the ftp prompt, type a question mark and press Enter. You'll be presented with a list of commands included in the File Transfer Protocol. If you don't want to do that yourself, you can always look at Figure 11.3, where we've done the heavy lifting for you.

```
ftp ?
Commands may be abbreviated.

! cr mdir proxy send
$ delete mget sendport site
account debug mkdir put size
append dir mls status
ascii bell mode quit struct
bell disconnect modtime system
binary form mput quote sunique
binary
bye newer regret tenex
case hash rstatus trace
ccc help nlist type
cd nstrans user
cdump image open umask
clear ls reset restart
clear private verbose
close passive prompt rmdir
cprotect de-let rename
tftp> mdelet protect runique
tftp> safe ?
```

# Odds, Enns, and Email

One of the widely used Internet facilities is email, and it may have been that first drew you to the Internet. When you first became "connected," your ISP or network administrator should have provided the names of your SMTP and POP servers, which you dutifully filled into the appropriate spaces in your client's configuration screen.

Once your email was started, you probably didnt give any more thought to the curious terms SMTP and POP. Surprisingly, the last P in each of these terms stands for "protocols." The protocols primarily responsible for delivering your messages and receiving them are the Simple Mail Transfer Protocol (SMTP), the Post Office Protocol (POP), and, to a growing extent, the Internet Message Access Protocol (IMAP).

Let's begin this discussion with SMTP, which transmits your message to its destination. SMTP is the protocol used between servers to exchange mail, not the program itself, so if you are running an SMTP daemon, you'll need to obtain an SMTP server program. The standard on Red Linux is the venerable and very powerful sendmail, notorious for its incredibly tricky configuration and infamous security for older versions. Simpler and more secure programs include QMail and Postfix, which is readily available in RPM format for a Red Hat system. Regardless of which server you choose, they all operate in the same fashion. Upon startup, they check their configuration, decide where they are running and from whom they will accept mail, then patiently await a connection on TCP/IP port 25.