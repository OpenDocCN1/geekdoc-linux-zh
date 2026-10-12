| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| :--- | :--- | :--- | :--- | :--- |
| **Login Servers** | | | | |
| Telnet | telnet-server | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/issue.net |
| | | (/etc/xinetd.d/telnetd) | (/usr/sbin/in.telnetd) | |
| Telnet with | krb5-workstation | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/krb5.conf |
| (krb5-telnet) | | (/etc/xinetd.d/telnetd) | /usr/kerberos/ |
| Open Secure Shell | openssh-server | /etc/init.d/sshd | /usr/sbin/sshd | /etc/ssh/* |
| (Rremssh) | | | | |
| Remote Login | rsh-server | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/hosts.equiv |
| (Rlogin) | | (/etc/xinetd.d/rlogind) | (/usr/sbin/in.rlogind) | $HOME/.rhosts |
| Remote Login with | krb5-workstation | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/krb5.conf |
| Kerberos Support | | (/etc/xinetd.d/elogind) | /usr/kerberos/ | $HOME/.klogin |
| (Etelogin) | | | /sbin/elogind | $HOME/.klogin |
| (Elogin) | krb5-workstation | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/krb5.conf |
| | | (/etc/xinetd.d/klogind) | /usr/kerberos/ | $HOME/.klogin |
| | | | /sbin/klogind | $HOME/.klogin |
| **E-mail Servers** | | | | |
| **Access Mail** | | | | |
| **Servers** | | | | |
| (IMAP) | imap | /etc/init.d/xinetd | /usr/sbin/xinetd | /var/spool/mail/user |
| | (/etc/inetd.d/imapd) | (/usr/sbin/imapd) | |
| (IMAP with SSL) | imap | /etc/init.d/xinetd | /usr/sbin/xinetd | /var/spool/mail/user |
| | (/etc/inetd.d/imapss) | (/usr/sbin/imapss) | |
| (POP2) | imap | /etc/init.d/xinetd | /usr/sbin/xinetd | /var/spool/mail/user |
| | (/etc/inetd.d/pop2d) | (/usr/sbin/ipop2d) | |
| (POP3) | imap | /etc/init.d/xinetd | /usr/sbin/xinetd | /var/spool/mail/user |
| | (/etc/inetd.d/pop3d) | (/usr/sbin/ipop3d) | |
| (POP3 with SSL) | imap | /etc/init.d/xinetd | /usr/sbin/xinetd | /var/spool/mail/user |
| | (/etc/inetd.d/pop3s) | (/usr/sbin/ipop3s) | |