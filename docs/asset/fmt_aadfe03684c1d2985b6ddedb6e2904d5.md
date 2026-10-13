
# inetd.conf
```
#
# service socket protocol wait/ user server server program
# name type nowait program arguments
#
echo stream tcp nowait root internal
echo dgram udp wait root internal
discard stream tcp nowait root internal
discard dgram udp wait root internal
daytime stream tcp nowait root internal
daytime dgram udp wait root internal
chargen stream tcp nowait root internal
chargen dgram udp wait root internal
ftp stream tcp nowait root /etc/ftpd ftpd
telnet stream tcp nowait root /etc/telnetd telnetd
time stream tcp nowait root internal
time dgram udp wait root internal
bootps dgram udp wait root /etc/bootpd bootpd
tftp dgram udp wait nobody /etc/tftpd tftpd -n
finger stream tcp nowait nobody /etc/fingerd fingerd
exec stream tcp nowait root /etc/rexeced rexecd
login stream tcp nowait root /etc/rlogind rlogind
shell stream tcp nowait root /etc/rshd rshd
talk dgram udp wait root /etc/talkd talkd
ntalk    dgram    udp wait    root /etc/talkd talkd
uucp     stream   tcp nowait  root /etc/uucpd uucpd
comsat   dgram    udp wait    root /etc/comsat comsat
netbios-ssn stream tcp nowait root /usr/local/samba/bin/smbd
netbios-ns dgram udp wait    root /usr/local/samba/bin/nmbd
```

## 示例 2.5 /etc/services
```
#
# Network well known services
#
# Service Port/Protocol Aliases
#
echo        7/tcp
echo        7/udp
discard     9/tcp        sink null
discard     9/udp        sink null
systat     11/tcp       users
daytime    13/tcp
daytime    13/udp
netstat    15/tcp
qotd       17/tcp       quote
chargen    19/tcp       ttytst source
chargen    19/udp       ttytst source
ftp-data   20/tcp
ftp        21/tcp
telnet     23/tcp
smtp       25/tcp       mail
time       37/tcp       timserver
time       37/udp       timserver
rlp        39/udp       resource  # resource location
nameserver 42/udp       name      # IEN 116
whois      43/tcp       nicname
domain     53/tcp       nameserver # name-domain server
domain     53/udp       nameserver
mtp        57/tcp              # deprecated
bootps     67/udp              # bootp server port
bootpc     68/udp              # bootp client port
tftp       69/udp
rje        77/tcp       netrje
finger     79/tcp
link       87/tcp       ttylink
supdup     95/tcp
hostnames 101/tcp       hostname # usually from sri-nic
iso_tsap  102/tcp
x400 103/tcp
x400-snd 104/tcp
csnet-ns 105/tcp
pop 109/tcp postoffice
sunrpc 111/tcp
sunrpc 111/udp
auth 113/tcp authentication
sftp 115/tcp
uucp-path 117/tcp
nntp 119/tcp readnews untp
ntp 123/tcp
ntp 123/udp # network time protocol (exp)
netbios-udp 137/udp # netbios udp
netbios-ssn 139/tcp # netbios tcp
NeWS 144/tcp
snmp 161/udp # snmp request port
snmp-trap 162/udp # snmp monitor trap port
mux 199/tcp # snmpd smux port
src 200/udp # System Resource controller
exec 512/tcp
login 513/tcp
who 513/udp whod
shell 514/tcp cmd # no passwords used
syslog 514/udp
printer 515/tcp spooler # line printer spooler
talk 517/udp
ntalk 518/udp
efs 520/tcp # for LucasFilm
route 520/udp router routed
timed 525/udp timeserver
tempo 526/tcp newdate
courier 530/tcp rpc
conference 531/tcp chat
netnews 532/tcp readnews
netwall 533/udp # for emergency broadcasts
uucp 540/tcp uucpd # uucp daemon
new-rwho 550/udp
remotefs 556/tcp rfs_server rfs
rmonitor 560/udp
monitor 561/udp
```

## 文件系统

UNIX 文件系统是位于一个或多个磁盘上的块分区，作为目录和文件树的容器。构成文件系统的主要结构是超级块、`inode` 和数据块。

超级块描述了文件系统的整体结构。它包含文件系统名称、大小、指向 `inode` 和空闲块列表的指针等。超级块用于在操作期间跟踪文件系统状态，该状态稍后可在启动过程的一部分以及在发生故障时用于验证文件系统的完整性。

文件系统中的每个目录和文件都由一个 `inode` 表示。`inode` 可以被视为一个索引条目。每个 `inode` 从 1 开始按顺序编号，直到为文件系统定义的最大 `inode` 数。`inode` 标识其所代表的文件或目录的属性（表 2.6）。

### 表 2.6 Inode 文件属性

- 文件模式
- 文件类型
- 所有者 UID 和 GID
- 日期和时间戳
- 链接数
- 数据块指针
- 字节大小
- 块大小

数据块用于在文件系统中存储实际的文件数据。通常每个 `inode` 包含 13 个数据块地址槽。前八个地址槽指向文件的前八个文件数据块。第九个地址指向一个内存中 `inode` 结构。当文件打开时，磁盘 `inode` 信息会被复制到该结构中。第 10 到第 13 个地址指向用于寻址大文件的数据块的间接数据块。每个间接块支持 1024 个地址。较新的 UNIX 文件系统可能包含额外的结构来表示更大文件和文件系统。

## 目录结构
