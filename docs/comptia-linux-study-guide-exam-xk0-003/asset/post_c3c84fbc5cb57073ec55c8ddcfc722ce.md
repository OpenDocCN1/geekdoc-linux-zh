
8. A. The vncserver script starts the VNC server as an ordinary user, enabling subsequent access to the Linux computer from remote systems. The vncviewer program is the VNC client; the user might use this program on a remote Linux system to access the server that's launched by vncserver. The Xvnc program is the actual VNC server binary, but it must be launched with various options—that's what the vncserver script does. The vncpasswd utility sets a VNC password; the command specifies that VNC has already been configured, so this step isn't necessary at this point.

9. D. FTP server programs vary in design; some are intended to be run from a local or SysV startup script, others are intended to be run from super servers, and others can be launched in either way. The needs of the site must also be considered; for instance, a lightly used FTP server might best be launched from a super server, whereas an FTP server that's in constant use might better be launched from a startup script. Thus, option D is correct.

10. D. The UserDir directive sets the subdirectory name that will be served as personal Web pages. The ServerDir directive is fictitious. ServerRoot sets the base directory where Apache looks for various files; many other options are specified relative to this one. The DocumentRoot directive sets the location of the server's main home page, rather than individual users' personal home pages.

11. A. The Squid program is a caching proxy server, meaning that it provides the features described in the question. PHP is a tool for running Web-centric scripts. lynx is a text-based Web browser. CGI is the Common Gateway Interface, a tool for running scripts from a Web server.

12. C. Tomcat refers to a package that enables an Apache server to run Java servlets, as used in option C. Tomcat has nothing to do with remote GUI configuration, the cat utility, or SSL encryption.

13. B. The wget command retrieves a file from a Web (HTTP) server. Used with the -r option, wget retrieves an entire Web site, so option B is correct. Although curl can also be used to retrieve documents from Web sites, option A's syntax is incorrect, and curl isn't a good tool for retrieving an entire site recursively. Apache is a Web server, not a client, so option C is incorrect. Option D will launch the text-based lynx Web browser, enabling you to view the current site; but this action won't save the site for subsequent editing.

14. C. The ftp command to retrieve a file is get. (receive will also work, and multifile variants, such as mget, are also available.) The cp command is a Linux Bash command to copy a file, but it doesn't work in ftp. The download command is fictitious in this context. The scp command is a tool that's part of the Secure Shell (SSH) package.

15. D. The lcd command in ftp changes the local current directory; it does as the question specifies, so option D is correct. Option A sounds promising if you're familiar with Bash options; however, the change implemented in this way does not affect the already launched ftp instance, so option A is incorrect. The cd command in option B changes the current directory on the server, not on the client, as the question specifies. The change-to command in option C is fictitious.

16. D. The `curl` command retrieves a file using HTTP, FTP, or various other protocols and sends the file to standard output. Thus, option D will do as requested. (If the file is long, you might want to pipe it through `less`.) The `ftp` program can't connect to an HTTP (Web) server, and even if the computer were running an FTP server, option A wouldn't accomplish the specified goal. You could type `telnet www.example.org 80` to connect to the Web server and then type additional HTTP commands to retrieve the file; however, as stated, option B won't work. Although you can use `wget` to retrieve the file, `wget` won't display it directly on your screen, so option C is incorrect.

17. A. FTP supports both ASCII and binary modes. Transferring binary data (such as a JPEG graphics file) in ASCII mode will almost certainly corrupt it, as option A suggests. The difference between active and passive modes, referred to in option B, won't corrupt data. FTP is perfectly suitable as a tool for transferring graphics data, contrary to option C. Although encryption could result in the specified problem, as option D suggests, this seems implausible for files on a public FTP site. Furthermore, to decrypt files, you'd probably need the sender's `public` key, not a `private` key, as option D suggests.

18. B. The symptoms described can be a result of firewall settings blocking the current FTP transfer mode (active vs. passive). The `passive` command in the `ftp` program toggles between these two modes, so it may correct the problem. This isn't guaranteed, though. The `ascii` command of option A switches to ASCII mode, which alters text files for the client or server default; it's unlikely to help. The `mute` and `mget` commands of options C and D attempt to upload and download, respectively, files matching the `fix*` wildcard. This action is unlikely to be helpful.

19. A. The `mysqladmin` utility enables you to administer a MySQL server, including setting its administrative password. Option A presents the correct syntax to do this. Option B's `mysql` `passwd` utility is fictitious. Option C's `passwd` command will change the Linux login password for the `mysql` user. This action has no effect on the MySQL server's administrative password, which is independent of the Linux account database. Likewise, option D will change the Samba password for the `mysql` user, which will have no effect on MySQL.

20. B. The `--host` (or `-h`) option to `mysql` tells it to connect to a remote server rather than the local one. The remaining options are all fictitious.

## Chapter 12

### Securing Linux

![](img/9903a4d3f7abd8dcbef1035fa04a3406_552_0.png)

THE FOLLOWING COMPTIA OBJECTIVES ARE COVERED IN THIS CHAPTER:

- ✓ 5.3 Explain the basics of SELinux (Running modes [Enabled, Disabled, Permissive]).
- ✓ 5.5 Explain the appropriate use of the following security related utilities (*nmap*, *Wireshark*, *NESSUS*, *Snort*, *Tripwire*).
- ✓ 5.6 Use checksum and file verification utilities (*md5sum*, *sha1sum*, *gpg*).
- ✓ 5.8 Explain the methods of authentication (PAM, LDAP, NIS, RADIUS, Two-factor authentication).

![](img/9903a4d3f7abd8dcbef1035fa04a3406_553_0.png)

Sadly, security is a very important topic. Sloppy configuration, program bugs, user error, and other problems can result in a system compromise. Such a compromise can result in confidential data falling into the wrong hands, data loss, abuse of your resources (such as network connectivity) to malicious or even criminal ends, and so on. For these reasons, you should pay careful attention to security, configuring your system in as secure a way as possible.

> Security isn't an all-or-nothing matter. No computer can be absolutely 100 percent secure—if nothing else, somebody might physically break in and steal the system. Rather, security comes in degrees, from very poor security up to very good security. You must decide where you want your system to fall on this continuum, trading off the benefits of improved security against the effort it takes to maintain that security, for both you and the system's users.

Many security topics are described in other chapters of this book. This chapter begins with a broad overview of security issues—where problems can exist. It then gets into the nitty-gritty details of how Linux authenticates users, since these details enable making changes with security implications. Using file encryption for transfers over the Internet is up next so that you can verify your correspondents' identities and encrypt private files and messages transferred via e-mail or other insecure media. This chapter then covers a set of high-security Linux tools that can be deployed in high-security environments. Next up is a description of tools and techniques you can use to review your system's overall level of security. Finally, this chapter looks at ways you can detect whether your system has been compromised.

### Sources of Security Vulnerability

Threats to system security are many and varied, and they're changing all the time. That is, bugs or other problems in specific programs are likely to be fixed soon after they're found, but new bugs or problems may be discovered the next day. Thus, a program-by-program listing of security problems is impractical in a book, although Web sites such as the Computer Emergency Response Team (CERT; http://www.cert.org) cite do track known vulnerabilities. Instead of attempting to list all known problems, I describe security vulnerabilities in broad categories. These include physical access, stolen passwords, bugs in local (nonserver) programs, bugs in server programs, denial-of-service attacks, encryption issues, and humans.
