# Table B-1 (continued)

| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| :--- | :--- | :--- | :--- | :--- |
| **Login Servers** | | | | |
| **Telnet** | telnet-server | /etc/init.d/xinetd<br>(etc/xinetd.d/telnet) | /usr/sbin/xinetd<br>(/usr/sbin/in.telnetd) | /etc/issue.net |
| **Telnet with Kerberos Support** (Krb5-telnet) | krb5-workstation | /etc/init.d/xinetd<br>(etc/xinetd.d.krb5-<br>telnet) | /usr/sbin/xinetd<br>(/usr/kerberos/<br>sbin/telnetd) | /etc/krb5.conf |
| **Open Secure Shell** (Openssh) | openssh-server | /etc/init.d/ssh | /usr/sbin/sshd | /etc/ssh/* |
| **Remote Login** (Rlogin) | rsh-server | /etc/init.d/xinetd<br>(etc/xinetd.d.rlogin) | /usr/sbin/xinetd<br>(/usr/sbin/in.rlogind) | /etc/hosts.equiv<br>$HOME/.rhosts |
| **Remote Login with Kerberos Support** (Eklogin) | krb5-workstation | /etc/init.d/xinetd<br>(etc/xinetd.d.eklogin) | /usr/sbin/xinetd<br>(/usr/kerberos/<br>sbin/eklogind) | /etc/krb5.conf<br>$HOME/.k5login<br>$HOME/.klogin |
| **(Klogin)** | krb5-workstation | /etc/init.d/xinetd | /usr/sbin/xinetd(/usr/<br>kerberos/sbin/klogind) | /etc/krb5.conf<br>$HOME/.k5login<br>$HOME/.klogin |
| **E-mail Servers** | | | | |
| **Remote Mail Access Servers** (IMAP) | dovecot | /etc/init.d/dovecot | /usr/sbin/dovecot | /etc/dovecot |
| **(POP3)** | dovecot | /etc/init.d/dovecot | /usr/sbin/dovecot | /etc/dovecot |
| **E-mail Transfer Servers** (Sendmail) | sendmail<br>sendmail-cf<br>sendmail-doc | /etc/init.d/sendmail | /usr/sbin/sendmail | /etc/sendmail.cf<br>/etc/mail/* |
| **(Postfix)** | postfix | /etc/init.d/postfix | /usr/sbin/postfix | /etc/postfix/* |