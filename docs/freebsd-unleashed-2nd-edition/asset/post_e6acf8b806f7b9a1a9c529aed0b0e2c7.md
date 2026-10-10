
dr-xr-xr-x 2 root wheel 512 May 15 18:30 etc
drwxr-xr-x 3 root wheel 512 May 13 15:26 pub
226 Transfer complete.
ftp> cd pub/FreeBSD/tools
ftp> get gunzip.exe
local: gunzip.exe remote: gunzip.exe
227 Entering Passive Mode (62,243,72,50,89,241)
150 Opening BINARY mode data connection for 'gunzip.exe' (37178 bytes).
100% |*****************************************************************| 37178 00:00 ETA
226 Transfer complete.
37178 bytes received in 9.55 seconds (3.80 KB/s)
ftp> bye
221 Goodbye!
bash$

If you would rather work with a graphical FTP client in X-Windows, several graphical FTP client ports are available in the ftp directory.

## E-mail Applications

E-mail was one of the first applications of the Internet, and it is still the most popular use of the Internet. There is no shortage of e-mail clients available for FreeBSD. Clients are available for text mode shell use, and also graphical clients are available for X-Windows. This section will look at some of the more popular e-mail clients available for both the shell and for X-Windows.

> **TIP**
>
> In addition to having an Internet connection configured and working properly, you will also need to have a mail transfer agent such as Sendmail configured and working properly before you can use some of these e-mail clients. In addition, if you need to retrieve your mail from a POP3 or IMAP server at your ISP, you will also need to have Fetchmail configured and working properly. Not all the clients listed here will require this because some can transfer mail on their own. It is better to use the mail transfer agent / Fetchmail setup, though. This allows much greater flexibility in dealing with e-mail because it uses FreeBSD's native mail-handling system. This will allow the shell to notify you when you have new e-mail, as well as allow mail-checking utilities for X-Windows, such as xbiiff, to notify you of new mail. These features will not work if you use the mail client's built-in mail-handling functions. See Chapter 24, “Configuring E-mail Services,” for details on how to set up and configure FreeBSD to send and receive e-mail.

### Pine

Pine is a text-based e-mail and news client that was designed with the nontechnical user in mind. It is menu driven and is designed to be intuitive and easy to use for the average computer user. Pine is available in the FreeBSD ports collection under the mail directory. Figure 6.12 shows the main menu of Pine.

![](img/48eec858cce7dfb89da36a4d40b7daf3_157_0.png)

**FIGURE 6.12** Pine is menu driven and can be navigated with the arrow keys or by pressing the letter in front of the menu entry.

Pine is very popular with end users because of its ease of use. Because it is text based, it also allows e-mail to be checked remotely over a dumb terminal.

Unfortunately, Pine has a reputation of being poorly programmed and having a lot of security problems. Although all the known problems have currently been fixed, many security experts believe that there are many more security holes in Pine that have not yet been discovered. Some even place the likely number of undiscovered holes in the thousands. You will also be warned of these potential security issues with Pine when you install the port.

If you do decide to make Pine available to your users, you should make sure your users are aware of the potential security hazards involved in using Pine.

