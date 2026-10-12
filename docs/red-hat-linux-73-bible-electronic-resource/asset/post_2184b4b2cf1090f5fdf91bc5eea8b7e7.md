
## Table C-1: Quick Reference to Network Services

| Feature | Package names | Startup script(s) | Daemon | Configuration file(s) |
| :-- | :-- | :-- | :-- | :-- |
| **Web Server** | | | | | |
| Web Page Server (Apache) | apache apache-manual apache-devel | /etc/init.d/httpd | /usr/sbin/httpd | /etc/httpd/conf/httpd.conf |
| (Tux) | tux | /etc/init.d/tux | /usr/sbin/tux | /etc/sysconfig/tux |
| **File Servers** | | | | | |
| FTP Servers (Wu-ftpd) | wu-ftpd | /etc/init.d/xinetd /etc/xinetd.d/wu-ftpd | /usr/sbin/xinetd /usr/sbin/in.ftpd | /etc/ftpaccess /etc/ftphosts /etc/ftpusers /etc/ftpgroups |
| (Vs-ftpd) | vsftpd | /etc/init.d/xinetd /etc/xinetd.d/vsftpd | /usr/sbin/vsftpd | /etc/vsftpd.conf /etc/vsftpd.user_list |
| FTP Server with Kerberos support (Gss-FTP) | krb5-workstation | /etc/init.d/xinetd /etc/xinetd.d/gssftp | /usr/sbin/xinetd /usr/kerberos/sbin/ftpd | /etc/krb5.conf |
| Samba/Windows File & Printers (SMB) | samba-common samba-client samba-swat | /etc/init.d/smb /etc/init.d/winbind | /usr/sbin/smbd /usr/sbin/nmbd /usr/sbin/winbind | /etc/samba/smb.conf |
| **UNIX Network System (NFS)** | nfs-utils | /etc/init.d/nfs /etc/init.d/nfslock | /usr/sbin/rpc.nfsd /usr/sbin/rpc.mountd /sbin/rpc.statd | /etc/exports |
| **NetWare Server (Mars-Nwe)** | mars-nwe | /etc/init.d/mars-nwe | /usr/sbin/nwser /usr/sbin/ngsserv /usr/sbin/nwbind | /etc/nwserv.conf |
| **Login Servers** | | | | | |
| Telnet | telnet-server | /etc/init.d/inetd /etc/xinetd.d/telnet | /usr/sbin/inetd (/usr/sbin/in.telnetd) | /etc/issue.net |
| Telnet w/ Kerberos Support (Krb5-telnet) | krb5-workstation | /etc/init.d/xinetd /etc/xinetd.d/krb5-telnet | /usr/sbin/inetd (/usr/sbin/krb5/sbin/telnetd) | /etc/krb5.conf |
| Open Secure Shell (OpenSSH) | openssh-server | /etc/init.d/sshd | /usr/sbin/sshd | /etc/ssh/* |
| Remote Login (Rlogin) | rsh-server | /etc/init.d/xinetd /etc/xinetd.d/rlogin | /usr/sbin/xinetd (/usr/sbin/in.rlogind) | /etc/hosts.equiv $HOME/.rhosts |
| Remote Login with Kerberos Support (Eklogin) | krb5-workstation | /etc/init.d/xinetd /etc/xinetd.d/eklogin | /usr/sbin/xinetd /usr/kerberos/sbin/klogin | /etc/krb5.conf $HOME/.k5login $HOME/.klogin |
| (Klogin) | | /etc/init.d/xinetd /etc/xinetd.d/klogin | /usr/sbin/xinetd /usr/kerberos/sbin/klogind | /etc/krb5.conf $HOME/.k5login $HOME/.klogin |
| **E-mail Servers** | | | | | |
| E-mail Reader Servers (IMAP) | imap | /etc/init.d/xinetd /etc/xinetd.d/imap | /usr/sbin/xinetd /usr/sbin/imapd | /var/spool/mail/user |
| (IMAP with SSL) | imap | /etc/init.d/xinetd /etc/xinetd.d/imapS | /usr/sbin/xinetd /usr/sbin/imapd | /var/spool/mail/user |
| (POP2) | imap | /etc/init.d/xinetd /etc/xinetd.d/pop2 | /usr/sbin/xinetd /usr/sbin/pop3d | /var/spool/mail/user |
| (POP3) | imap | /etc/init.d/xinetd /etc/xinetd.d/pop3 | /usr/sbin/xinetd /usr/sbin/pop3d | /var/spool/mail/user |
| (POP3 with SSL) | imap | /etc/init.d/xinetd /etc/xinetd.d/pop3s | /usr/sbin/xinetd /usr/sbin/ipop3d | /var/spool/mail/user |
| POP3 with SSL | inap | /etc/init.d/xinetd /etc/xinetd.d/pop3d | /usr/sbin/xinetd /usr/sbin/pop3d | /var/spool/mail/user |
| E-mail Transfer Servers (Sendmail) | sendmail sendmail-cf sendmail-doc | /etc/init.d/sendmail | /usr/sbin/sendmail | /etc/sendmail.cf /etc/mail/* |
| (Postfix) | postfix | /etc/init.d/postfix | /usr/sbin/postfix | /etc/postfix/* |
| E-mail Notice Server (comsat) | comsat | /etc/init.d/xinetd /usr/sbin/in.comsat | /usr/sbin/xinetd /usr/sbin/in.comsat | |
| News Server | innd | /etc/init.d/innd | /usr/bin/innd | /etc/news/* |
| Internet Network News (INN) | | | | | |
| LPR New Generation (LP_Rng) | LPRng | /etc/init.d/lpd | /usr/sbin/lpd | /etc/printcap /etc/printcap.local /etc/lpd.conf /etc/lpd.perms |
| **Print Servers** | | | | | |
| Common UNIX Printing System (CUPS) | cups cups-drivers cups-drivers cups-libs cups-driver-hpijs | /etc/init.d/cups | /usr/sbin/cupsd | /etc/cups/* |
| Network Time Protocol Server (NTP) | ntp | /etc/init.d/ntpd | /usr/sbin/ntpd | /etc/ntp.conf etc/ntp/keys |
| Network Portmap (RPC to DARPA) | portmap | /etc/init.d/portmap | /sbin/portmap | /etc/rpc |
| Samba Administration (SWAT) | samba-swat | /etc/init.d/xinetd /etc/xinetd.d/swat | /usr/sbin/xinetd /usr/sbin/swat | /etc/smb.conf |
| Network Management | arpwatch | /etc/init.d/arpwatch | /usr/sbin/arpwatch | |
| Simple Network Management Protocol (SNMP) | ucd-snmp | /etc/init.d/snmpd | /usr/sbin/snmpd | /etc/snmp/snmpd.conf |
| Network Information Server (YPBIND) | ypbind | /etc/init.d/ypbind | /bin/ypbind | /etc/yp.conf |
| (ypasswd) | ypserv | /etc/init.d/ypasswd | /usr/sbin/ypasswd | /etc/passwd etc/shadow |
| (ypserv) | ypserv | /etc/init.d/ypserv | /usr/sbin/ypserv | /etc/ypserv.conf |
| Dynamic Host Configuration Protocol (DHCP) | dhcp | /etc/init.d/dhcpd | /usr/sbin/dhcpd | /etc/dhcpd.conf |
| Lightweight Directory Access Protocol (LDAP) | openldap-servers | /etc/init.d/ldap | /usr/sbin/slapd /usr/sbin/slurpd | /etc/openldap/slapd.conf |
| Domain Name System Server (DNS) | bind | /etc/init.d/named | /usr/sbin/named | /etc/named.conf /var/named/* |
| Reverse Address Resolution Protocol Server (RARP) | rarpd | /etc/init.d/rarpd | /usr/sbin/rarpd | /etc/ethers |
| **Database Services** | | | | | |
| MySQL Database | mysql mysql-server | /etc/init.d/mysql | /usr/libexec/mysqld | /etc/my.cnf |
| PostgreSQL | postgresql-lbs postgresql postgresql-server | /etc/init.d/postgresql | /usr/bin/postmaster /var/lib/pgsql/data | |
| **User Services** | | | | | |
| Remote Execution Servers (Rsh) | rsh-server | /etc/init.d/xinetd /etc/xinetd.d/rsh | /usr/sbin/xinetd /usr/sbin/in.rshd | /etc/hosts.equiv $HOME/.rhosts |
| (Rexec) | rsh-server | /etc/init.d/xinetd /etc/xinetd.d/rexec | /usr/sbin/xinetd /usr/sbin/in.rexecd | /etc/passwd |
| (Kshell) | krb5-workstation | /etc/init.d/xinetd /etc/xinetd.d/kshell | /usr/sbin/xinetd /usr/kerberos/sbin/kshd | /etc/krb5.conf |
| **Talk Server** (ntalk) | talk-server | /etc/init.d/xinetd /etc/xinetd.d/ntalk | /usr/sbin/xinetd (/usr/bin/in.ntalkd) | |
| (**talk**) | talk-server | /etc/init.d/xinetd /etc/xinetd.d/talk | /usr/sbin/xinetd (/usr/bin/in.talkd) | |
| **Finger Server** (Finger) | finger-server | /etc/init.d/xinetd /etc/xinetd.d/finger | /usr/sbin/xinetd (/usr/bin/in.fingerd) | |
| **Identify Users** (Rusers) | rusers-server | /etc/init.d/rusersd | /usr/sbin/rpc.rusersd | |
| **Write All Users** (Rwall) | rwall-server | /etc/init.d/rwalld | /usr/sbin/rpc.rwalld | |
| **Security Services** | | | | | |
| **System Logging** (syslog) | sysklogd | /etc/init.d/syslog /etc/cipe/ip-up /etc/cipe/ip-down | /sbin/syslog /usr/sbin/cipe-cb | /etc/syslog.conf |
| **Virtual Private Network Servers** (CIPE) | cipe | /etc/cipe/ip-up /etc/cipe/ip-down | /usr/sbin/cipe-cb | /etc/sysconfig/network-scripts/ifdown-cipe and ifup-cipe |
| **Caching Server** (Squid) | squid | /etc/init.d/squid | /usr/sbin/squid | /etc/squid/squid.conf |
