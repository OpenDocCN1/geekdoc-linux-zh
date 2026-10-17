
```bash
Selecting previously unselected package gcc-4.7-base:amd64.
(Reading database ... 142987 files and directories currently installed.)
Unpacking gcc-4.7-base:amd64 (from gcc-4.7-base_4.7.2-5_amd64.deb) ...
Setting up gcc-4.7-base:amd64 (4.7.2-5) ...
```

```bash
dpkg -i gcc-4.7-base_4.7.2-5_amd64.deb libgcc1_1:4.7.2-5_amd64.deb
```

```bash
dpkg --force-reinstreq packagename
```

```bash
dpkg --install --force-depends packname
```

```bash
dpkg --install new_pkg.deb --force-conflicts
```

```bash
### dpkg --list krb*
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/Half-conf/Half-inst/trig-await/
Trig-pend
| Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name            Version               Architecture Description
+-------------------------------------------------------
```

（等待，下方的表格碎片碎片）

```text
un krb5-doc            <none> (no description 
available)
ii krb5-locales      1.10.1+dfsg-5+d all Internationalization support 
   for MIT Kerberos
un krb5-user         <none> (no description 
available)

-apt: /etc/apt/conf.d/01autoremove
unattended-upgrades: /etc/apt/conf.d/50unattended-upgrades
apt: /usr/share/man/ja/man5/apt.gz
apt: /usr/share/man/pt/man5/apt.gz
apt: /usr/share/doc/examples/apt.conf
apt-listchanges: /etc/apt/conf.d/20listchanges
aptdaemon: /etc/apt/conf.d/20dbus
aptdaemon: /etc/apt/system.d/org
```

```bash
# apt-get install nginx-light
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
nginx-common
The following NEW packages will be installed:
nginx-common nginx-light
0 upgraded, 1 installed, 0 to remove and 63 not upgraded.
Need to get 392 KB of archives.
After this operation, 863 KB of additional disk space will be used.
Do you want to continue [Y/n]? y
Get: 1 http://cdn.debian.com/deb/whezy/main nginx-common all 1.2.1-2.2+whezy [72.8 KB]
Get: 2 http://cdn.debian.com/deb/whezy/main nginx-light amd64 1.2.1-2.2+whezy [320 KB]
Fetched 392 KB in 1 s (373 KB/s)
Selecting previously unselected package nginx-common.
(Reading database ... 156200 files and directories.)
Unpacking nginx-common (from ...nginx-common_1.2.1-2.2+whezy_all.deb) ...
...
Selecting previously unselected package nginx-light.
Unpacking nginx-light (from ...nginx-light_1.2.1-2.2+whezy_amd64.deb) ...
...
Processing triggers for man-db...
Setting up nginx-common (1.2.1-2.2+whezy) ...
Setting up nginx-light (1.2.1-2.2+whezy) ...
```

```text
deb http://cdn.debian.net/debian/whezy main
deb-src http://cdn.debian.net/debian/whezy main
deb http://security.debian.org/whezy/updates main
deb-src http://security.debian.org/whezy/updates

# whezy-updates, previously known as 'volatile'
deb http://cdn.debian.net/debian/whezy-updates main
deb-src http://cdn.debian.net/debian/whezy-updates main
```

```bash
### apt-get install cpio
Reading package lists... Done
Building dependency tree
Reading state information... Done
Suggested packages:
  libarchiver
The following packages will be upgraded:
  cpio
```

```bash
warning: waiting for transaction lock on /var/lib/rpm/.rpm.lock
```

```bash
### rpm -q kernel
kernel-3.17.7-300.fc21.x864
kernel-3.17.8-300.fc21.x864
```

```bash
rpm -K R-3.1.2-1-fc22.rpm
```

```bash
R-3.1.2-1-fc22.x864.rpm: RSA sha ((MD5) PGP) md5 NOT OK (MISSING KEYS: (MD5) PGP#8e1431d5)
```

```bash
# rpm --import https://getfedora.org/static/8E141D5.txt
# rpm -K R-3.1.2-1-fc22.x864.rpm
R-3.1.2-1-fc22.x864.rpm: rsa sha (md5) pgp md5 OK
```

```bash
# rpm -ivh R-3.1.2-1-fc21.x864.rpm
Preparing...
[##########] 100
Updating / installing...
1:R-3.1.2-1-fc21
[##########] 100
```

```bash
rpm -ivh tarfoo-1.2-3.i386.rpm
tarfoo /etc/tarfoo.conf conflicts with file from snafu-1.1
```

```bash
rpm -ivh --force tarfoo-1.2-3.i386.rpm
```

```bash
rpm -ivh R-3.1.2-1-fc22.x864.rpm
```

```text
error: Failed dependencies:
R-devel = 3.1.2-1-fc22 needed by kernel
R-java = 3.1.2-1-fc22 needed by kernel
R-math = 3.1.2-1-fc22 needed by kernel
```

```text
rpm -V logrotate
/etc/logrotate.conf
```

```text
rpm -V logrotate
/root/logrotate.txt
```

```bash
### rpm -q kernel
kernel-3.17.7-300.fc21.x864
kernel-3.17.8-300.fc21.x864
```

```text
error: "kernel" specifies multiple packages:
kernel-3.17.7-300.fc21.x864
kernel-3.17.8-300.fc21.x864
```

```bash
### rpm -e kernel
```

# rpm -q --changelog cogl

* 2014年11月16日 Kalev Lember <kalevember@gmail.com> - 1.18.2-9

- 来自 rhughes-f20-gnome-3-12 copr 的过时 compat-cogl116

* 2014年11月13日 Kalev Lember <kalevember@gmail.com> - 1.18.2-8

