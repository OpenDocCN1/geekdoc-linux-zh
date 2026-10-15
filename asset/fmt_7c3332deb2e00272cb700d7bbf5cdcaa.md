
```bash
$ whereis ls
ls: /bin/ls /usr/man/man1/ls.1.gz
```

```bash
$ type ls
ls is aliased to `ls --color=auto`
```

```bash
$ type -a ls
ls is aliased to `ls --color=auto`
ls is /bin/ls
```

```bash
ln -s /mnt/projdata projdata
ls -l projdata
lrwxrwxrwx 1 root root 13 Jan 26 12:09 projdata -> /mnt/projdata
```

```bash
cd ~jaime
ln ccontactlist.txt /backup/home_jaime_ccontactlist.txt
ls -l ccontactlist.txt
-rw-r--r-- 2 jaime users 0 Jan 26 13:08 ccontactlist.txt
```

```bash
ls -i ccontactlist.txt
17392 ccontactlist.txt
find / -inum 17392
/home/jaime/ccontactlist.txt
/backup/home_jaime_ccontactlist.txt
```

```bash
tar -czf archive.tar.gz /foo
```

```
tar: Removing leading `/' from member names
foo/
foo/install.log
foo/install.log.syslog
foo/.bash_logout
```

```bash
etc/
etc/sysconfig/
etc/sysconfig/network-scripts/
etc/sysconfig/network-scripts/ifup-aliases
etc/sysconfig/network-scripts/ifcfg-lo
```

```bash
etc/
etc/sysconfig/
etc/sysconfig/network-scripts/
etc/sysconfig/network-scripts/ifup-aliases
etc/sysconfig/network-scripts/ifcfg-lo
```

```
drwxr-xr-x 1 root root 0 2015-02-10 03:46 etc/
drwxr-xr-x 1 root root 0 2015-01-31 10:09 etc/sysconfig/
drwxr-xr-x 1 root root 0 2014-11-10 22:13 etc/sysconfig/network-scripts/
```

```bash
find . | cpio -o > archive.cpio
```

```bash
ls *.txt | cpio -o > txt.cpio
```

```bash
find /home -iname *.mp3
$ find / -iname "*.txt" | sort
```

```bash
find / -iname *.txt 2>/dev/null | more
```

```
./kde/share/apps/deprint/db_cups.txt
./1.txt
./3.txt
```

```bash
find / -iname *.txt > foundfiles
```

```bash
find / -iname *.txt 2>errors
```

```bash
find / -iname *.txt > gooddata 2>bad
```

```bash
find / -iname *.txt > /dev/null 2>&1
```

```bash
cat codes.c | nl | lpr
```

```bash
lsof /mnt/cdrom | mail -s"CD-ROM Users"
```

```bash
make modules ; echo MAKE_INSTALL
```

```bash
compile && mail root -s "compile"
```

```bash
tar -czvf /dev/sda || mail root -s "backup"
```

```bash
export DATETIME='date'
echo $DATETIME
Tue Jan 13 17:18:35 PST 2004
```

```bash
file $(grep -l /usr/src/linux-2.4.2)
```

```bash
ldd 'which ls'
linux-so.1 => (0xb78c000)
libinux.so.1 => /lib/i386-linux-gnu/libinux.so.1 (0xb74e000)
libacl.so.1 => /lib/i386-linux-gnu/libacl.so.1 (0xb745000)
libc.so.6 => /lib/i386-linux-gnu/libc.so.6 (0xb795000)
libpcre.so.3 => /lib/i386-linux-gnu/libpcre.so.3 (0xb757000)
libdl.so.2 => /lib/i386-linux-gnu/libdl.so.2 (0xb752000)
/lib/ld-linux.2 (0xb778d00)
libattr.so.1 => /lib/i386-linux-gnu/libattr.so.1 (0xb754c00)
```

```bash
find / -iname *.txt | tee findit.out
```

```bash
find / -iname readme | cat > mongofile.txt
```

```bash
find / -iname readme | xargs cat > mongofile.txt
```

```
1: steve johnson
2: guillermo villalobos
3: bo regard
4: lawrence aribacus
5: marge innovera
```

```bash
cut -c 20-40 /etc/passwd | tail -n 5
ar/spool/postfix:/bin
hare/pvm3:/bin/bash
ross brunson:/home/rb
home/snuffy:/bin/bash
:/home/quotaboy:/bin/
```

```bash
cut -d: -f 1,5,6 /etc/passwd | tail -n 5
postfix::/var/spool/postfix
pvm::/usr/share/pvm3
brunson:ross brunson:/home/rbrunson
snuffy::/home/snuffy
quotaboy::/home/quotaboy
```

```
Line one of file1
Line two of file2
users:
brunson:500:
suffy:501:
quotaboy:502:
```

```
Line one of file1
Line two of file2
users:
brunson:500:
suffy:501:
quotaboy:502:
```

```bash
uniq -u /etc/passwd
rbrunson:x:500::/home/rbrunson:/bin/bash
suffy:x:501::/home/snuffy:/bin/bash
quotaboy:x:502::/home/quotaboy:/bin/bash
```

```bash
uniq -u /etc/passwd > /etc/newpasswd
```

```bash
head -n 5 /etc/fstab
=/ ext3 defaults 1 1
none /dev/pts dev=5,mode=620 0
none /proc defaults 0
none /dev/shm tmpfs 0
/dev/hda swap 0
```

```bash
tail -n 5 /etc/passwd
netdump:x:34:34:/var/crash:/bin/bash
quagga:x:92:92:/var/run/quagga:/sbin/nologin
radvd:x:75:75:/sbin/nologin
rbrunson:x:500::/home/rbrunson:/bin/bash
snuffy:x:501::/home/snuffy:/bin/bash
```

```
Feb 23 21:00:01 sshd(pam_unix) [29358]: closed for user root
Feb 23 21:00:04 sshd(pam_unix) [29501]: opened for user root by (uid=0)
Feb 23 21:00:13 sshd(pam_unix) [29501]: closed for user root
Feb 23 21:00:16 sshd(pam_unix) [29549]: opened for user root
```

pr --columns=2 50linefile 50linefile 页

2004-02-23 21:02 1

1 看门定时器 定 26 以及一些伯克希卡。

2 27 内部温度以

deg

3 Alan Cox <a 28 给出温度。

4 29

5 Custom Linux D 30 第三个接口日志

ke

```
[root@localhost root]# fmt -35 50linefile | pr --column=2
2004-02-23 21:49 50linefile
```

页 1

1 看门定时器温度。 29 30 第三个

Timer Interfaces 接口日志内核消息

Linux 操作系统 2 额外的警报事件。

3 Alan Cox 31 32 软件和

```bash
tr 'A-Z' 'a-z' < commands.txt
```

```bash
tr [:upper:] [:lower:] < commands.txt
```

```bash
sed -option action/regexp/replacement/flag filename
```

```bash
sed 's/bob/BOB/g ; s/BOB/snuffy/g' file1
```

```bash
sed -e s/bob/BOB/g -e s/BOB/snuffy/g file1
```

```bash
sed 's/is not/is too/g' file1
```

```bash
sed -f scriptfile targetfile
```

```bash
sed -n 's/machine/MACHINE/pg' watchdog.txt
```

```bash
sed -n '1,5s/server/SERVER/pg' sedfile
```

X SERVER 使用此目录来存储当前键映射的编译版本和/或客户端使用的任何临时键映射。X SERVER 时间。任何 SERVER 的默认键映射通常存储在：

在考试中，sed 题目都是关于如何查找和替换字符串，特别关注全局替换与单次替换。

```bash
find / -name readme -exec grep -iw kernel {} \;
```

```bash
grep -v :x: /etc/passwd
snuffy:$1$3O238@jrk$WCt15uH7V0EgxdtFT1xkk1:501::/home/snuffy:/bin/bash
```

```bash
grep -ir fool /usr/share/doc | tail -n 15
```

```bash
grep -irw fool /usr/share/doc | tail -n 15
```

```bash
rpc:x:490:65534:user for rpcbind:/var/lib/empty:/sbin/nologin
rtkit:x:492:490:RealtimeKit:/proc:/bin/false
```

```bash
egrep '(false|nologin)' /etc/passwd
```

```bash
egrep '(one|three|eight)' filetosearch.txt
grep -f searchterms.txt foobartar.fu
```

```bash
grep -rl Kernel /usr/share/doc | wc -l
138
```

```bash
grep -rlw Kernel /usr/share/doc | wc -l
131
```

```bash
grep -rwl Kernel\. /usr/share/doc | wc -l
27
```

```bash
grep -rwl silly /usr/share/doc | wc -l
93
```

```bash
grep -rwn -C2 silly /usr/share/doc
```

01 第一行包含 broad

02 第二行包含 bring

03 第三行包含 brush

04 第四行以 BRIDGE 结尾：bridge

broad 05 第五行以 BROAD 开头

06 第六行不包含四个词中的任何一个

07 此行包含 bringing, broadened, brushed

```bash
grep "\<br[^i]" watch.txt
01 第一行包含 broad
03 第三行包含 brush
broad 05 第五行以 BROAD 开头
```

```bash
grep "ad\>" watch.txt
```

01 第一行包含 broad broad

broad 05 第五行以 BROAD 开头

```

