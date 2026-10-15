
# 为了可靠性进行安装与配置 157

| mpd | off | off | off | off | off | off | off |
| arpwatch | off | off | off | on | off | off | off |
| atd | off | off | off | on | off | off | off |
| named | off | off | off | off | off | off | off |
| keytable | off | off | on | on | on | off | off |
| gpm | off | off | on | on | on | off | off |
| innd | off | off | off | off | off | off | off |
| ipchains | off | off | on | on | on | on | off |
| irda | off | off | off | off | off | off | off |
| isdn | off | off | on | on | on | off | off |
| pccmia | off | off | on | on | off | off | off |
| kcdrocrate | off | off | off | off | off | off | off |
| kudzu | off | off | off | on | on | off | off |
| linuxconf | off | off | on | on | on | off | off |
| lpd | off | off | on | on | off | off | off |
| mars-ve | off | off | off | off | off | off | off |
| nfs | off | off | off | off | off | off | off |
| nlock | off | off | off | on | on | off | off |
| sshd | off | off | off | on | on | off | off |
| ident | off | off | off | on | on | off | off |
| portmap | off | off | off | off | off | off | off |
| postgresql | off | off | off | off | off | off | off |
| ppo | off | off | off | off | off | off | off |
| rstatd | off | off | off | off | off | off | off |
| rersad | off | off | off | off | off | off | off |
| rwalld | off | off | off | off | off | off | off |
| rwhod | off | off | off | off | off | off | off |
| smb | off | off | off | off | off | off | off |
| sendmail | off | off | on | on | off | off | off |
| snmpd | off | off | off | off | off | off | off |
| rhndd | off | off | off | on | on | off | off |
| ypbind | off | off | off | off | off | off | off |
| yppasswd | off | off | off | off | off | off | off |
| ypserv | off | off | off | off | off | off | off |
| autofs | off | off | off | off | on | off | off |
| bootparam | off | off | off | off | off | off | off |
| dhcpd | off | off | off | off | off | off | off |
| gated | off | off | off | off | off | off | off |
| kadmin | off | off | off | off | off | off | off |
| kprop | off | off | off | off | off | off | off |
| krb524 | off | off | off | off | off | off | off |
| krb5kdc | off | off | off | off | off | off | off |
| mcsrv | off | off | off | off | off | off | off |
| mysql | off | off | off | off | off | off | off |
| nscd | off | off | off | off | off | off | off |
| ntpd | off | off | off | off | off | off | off |
| ups | off | off | off | off | on | off | off |
| ldap | off | off | off | off | off | off | off |
| pvmd | off | off | off | off | off | off | off |
| pxe | off | off | off | off | off | off | off |
| rarpd | off | off | off | off | off | off | off |
| routed | off | off | off | off | off | off | off |
| squid | off | off | off | off | off | off | off |
| vmncerver | off | off | off | off | off | on | off |
| vmware | off | off | off | off | on | on | off |
| arkeia | off | off | on | on | on | off | off |

```
xinetd based services:
amandaix: off
amidxtape: off
finger: on
linuxconf-web: off
rexec: off
rlogin: on
rsh: on
swat: off
tntalk: off
talk: off
telnet: on
tftp: off
wu-ftpdd: on
comsat: off
imap: off
imaps: off
ipop2: off
nipop3: off
pop3s: off
eklogin: off
gssftp: off
klogin: off
krb5-telnet: off
shell: off
```

以 `xinetd`（输出中**加粗**的部分）为例，此列表告诉我们 `xinetd` 服务将在运行级别 3、4 和 5 启动，而在运行级别 0、1、2 和 6 处于关闭状态。注意列表的末尾，`ckconfig` 同时也告诉我们 `xinetd` 支持哪些服务；我们很快会再次查看 `xinetd`，你将看到它的意义。为了确保 `xinetd` 在运行级别 6 启动，请使用此命令：

```
### ckconfig --level 6 xinetd on
```

要确认此操作成功，请执行此命令：

```
### ckconfig --list xinetd
xinetd	0:off 1:off 2:off 3:on 4:on 5:on 6:on
```

或者，直接从运行级别目录进行确认：

```
### ls -1 /etc/rc.d/rc6.d/*xinetd
lrwxrwxr-x 1 root root 16 Jul 25 13:59 /etc/rc.d/rc6.d/S50xinetd ->
../init.d/xinetd
```