If security is a high-level concern on your system (for example, if you have confidential data on the system that these users have access to), it is probably best to forbid the use of Pine altogether (in other words, don't install Pine, or uninstall it if it is already installed). Your users may have fits, but in some situations, security may be more important than user convenience. Other mail programs are available that your users can use (one popular alternative, Mutt, is discussed in the next section). Although they may not be as easy to use as Pine, these programs are generally much more secure.

> **CAUTION**
>
> Although it is generally a bad idea to open any e-mail while logged in as root, it is even more so with Pine. This is because of the nature of some of the potential holes in Pine that might allow someone to execute arbitrary code on your system as the user running Pine simply by sending a bad e-mail header. It is a much better idea to forward root's mail to a normal user account and then read the e-mail using that account instead. Instructions on e-mail forwarding can be found in Chapter 24.

### Mutt

Mutt is another text-based e-mail client for FreeBSD and other Unix-like operating systems. It is available in the FreeBSD ports collection under the mail directory. Figure 6.13 shows the main screen of Mutt.

![](img/48eec858cce7dfb89da36a4d40b7daf3_158_0.png)

**FIGURE 6.13** Although it does not have the simple menu-driven interface of Pine, Mutt is much more secure than Pine and is also more configurable.

Mutt got its name because it is known as “the mongrel of mail clients.” This is because it is a relatively new mail client that attempts to combine the best features of Elm (a very old e-mail client that is not widely used anymore) and Pine (which was designed to be much easier to use than Elm). Mutt has many users who would agree that the client successfully fulfills these goals.

Mutt is a very complex program with a rich set of features. Its use and configuration is beyond the scope of this book. The Mutt Web site, located at www.mutt.org, has very good online documentation and reference manuals that explain the use and configuration of this powerful program.

### uuencode and uudecode

A brief word on uuencode and uudecode is in order here. uuencode is basically a method of sending binary files as plain-text so that they can be sent through e-mail. Often, the e-mail client will handle encoding and decoding of the attachments automatically. However, this is not always the case. Sometimes, you may receive an e-mail that has an attachment, and the attachment may appear as several hundred lines of what appears to be garbage text. It will look something like the following:

```text
begin 644 gunzip.exe
M35H2`4D``````````.I6__/6H`````,.4(`````SQ.8`)BX&"<`F_59(`/M&
M``_XN&\`#`E`X9`+[F0(`F0_`I)X/$#,N050L~"PSN"0`B7`",1OR,70ZX1`?=
M#B;_`\7X#A3HQZ@%*`[HH?`K`1`(AD,1>_/&.I-MW<,`,"#>X(<GX@8S@)0]W
MBP<<F"*<=--2+Y5W+D/’V4”\UKD/UBSV\0^!%HD/ E//@1=<6E/ ?@N”C>0J\X M$B8C^ \H}7#MGONEY/ @, $*+>ML”N^X(N , N^!#@@0QZ~ \XS/ =_^ \XS/CN M”1 #’ , [X#E/ U’E=60T/ ZSL\’ 107C4BZ\%L-’P; /FE\@0P48\ ,,@\@B”C/ B8
```

These are what the first several lines of a uencoded file may look like. The *begin* line contains the name of the file that this file will be saved to when udecoded.

To decode the file, save the attachment (and/or e-mail message that contains the garbage text) to a file in the directory where you want to decode it. For example, suppose you save the file as program.txt. You can now use the following command to decode the file:

```
uudecode program.txt
```

This will decode the file and write the contents to whatever filename is given in the encoding. In the previous example, this would write an output file called gunzip.exe. If you need to encode a file, you can do so with a command like the following (assume that the file you want to encode is called gunzip.exe):

```
uuencode gunzip.exe gunzip.exe > gunzip.txt
```

The three arguments in the previous command are the name of the file you want to encode (in this case gunzip.exe), the name of the output file that should be produced when the file is decoded (usually this will be the same as the input file, as in this example), and a redirect of the output to a file called gunzip.txt, which will contain the encoded file. The > character tells the command to redirect the output to whatever is on the right side of it. If we do not do this, the output will be sent to the screen instead. This allows the output to be piped directly into a mail program, for example, if you wish to send the encoded file to someone.

See Chapter 7 for more information on input/output redirection and pipes.

## Working with Java Applications

Until recently, the latest Java runtime engine (JRE) available for FreeBSD was version 1.1.8. Of course, this version is very outdated and lacks many features of the newer runtime engines. Fortunately, the FreeBSD project was recently given Sun’s blessing to develop a native port of a more recent version of the Java runtime engine. At this time, the most recent stable JRE for FreeBSD is 1.3, although 1.4 may be available by the time this book is printed.

> **NOTE**
>
> The Java compiler is actually written in Java. Therefore, once the Java Runtime Environment has been ported to a platform, the Java compiler will also run on that platform. Because this is the case with FreeBSD, you can also develop Java applications on FreeBSD and compile them on FreeBSD with the Java compiler.