```bash

linux-8z04:~ # jobs

[1] - Stopped      top

[2]+ Stopped      vim

[3] Running      strace top &

```

ps

```

PID TTY          TIME CMD

19856 pts/0      00:00:00 bash

20057 pts/0      00:00:00 ps

```

```bash

ps -a

PID TTY TIME CMD

1497 tty1 00:00:00 startx

1510 tty1 00:00:00 init

1523 tty1 00:00:00 gnome-session

1528 tty1 00:00:00 xinit <defunct>

15075 pts/1 00:00:00 ps

... 为了可读性，输出已截断。

```

```

init-apmd

atd

flush

bonobo-activati

crond

dhcp

evolution-alarm

confd

gnome-cups

gnome-panel

gnome-settings

gnome-terminal-bash

~-mgt-pty-helper

```

```

总已内存 (MemTotal and SwapTotal /proc/meminfo)

已内存（按总计计算）

free 空闲内存 (MemFree and SwapFree /proc/meminfo)

共享内存（由 tmpfs 共享，如果不可用则显示为 0）

内核使用的缓冲区（Buffers /proc/meminfo）

已缓存的内存（Cached /proc/meminfo）

```

```bash

kill -1 PID or UP（重启进程）

```

```bash

kill -9 PID or KILL（杀死进程）

```

