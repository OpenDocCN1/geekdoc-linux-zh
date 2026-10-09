# ## The Very Secure File Transfer Protocol Daemon

The Very Secure File Transfer Protocol Daemon (VSFTPD) is used for sending and receiving files from one computer to another through the Internet. It provides a secure way of transferring files in Linux-based operating systems. It provides greater security, better performance, and more stability than the previous versions of FTP. It allows anonymous or virtual user access. The vsftpd.conf file, which is stored in the /etc/vsftpd directory, is the main configuration file.

![](bbox=[0.76, 0.09, 0.93, 0.16])

![](bbox=[0.21, 0.22, 0.56, 0.47])

# ## vsftpd Configuration Files

vsftpd RPM installs the vsftp daemon in the /usr/sbin/vsftpd directory and the daemon listens on ports 20 and 21. There are some default files that are installed while configuring VSFTPD.

![](bbox=[0.76, 0.6, 0.93, 0.66])

| File | Description |
| :--- | :--- |
| /etc/vsftpd/vsftpd.conf | Configures vsftpd. |
| /etc/init.d/vsftpd | Runs the initialization script for vsftpd. |
| /etc/vsftpd/user_list | Controls the user access for the FTP server using the user_list_deny directive specified in the vsftpd.conf file. Depending on whether the directive is set to YES or NO, the user access is decided. |
| /etc/pam.d/vsftpd | Defines the requirements for a user to access the FTP server. It is a PAM configuration file for vsftpd. |