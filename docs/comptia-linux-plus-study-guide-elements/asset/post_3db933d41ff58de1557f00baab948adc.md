
# Chapter 11 • Configuring Network Servers II

## 508

15. You've launched ftp to transfer some files, but you've just realized that you launched it in the wrong local directory; you want to be in ~/programming. How can you correct this mistake without exiting ftp?

- A. Press Ctrl+Z, type cd ~/programming, and then type fg.
- B. Type cd ~/programming.
- C. Type change-to ~/programming.
- D. Type lcd ~/programming.

16. A Web server holds a text file for which you have a URL: http://www.example.org/text.txt. You want to view this text file without launching a full Web browser. How might you do this?

- A. Type ftp http://www.example.org/text.txt.
- B. Type telnet http://www.example.org/text.txt.
- C. Type wget http://www.example.org/text.txt.
- D. Type curl http://www.example.org/text.txt.

17. You've connected to a public FTP server and retrieved several JPEG graphics files. You can't open these files in any Linux graphics editor, though. What is the most likely explanation?

- A. The FTP transfer occurred in ASCII mode, thus corrupting the binary graphics data.
- B. The FTP transfer occurred in passive mode, thus corrupting the binary graphics data.
- C. FTP is unsuitable for transferring graphics data; you should have used HTTP.
- D. The graphics files were encrypted, so you need a private key to decrypt them.

18. When you attempt to download a file from an FTP site using a computer located on your heavily protected local network, nothing seems to happen. The server responds to pings, but you can't download files. What might you do to overcome this problem?

- A. Type ascii at the ftp> prompt, and try again.
- B. Type passive at the ftp> prompt, and try again.
- C. Type mput fix* at the ftp> prompt, and try again.
- D. Type mget fix* at the ftp> prompt, and try again.

19. You want to set the password on a freshly installed MySQL server. What command would you use to do this?

- A. mysqladmin -u root password newpassword
- B. mysql passwd newpassword
- C. passwd mysql
- D. smbpasswd mysql

20. Which option would you pass to mysql to have it access a remote MySQL server?

- A. --server=name
- B. --host=name
- C. --remote=name
- D. --db=name

### Answers to Review Questions

1. A. NFS uses a “trusted host” policy to let clients police their own users, including access to the NFS server’s files. NFS does not use a password, nor does it use the `.rlogin` file in users’ home directories.

2. C. Option C presents the correct syntax for achieving the specified goal in `/etc/exports`. Options A and D incorrectly place the exported directory name in the option list for each client. Option B uses `[homes]` (a Samba name for users’ home directories) rather than `/homes`. Options B and D incorrectly expand the `ro` and `rw` codes to **readonly** and **readwrite**.

3. C. The `exportfs` program controls the NFS server; it adds or removes directories and clients from the list the server maintains, thus temporarily extending or restricting the list that’s normally maintained in `/etc/exports`. Option C presents the correct syntax for this program to achieve the stated goal. There is no standard **exports** command, so option A is incorrect. Option B’s **showmount** command displays information on the clients that are using the server, but it doesn’t change the export list. The **mount** command mounts a remote export; it doesn’t affect what’s exported, so option D is incorrect.

4. D. The `[homes]` share in Samba is special; it gives access to users’ home directories, with each user being given access to his or her own **home directory**, as option D describes. Option A is incorrect because the point of the `[homes]` share is to enable access to home directories without having to explicitly define a new share for each user. Option B is incorrect because the `[homes]` share gives access to users’ individual **home directories**, not to the Linux `/home` directory, which is typically the directory in which all users’ home directories reside. Option C is incorrect because a correct password is still normally required to access `[homes]` and because this share doesn’t give access to `/tmp` unless options are set strategically. (The default directory for most Samba shares is `/tmp`, but this isn’t true of `[homes]`.)