- 只要我们还没有 clutter-gst3，就禁用 cogl-gst (#1158676)

# rpm -qRp tree-1.7.0-3.fc21.x86_64.rpm

libc.so.6() (64bit)

libc.so.6 (GLIBC_2.14) (64bit)

libc.so.6 (GLIBC_2.2.5) (64bit)

libc.so.6 (GLIBC_2.3) (64bit)

libc.so.6 (GLIBC_2.3.4) (64bit)

libc.so.6 (GLIBC_2.4) (64bit)

rpmdlib(CompressedFileNames) <= 3.0.4-1

rpmdlib(FileDigests) <= 4.6.0-1

rpmdlib(PayloadFilesHavePrefix) <= 4.0-1

rtld(GNU HASH)

# rpm -qf /usr/lib64/libc.so.6

glibc-2.20-8.fc21.x86_64

# rpm -qf /etc/krb5.conf

krb5-libs-1.12.2-9.fc21.x86_64

# yum install R

加载插件：langpacks

正在解析依赖关系

--> 运行事务检查

--> 将安装 R.x86_64 0:3.1.2-1.fc21

--> 正在处理包 R-3.1.2-1.fc21.x86_64 的依赖：R-devel = 3.1.2-1.fc21

--> 运行事务检查

--> 将安装 R-devel.x86_64 0:3.1.2-1.fc21 用于包 R-devel-3.1.2-1.fc21.x86_64

--> 正在处理包 R-core-devel-3.1.2-1.fc21.x86_64 的依赖：R-core-devel = 3.1.2-1.fc21

--> 运行事务检查

--> 将安装 R-core.x86_64 0:3.1.2-1.fc21

--> 正在处理包 R-core-devel-3.1.2-1.fc21.x86_64 的依赖：R-core = 3.1.2-1.fc21

--> 运行事务检查

--> 将安装 R-core.x86_64 0:3.1.2-1.fc21

--> 完成依赖解析

依赖关系已解析

=================================================================

================

| 包 | 架构 | 版本 | 存储库 | 大小 |

| :--- | :--- | :--- | :--- | :--- |

| R | x86_64 | 3.1.2-1.fc21 | updates | 27 k |

| R-core | x86_64 | 3.1.2-1.fc21 | updates | 48 M |

| R-core-devel | x86_64 | 3.1.2-1.fc21 | updates | 99 k |

| R-devel | x86_64 | 3.1.2-1.fc21 | updates | 26 k |

事务摘要

===============================================================

安装 1 个包 (+3 个依赖包)

总大小：48 M

总下载大小：48 M

安装大小：74 M

是否确定 [y/d/N]: Y

正在下载包：

运行事务检查

正在运行事务测试

事务测试成功

正在运行事务（已受系统抑制）

警告：RPMDB 在 yum 之外被修改。

正在安装 : R-core-3.1.2-1.fc21.x86_64

正在安装 : R-core-devel-3.1.2-1.fc21.x86_64

正在安装 : R-devel-3.1.2-1.fc21.x86_64

正在安装 : R-3.1.2-1.fc21.x86_64

正在验证 : R-core-3.1.2-1.fc21.x86_64

正在验证 : R-devel-3.1.2-1.fc21.x86_64

正在验证 : R-core-devel-3.1.2-1.fc21.x86_64

正在验证 : R-core-3.1.2-1.fc21.x86_64

已安装：

R.x86_64 0:3.1.2-1.fc21

依赖已安装：

R-core.x86_64 0:3.1.2-1.fc21
```

```bash
$ file file2
$ stat file2
File: `file2'
Size: 0 Blocks: 0 IO Block: 4096 regular empty file
Device: fd00h/64768d Inode: 2261179 Links: 1
Access: (0664/-rw-rw-r--)Uid: (500/sean) Gid: (500/sean)
Access: 2015-02-03 21:47:46.000000000 -0600
Modify: 2015-02-03 21:47:46.000000000 -0600
Change: 2015-02-03 21:48:41.000000000 -0600
Birth: -
```

```bash
dd if=/mnt/cdrom/images/boot.img of=/dev/sdb
```

```bash
dd if=/dev/sdb of=/root/usb.img
```

```bash
dd if=/dev/sda1 of=/dev/sdb1
```

```bash
dd if=/dev/sda of=/root/MBR.img count=1 bs=512
```

```bash
dd if=/root/MBR.img of=/dev/sda count=1 bs=512
```

```bash
mkdir -p /dir1/dir2/dir3/dir4
```

```bash
rmdir -p /dir1/dir2/dir3/dir4
```

```bash
/readme
/usr/src/linux-2.4.20-8/drivers/net/wan/8253x/readme.txt
```

```bash
PRUNEFS="devpts NFS nfs afs sfs proc smbfs autofs auto iso9660"
PRUNEPATHS="/tmp /usr/tmp /var /tmp /afs /net /sfs"
export PRUNEFS
export PRUNEPATHS
```

```bash
find startpath -options arguments
```

```bash
### find /home -iname *.mp3
/home/snuffy/g3 -red house.mp3
```

```bash
find /home -iname *.mp3 -exec cp -f {} \;
```

```bash
find /home -iname *.mp3 -user snuffy
/home/snuffy/bls -all for you.mp3
```

```bash
find /etc -iname fstab -exec cat {} \;
```

```bash
find /home -mtime +7 -iname core -exec rm -f {} \;
```

```bash
find / -user bob -exec chown root {} \;
```

```bash
find /data -user tjordan -exec chgrp users {} \;
```

```bash
find /data -user tjordan -ok chgrp users {} \;
```
