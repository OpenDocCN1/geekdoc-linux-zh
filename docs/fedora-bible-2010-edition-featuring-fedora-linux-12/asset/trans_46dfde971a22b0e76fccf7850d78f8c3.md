

## 表 B-1：网络服务快速参考

| 特性 | 软件包名称 | 启动脚本 | 守护进程 | 配置文件 |
| :--- | :--- | :--- | :--- | :--- |
| Web 服务器 (Apache) | httpd | /etc/init.d/httpd | /usr/sbin/httpd | /etc/httpd/conf/httpd.conf |
| &nbsp;&nbsp;&nbsp;&nbsp;模块 | httpd-massail | | | |
| &nbsp;&nbsp;&nbsp;&nbsp; | httpd-devssl | | | |
| 文件服务器 | | | | |
| FTP 服务器 (v4.02+) | vsftpd | /etc/init.d/vsftpd | /usr/sbin/vsftpd | /etc/vsftpd/vsftpd.conf<br>/etc/vsftpd/vsftpd_list |
| Samba | samba | /etc/init.d/smb | /usr/sbin/smbd | /etc/samba/smb.conf |
| Windows 文件和打印机 (SMB) | samba-common | /etc/init.d/nmb | /usr/sbin/nmbd | |
| &nbsp;&nbsp;&nbsp;&nbsp; | samba-client | | | |
| &nbsp;&nbsp;&nbsp;&nbsp; | samba-swat | | | |
| &nbsp;&nbsp;&nbsp;&nbsp; | samba-winbind | | | |
| &nbsp;&nbsp;&nbsp;&nbsp; | system-config-samba | | | |
| UNIX 网络文件系统 (NFS) | nfs-utils | /etc/init.d/nfs | /usr/sbin/rpc.nfsd | /etc/exports |
| &nbsp;&nbsp;&nbsp;&nbsp; | system-configure | /etc/init.d/autolock | /usr/sbin/rpc.mountd | |
| &nbsp;&nbsp;&nbsp;&nbsp; | /etc/init.d/lockd | /sbin/rpc_statd | | |
| 登录服务器 | openssh-server | /etc/init.d/sshd | /usr/sbin/sshd | /etc/ssh/* |
| Shell | | | | |
| 邮件服务器 | dovecot | /etc/init.d/dovecot | /usr/sbin/dovecot | /etc/dovecot.conf |
| 远程访问邮件服务器 (IMAP/POP3) | | | | |
| 邮件传输服务器 (Sendmail) | sendmail | /etc/init.d/sendmail | /usr/lib/sendmail | /etc/mail/sendmail.mc |
| &nbsp;&nbsp;&nbsp;&nbsp; | sendmail-of | /etc/init.d/sendmail-of | /etc/mail/sendmail.cf | /etc/mail* |
| &nbsp;&nbsp;&nbsp;&nbsp; | sendmail-doc | | | |
| (Postfix) | postfix | /etc/init.d/postfix | /usr/lib/postfix | /etc/postfix/master.cf |
| 新闻服务器 | | | /usr/lib/news/bin/master | |
| 互联网网络新闻 (INN) | inn | /etc/init.d/inn | /usr/lib/news/bin/inn | /etc/news/* |
| 打印服务器 | | | | |
| 通用 UNIX 打印系统 (CUPS) | cups | /etc/init.d/cups | /usr/sbin/cupsd | /etc/cups/* |
| &nbsp;&nbsp;&nbsp;&nbsp; | cups-libs | | | |
| 网络管理服务器 | | | | |
| 网络时间协议 (NTP) | ntp | /etc/init.d/ntpd | /usr/sbin/ntpd | /etc/ntp.conf<br>/etc/ntp/sys |
| Samba 管理 (SAMBA) | samba-swat | /etc/init.d/swat | /usr/sbin/swat | /etc/swat.conf |
| &nbsp;&nbsp;&nbsp;&nbsp; | argwatch | /etc/init.d/argwatch | /usr/sbin/argwatch | /etc/sysconfig/argwatch |
| 网络简单网络管理协议 (SNMP) | net-snmp | /etc/init.d/snmpd | /usr/sbin/snmpd | /etc/snmp/snmp.conf |
| &nbsp;&nbsp;&nbsp;&nbsp; | | /etc/init.d/snmptrapd | /usr/sbin/snmptrapd | /etc/snmp/snmp.conf |