5. B, C, D. The **Server** setting tells Samba to authenticate against the domain controller without fully joining the domain. The **Domain** setting tells Samba to fully join the domain using Windows NT 4 protocols. The **ADS** setting tells Samba to fully join the domain using Active Directory (AD) protocols. Any of these options will work, if properly configured. The **User** setting tells Samba to use its local account database, so this setting won’t do as the question specifies.

6. B. The **name resolve order** option in Samba determines what tools Samba uses to resolve hostnames into IP addresses. Since only one option (`[lmhosts]`) appears in this example, this is the only tool that’s used, as stated by option B. Option A is incorrect because no other methods will be used. Options C and D are incorrect because the **name resolve order** option controls Samba’s own name resolution, not how it functions as a NetBIOS name server or how it delivers names to clients.

7. C. The Remote Desktop Protocol (RDP) is used by Windows systems to support remote GUI logins. (The Linux `rdsktop` program is an RDP client.) The Virtual Network Computing (VNC) software is a cross-platform remote GUI login tool using the Remote Framebuffer (RFB) protocol. Thus, option C is correct. Since both tools are GUIs, options A and B are both incorrect. Option D would more accurately describe X (used by Unix and Linux) vs. RDP (used by Windows).

8. A. The **vncserver** script starts the VNC server as an ordinary user, enabling subsequent access to the Linux computer from remote systems. The **vncviewer** program is the VNC client; the user might use this program on a remote Linux system to access the server that’s launched by **vncserver**. The **Xvnc** program is the actual VNC server binary, but it must be launched with various options—that’s what the **vncserver** script does. The **vncpasswd** utility sets a VNC password; the command specifies that VNC has already been configured, so this step isn’t necessary at this point.

9. D. FTP server programs vary in design: some are intended to be run from a local or SysV startup script, others are intended to be run from super servers, and others can be launched in either way. The needs of the site must also be considered; for instance, a lightly used FTP server might best be launched from a super server, whereas an FTP server that’s in constant use might better be launched from a startup script. Thus, option D is correct.

10. D. The **UserDir** directive sets the subdirectory name that will be served as personal Web pages. The **ServerDir** directive is fictitious. **ServerRoot** sets the base directory where Apache looks for various files; many other options are specified relative to this one. The **DocumentRoot** directive sets the location of the server’s **main** home page, rather than individual users’ *personal* home pages.

11. A. The Squid program is a caching proxy server, meaning that it provides the features described in the question. PHP is a tool for running Web-centric scripts. Jynx is a text-based Web browser. CGI is the Common Gateway Interface, a tool for running scripts from a Web server.

12. C. Tomcat refers to a package that enables an Apache server to run Java servlets, as described in option C. Tomcat has nothing to do with remote GUI configuration, the **cat** utility, or SSL encryption.

13. B. The **wget** command retrieves a file from a Web (HTTP) server. Used with the **-r** option, **wget** retrieves an entire Web site, so option B is correct. Although **curl** can also be used to retrieve documents from Web sites, option A’s syntax is incorrect, and **curl** isn’t a good tool for retrieving an entire site recursively. Apache is a Web server, not a client, so option C is incorrect. Option D will launch the text-based Lynx Web browser, enabling you to view the current site; but this action won’t save the site for subsequent editing.

14. C. The **ftp** command to retrieve a file is **get** ( *receive* will also work, and multiple variants, such as **mget**, are also available.) The **cp** command is a Linux Bash command to copy a file, but it doesn’t work in **ftp**. The **Download** command is fictitious in this context. The **scp** command is a tool that’s part of the Secure Shell (SSH) package.

15. D. The **lcd** command in **ftp** changes the local current directory; it does as the question specifies, so option D is correct. Option A sounds promising if you’re familiar with Bash options; however, the change implemented in this way does not affect the already launched **ftp** instance, so option A is incorrect. The **cd** command in option B changes the current directory on the *server*, not on the *client*, as the question specifies. The **change-to** command in option C is fictitious.
