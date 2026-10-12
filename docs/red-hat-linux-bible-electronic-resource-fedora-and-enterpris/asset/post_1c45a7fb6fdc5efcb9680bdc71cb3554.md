
| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
|---|---|---|---|---|
| Web Server | httpd | /etc/init.d/httpd | /usr/sbin/httpd | /etc/httpd/conf/httpd.conf |
| Web Servers (Apache) | httpd-manual httpd-devel | | | |
| (Tux) | tux | /etc/init.d/tux | /usr/sbin/tux | /etc/sysconfig/tux |
| File Servers | | | | |
| FTP Servers (vs-ftpd) | vsftpd | /etc/init.d/vsftpd | /usr/sbin/vsftpd | /etc/vsftpd.conf /etc/vsftpd.user_list |
| FTP Server with Kerberos Support (GSS-FTP) | krb5-workstation | /etc/xinetd.d/vsftpd (/etc/xinetd.d/gssftp) | /usr/sbin/xinetd (/usr/kerberos/sbin/ftpd) | /etc/xinetd.conf /etc/krb5.conf |
| Samba Windows File and Printers (SMB) | samba samba-common samba-client samba-swat samba-config-samba | /etc/init.d/smbd /etc/init.d/nmbd /etc/init.d/winbindd | /usr/sbin/smbd /usr/sbin/nmbd /usr/sbin/winbindd | /etc/samba/smb.conf |
| UNIX Network File System (NFS) | nfs-utils nfs-utils-config nfs-utils-config-nfs | /etc/init.d/nfs /etc/init.d/nfslock | /usr/sbin/rpc.nfsd /usr/sbin/rpc.mountd /sbin/rpc.statd | /etc/exports |
| AppleTalk File and Print Server (Netatalk) | netatalk | /etc/init.d/atalk | /usr/sbin/atalkd | /etc/atalk/* |
| NetWare Server (Mars-Nwe) | mars-nwe | /etc/init.d/mars-nwe | /usr/sbin/nwserv /usr/sbin/ncpserv /usr/sbin/nwbind | /etc/nwserv.conf |
| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| :--- | :--- | :--- | :--- | :--- |
| **Login Servers** | | | | |
| Telnet | telnet-server | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/issue.net |
| | | (/etc/xinetd.d/telnetd) | (/usr/sbin/in.telnetd) | |
| Telnet with | krb5-workstation | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/krb5.conf |
| (krb5-telnet) | | (/etc/xinetd.d/telnetd) | /usr/kerberos/ | |
| Open Secure Shell | openssh-server | /etc/init.d/sshd | /usr/sbin/sshd | /etc/ssh/* |
| (Remsh) | | | | |
| Remote Login | rsh-server | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/hosts.equiv |
| (Rlogin) | | (/etc/xinetd.d/rlogind) | (/usr/sbin/in.rlogind) | $HOME/.rhosts |
| Remote Login with | krb5-workstation | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/krb5.conf |
| Kerberos Support | | (/etc/xinetd.d/elogind) | /usr/kerberos/ | $HOME/.klogin |
| (Elogin) | | | /sbin/elogind | $HOME/.klogin |
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
| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
|:---|:---|:---|:---|:---|
| E-mail Transfer Servers (Sendmail) | sendmail sendmail-cf sendmail-doc sendmail | /etc/init.d/sendmail | /usr/sbin/sendmail | /etc/sendmail.cf<br>*/etc/mail/* |
| (Postfix) | postfix | /etc/init.d/postfix | /usr/sbin/postfix | /etc/postfix/* |
| E-mail Notice | | /etc/init.d/xinetd | /usr/sbin/xinetd | |
| Server (comsat) | comsat | (/etc/xinetd.d/comsat) | /usr/sbin/comsat | |
| News Server | | | | |
| Internet Network News (INN) | inn | /etc/init.d/inn | /usr/bin/inn | /etc/news/* |
| Print Servers | | | | |
| LPR New Generation (LPRng) | lprng | /etc/init.d/lpd | /usr/sbin/lpd | /etc/printcap<br>/etc/printcap.local<br>/etc/lpd.conf<br>/etc/lpd.perms |
| Common UNIX Printing System (CUPS) | cups cups-drivers cups-libs cups-drivers-cups drivers-hipjs | /etc/init.d/cups | /usr/sbin/cupsd | /etc/cups/* |
| Network Administration Servers | | | | |
| Network Time Protocol Server (NTP) | ntp | /etc/init.d/ntpd | /usr/sbin/ntpd | /etc/ntp.conf<br>/etc/ntp/keys |
| Network Portmap (RPC to DARPA) | portmap | /etc/init.d/portmap | /sbin/portmap | /etc/rpc |
| Samba Administration (SWAT) | samba-swat | /etc/init.d/xinetd<br>(/etc/xinetd.d/swat) | /usr/sbin/xinetd<br>(/usr/sbin/swat) | /etc/smb.conf |
| Network Management (arpwatch) | arpwatch | /etc/init.d/arpwatch | /usr/sbin/arpwatch | /etc/sysconfig/arpwatch |
## Table C-1 (continued)
| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| --- | --- | --- | --- | --- |
| Simple Network Management Protocol (SNMP) | ucd-snmp | /etc/init.d/snmpd<br>/etc/init.d/snmptrapd | /usr/sbin/snmpd<br>/usr/sbin/snmptrapd | /etc/snmp/snmpd.conf<br>/etc/snmp/snmptrapd.conf |
| Network Information Server (ypbind) | ypbind | /etc/init.d/ypbind | /sbin/ypbind | /etc/yp.conf |
| Information Server (yppasswdd) (ypserv) | ypserv | /etc/init.d/yppasswdd<br>/etc/init.d/ypserv<br>/etc/init.d/dhcpd | /usr/sbin/rpc.yppasswd<br>/usr/sbin/ypserv<br>/usr/sbin/dhcpd | /etc/passwd<br>/etc/shadow<br>/etc/ypserv.conf<br>/etc/dhcpd.conf |
| Dynamic Host Configuration Protocol Server (DHCP) | dhcpd | /etc/init.d/dhcpd | /usr/sbin/dhcpd | /etc/dhcpd.conf |
| Lightweight Directory Access Protocol (LDAP) | openldap-servers | /etc/init.d/ldap | /usr/sbin/ldapd<br>/usr/sbin/slapd | /etc/openldap/slapd.conf |
| Domain Name System Server (DNS) | bind<br>bind-utils | /etc/init.d/named | /usr/sbin/named | /etc/named.conf<br>/var/named/* |
| Reverse Address Resolution Protocol Server (RARP) | rarpd | /etc/init.d/rarpd | /usr/sbin/rarpd | /etc/ethers |
| MySQL Database | mysql<br>mysql-server<br>postgresql<br>postgresql-libs<br>postgresql-server | /etc/init.d/mysql<br>/etc/init.d/postgresql | /usr/libexec/mysqld<br>/usr/bin/postmaster | /etc/my.cnf<br>/var/lib/pgsql/data |
## Table C-1 (continued)
| Feature | Package Name | Startup Script(s) | Daemon | Configuration File(s) |
| :--- | :--- | :--- | :--- | :--- |
| User Services | | | | |
| Remote Execution Servers (rsh) | rsh-server | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/hosts.equiv |
| | | /etc/xinetd.d/rsh | (/usr/sbin/in.rshd) | $HOME/.rhosts |
| (rexec) | rsh-server | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/passwd |
| | | /etc/xinetd.d/rexec | (/usr/sbin/in.rexecd) | |
| (kshell) | krb5-workstation | /etc/init.d/xinetd | /usr/sbin/xinetd | /etc/krb5.conf |
| | | /etc/xinetd.d/kshell | (/usr/kerberos/sbin/kshell) | |
| Talk Server (ntalk) | talk-server | /etc/init.d/xinetd | /usr/sbin/xinetd | |
| | | | | |
| (talk) | talk-server | /etc/init.d/xinetd | /usr/sbin/xinetd | |
| | | /etc/xinetd.d/ntalk | (/usr/sbin/in.ntalkd) | |
| | | /etc/xinetd.d/talk | (/usr/sbin/in.talkd) | |
| Finger Server (Finger) | finger-server | /etc/init.d/xinetd | /usr/sbin/xinetd | |
| | | /etc/xinetd.d/finger | (/usr/sbin/in.fingerd) | |
| Identify Users (Rusers) | rusers-server | /etc/init.d/rusersd | /usr/sbin/rpc.rusersd | |
| Write All Users (Rwall) | rwall-server | /etc/init.d/rwall | /usr/sbin/rpc.rwall | |
## Table C-1 (continued)
| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| :--- | :--- | :--- | :--- | :--- |
| Security Services | | | | |
| System Logging (syslog) | syslogd | /etc/init.d/syslog | /sbin/syslogd | /etc/syslog.conf |
| Virtual Private Network Servers (CIPE) | cipe | /etc/cipe/ip-up /etc/cipe/ip-down | /usr/sbin/ciped | /etc/sysconfig/network-scripts/ifdown-cipe<br>/etc/sysconfig/network-scripts/ifup-cipe |
| Caching Server (Squid) | squid | /etc/init.d/squid | /usr/sbin/squid | /etc/squid/squid.conf |
## Index
$ (dollar sign) metacharacter, 141
$HOME file, 347
& (ampersand), 140
; (semicolon), 140
. (dot) in paths, 149, 153
; (semicolon), 140
{} (braces), environment variables, 144
| (pipe metacharacter), 139
~ (tilde), directories, 153
3dfx video cards, 241
3Dlabs video cards, 241
8mm AIT-2 tapes, 458
### A
AbiWord, 207-209
absolute path, 127
access
exports file, 684
FTP server
control, 776
host computer, 781
real users, 782
UID/GID, 782
PortSentry software, restoring, 560
vsFTPd, configuration, 764-766
wu-ftpd, 768
access point, wireless networks, 575
access.conf file, Apache server configuration, 792
accessibility
keyboard, 97
mouse, 97
accounts
installation and, 22
root user, accessing (MAC OS X), 967
ACPI (Advanced Configuration and Power Interface), 377
acid package, 16
Acrobat Reader, 233-234
Acronis OS Selector, partitions and, 57
Action directive, Apache server, 821
address book, Mozilla, 302
addresses
binding to specific, Apache server, 798
e-mail, Apache server, 803
gateway, default, 570
IP addresses, 592, 610
assigning, 594-595
host names, adding, 571-572
hosts file, 568-569
netmasks, 593
static, 924
adjtime file, 347
administration tasks, 354
administrative tools, 13
administrative account, MySQL, 891
administrative commands, 346-347
administrative configuration files, 347-351
administrative log files, 351
Adobe Acrobat plug-in, 306
Advanced Configuration and Power Interface (ACPI), 377
Advanced Power Management (APM), 376
aecho command, 964
affs file system, 363
afpd daemon, 954, 955
afpd.conf file, 954-956
alert notification tool (Red Hat updates), 382-383
aliases, 133
Apache server, Web content, 814-815
command line automatic completion feature, 136
commands, root user and, 340
aliases file, 347
sendmail, 748-749
AliasWait option, sendmail, 732
allow line, wu-ftpd, 768
AllowBogusHELO option, sendmail, 743
ALTER command (MySQL), 915
alternatives system, selecting alternative software, 379-380
Amanda
amanda.conf file, 475-477
configuring, 473-474
creating directories, 475
disklist file, 477
network services, 478-479
running, 479-480
ampersand (&) metacharacter, 140
amsxex macros (publishing tools), 222
Analog log-file analyzer, 836
anonymous users exports file, 685
FTP
access, 782
wu-ftpd, 770-771
antennas, wireless networks, 579, 580
AOL Instant Messenger, Gaim, 324, 325
AOLserver 3 Web server, 790
Apache server, 788-789
Action directive, 821
addresses
binding to specific, 798
e-mail, 803
browsers, responses to, 823-824
caching, 824-826
canonical names, 804
character sets, 820
configuration, 792
directories
access control, 809
content, 804
users, 807-808
encoding, 819-820
error logging, 833
error response codes, 821-823
group, 802-803
handlers, 821
headers, 821
host name lookups, 810
HTTP port number, 803
httpd.conf file, 793-794
command-line arguments, 829
global environment, 794
lock files, 795
module-specific files, 798
modules, 799-802
PID, 795
root directory, 794
ScoreBoard files, 795
subcomponents, 794
timeout values, 795-796
indexing files, 816-819
language, 819-820