```bash

jobs

[1]+ Stopped      vim

```

```bash

kill %1

Vim: 接收到信号 TERM

Vim: 完成。

```

```bash

ps aux | grep mybig

brunson 14729 19.2 0.6 5254/pts/0 R 01:30 renice +5 -14729

```

```bash

top -b -n 1 | mail@server.xxx -s "Top output from Server 1"

```

```bash

System1:~ ross$ localbash[detached]

```

.............78229.Local (Detached)
.............78520.bash (Attached)
2 Sockets in /var/folders/d7/mgpx1wd6ytx4000gr/T/.screen.
action/to/replacewith/modifier
这是行 1

这是更长的行 2

这是更长的行 3

这是行 1

#
fdisk /dev/sdb

欢迎使用 fdisk (util-linux 25.2)。更改将留在内存中，直到你决定写入它们。使用 write 命令时要小心。设备不包含识别的分区表。
创建一个标识符为 0x25fd22 的新磁盘。
```bash

Command (m for help): p

Disk /dev/sdb: 8 GiB, 8589934592 bytes, 16777216 扇

扇区大小：1 * 512 = 512 字节

扇区大小（逻辑/物理）：512 字节 / 512 字节

I/O 大小（最小/最佳）：512 字节 / 512 字节

磁盘类型：dos

标识符：0x25fd22

```

```bash

Command (m for help): n

分区类型

p 主（0 个主，0 个扩展，4 空闲）
```
