# 644 Setting Up Secure Anonymous FTP

This command basically says that anyone listed in the /etc/vsftpd.ftpusers is denied login. The default /etc/vsftpd.ftpusers file contains the following list of users:

+   - root
- bin
daemon
adm
lp
sync
shutdown
halt
mail
news
uucp
operator
games
nbody

# letc/vsftpd.user_list file

If the userlist_deny option is set to YES, vsftpd does not allow users in the /etc/vsftpd.user_list file any access to FTP services. It does not even prompt them for a password. However, if userlist_deny is set to NO, the meaning is reversed and these users are the only allowed access (by the PAM configuration still denies anyone on the /etc/vsftpd.ftpusers list).

# Setting Up Secure Anonymous FTP

Anonymous FTP refers to the use of the username anonymous, which anyone can use FTP to transfer files from a system. Anonymous FTP is a common way to share files on the Internet.

If you have used anonymous FTP to download files from Internet sites, you already know the convenience of that service. Anonymous FTP makes information available to anyone on the Internet. If you have a Fedora Core application that you want to share with the world, set up anonymous FTP on your Fedora Core PC and place the software in an appropriate directory. After that, all you have to do is announce to the world (probably through a posting in the comp.os.linux.announce news) that you have a new program available. Now anyone can get the software from your system at his or her convenience.

Even if you run a for-profit business, you can use anonymous FTP to support your customers. If you sell a hardware or software product, you may want to provide technical information or software "fixes" through anonymous FTP.