

## 在 chroot  jails 中运行 BIND

为了提高安全性，你可以在 chroot jails 中运行 BIND。有关 chroot jails 的安全优势及设置方法的详细信息，请参见第 466 页。`bind-chroot.sh` Shell 脚本（如下所示）用于设置 BIND 在 chroot jails 中运行，它创建了一个名为 `/var/lib/named` 的目录，该目录替代了根目录（`/`），用于存放所有 BIND 文件。`bind-chroot.sh` 脚本会安装 `bind9` 和 `resolvconf` 软件包（如果尚未安装），然后运行 `bind9` 和 `resolvconf` 初始化脚本来停止 `named`。接着，它在 `/etc/default/bind9` 中的 `named` 选项中添加 `-t` 选项，以便 `named` 在读取其配置文件之前 chroot 到 `/var/lib/named` 目录。`named` 守护进程已设置为以用户 `bind`（`-u bind`）的身份运行。

在 `/var/lib/named` 中创建必要的目录后，脚本将文件从 `/etc/bind` 移动到 `/var/lib/named`，创建从 `/var/lib/named` 指向 `/etc/bind` 的符号链接，并创建 BIND 可能需要的设备并设置其权限。接下来，`bind-chroot.sh` 禁用 `named` 的 apparmor 保护。最后，脚本启动 `named` 和 `resolvconf`，并显示 syslog 文件的末尾。

```bash
$ cat bind-chroot.sh
#!/bin/bash
# install and stop bind
aptitude -y install bind9
service bind9 stop
# install and stop resolvconf
aptitude -y install resolvconf
service resolvconf stop
# add -t /var/lib/named to OPTIONS in /etc/default/bind9
sed -i 's:OPTIONS="(.*)":OPTIONS="\1" -t /var/lib/named': '/etc/default/bind9
# make the chroot directories
mkdir -p /var/lib/named/{etc,dev,var,cache/bind,var/run/bind/run}
# move the configuration to the chroot and link back to /etc
mv /etc/bind /var/lib/named/etc
ln -s /var/lib/named/etc/bind /etc/bind

# create devices and set permissions
mknod /var/lib/named/dev/null c 1 3
mknod /var/lib/named/dev/random c 1 8
chmod 666 /var/lib/named/dev/{null,random}
chown -R bind:bind /var/lib/named/var/*
chown -R bind:bind /var/lib/named/etc/bind

# disable apparmor protection of /usr/sbin/named and restart apparmor
cd /etc/apparmor.d/disable
ln -s /etc/apparmor.d/usr.sbin.named .
service apparmor restart

# start bind and resolvconf
service resolvconf start
service bind9 start

# check that everything started fine
tail /var/log/syslog
```

以下是执行 `bind-chroot.sh` 的输出。您必须在拥有 **root** 权限的情况下运行此脚本。您还必须拥有执行该脚本的权限。在示例中，`bind-chroot.sh` 文件位于当前工作目录中。

```bash
$ sudo ./bind-chroot.sh
Reading package lists... Done
Building dependency tree
Reading state information... Done
Reading extended state information
Initializing package states... Done
No packages will be installed, upgraded, or removed.
0 packages upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 0B of archives. After unpacking 0B will be used.
Writing extended state information... Done
Reading package lists... Done
Building dependency tree
Reading state information... Done
Reading extended state information
Initializing package states... Done

* Stopping domain name service... bind9 [ OK ]
Reading package lists... Done
Building dependency tree
Reading state information... Done
Reading extended state information
Initializing package states... Done
No packages will be installed, upgraded, or removed.
0 packages upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 0B of archives. After unpacking 0B will be used.
Writing extended state information... Done
Reading package lists... Done
Building dependency tree
Reading state information... Done
Reading extended state information
Initializing package states... Done

* Stopping resolvconf... [ OK ]
* Reloading AppArmor profiles
Skipped profile in /etc/apparmor.d/disable: usr.bin.firefox
Skipped profile in /etc/apparmor.d/disable: usr.sbin.named [ OK ]
* Setting up resolvconf... [ OK ]
* Starting domain name service... bind9 [ OK ]
Apr 5 11:28:21 10 named[4138]: command channel listening on ::1#953
Apr 5 11:28:21 10 named[4138]: zone 0.in-addr.arpa/IN: loaded serial 1
Apr 5 11:28:21 10 named[4138]: zone 127.in-addr.arpa/IN: loaded serial 1
Apr 5 11:28:21 10 named[4138]: zone 255.in-addr.arpa/IN: loaded serial 1
Apr 5 11:28:21 10 named[4138]: zone localhost/IN: loaded serial 2
Apr 5 11:28:21 10 named[4138]: running
```

运行此脚本后，所有控制 BIND 的文件都位于这个 chroot jails 中，本章中使用的文件名是指向 chroot jails 中文件的符号链接。请参见下一页的命令和输出。

```bash
$ ls -l /etc/bind /var/lib/named/etc/bind
lrwxrwxrwx 1 root root 23 2010-04-05 11:28 /etc/bind -> /var/lib/named/etc/bind

/var/lib/named/etc/bind:
-rw-r--r-- 1 bind bind 601 2010-03-22 12:59 bind.keys
-rw-r--r-- 1 bind bind 237 2010-03-22 12:59 db.0
-rw-r--r-- 1 bind bind 271 2010-03-22 12:59 db.127
-rw-r--r-- 1 bind bind 237 2010-03-22 12:59 db.255
-rw-r--r-- 1 bind bind 353 2010-03-22 12:59 db.empty
-rw-r--r-- 1 bind bind 270 2010-03-22 12:59 db.local
-rw-r--r-- 1 bind bind 2940 2010-03-22 12:59 db.root
-rw-r--r-- 1 bind bind 463 2010-03-22 12:59 named.conf
-rw-r--r-- 1 bind bind 490 2010-03-22 12:59 named.conf.default-zones
-rw-r--r-- 1 bind bind 165 2010-03-22 12:59 named.conf.local
-rw-r--r-- 1 bind bind 572 2010-03-22 12:59 named.conf.options
-rw-r--r-- 1 bind bind 77 2010-04-05 11:26 rndc.key
-rw-r--r-- 1 bind bind 1317 2010-03-22 12:59 zones.rfc1918
```

BIND 正在 `/var/lib/named` 中的 chroot jails 中运行。由于 `/etc/bind` 目录现在是指向 `/var/lib/named` 的链接，您可以从任一位置对 BIND 进行更改。

## 故障排除

当您启动 DNS 缓存时，`/var/log/syslog` 文件包含类似于以下内容的行。其他类型的 DNS 服务器也会显示类似的消息。

```bash
$ cat /var/log/syslog
...
Apr 26 11:00:02 plum named[9301]: starting 9.7.0-P1 -u bind
Apr 26 11:00:02 plum named[9301]: found 1 CPU, using 1 worker thread
Apr 26 11:00:02 plum named[9301]: loading configuration from '/etc/bind/named.conf'
Apr 26 11:00:02 plum named[9301]: listening on IPv6 interfaces, port 53
Apr 26 11:00:02 plum named[9301]: listening on IPv4 interface lo, 127.0.0.1#53
Apr 26 11:00:02 plum named[9301]: listening on IPv4 interface eth0, 192.168.0.10#53
Apr 26 11:00:02 plum named[9301]: command channel listening on 127.0.0.1#953
Apr 26 11:00:02 plum named[9301]: command channel listening on ::1#953
Apr 26 11:00:02 plum named[9301]: zone 0.in-addr.arpa/IN: loaded serial 1
Apr 26 11:00:02 plum named[9301]: zone 127.in-addr.arpa/IN: loaded serial 1
Apr 26 11:00:02 plum named[9301]: zone 255.in-addr.arpa/IN: loaded serial 1
Apr 26 11:00:02 plum named[9301]: zone localhost/IN: loaded serial 1
Apr 26 11:00:02 plum named[9301]: running
```

创建或更新 DNS 信息时，您可以使用 **dig** 或 **host** 来测试服务器是否按预期工作。来自 **dig** 的输出中，通常最有用的部分是答案部分（answer section），它给出了名字服务器对您查询的回复：

```bash
$ dig example.com
...
;; ANSWER SECTION:
example.com.          172800   IN   A   192.0.32.10
...
```

上述输出表明，**example.com** 域有一个指向 192.0.32.10 的 A 记录。该记录的 TTL（生存时间）为 172,800 秒（两天），这告诉您该记录可以在缓存中保留多久。您还可以使用 **dig** 配合 `-t` 选项后跟要查询的记录类型（`-t` 同样适用于 **host**）来查询其他类型的记录：

```bash
$ dig -t MX ubuntu.com
...
;; ANSWER SECTION:
ubuntu.com.           3587     IN   MX  10 mx.canonical.com.
...
```

如果您查询一个不存在的域，**dig** 将返回查询中最高级别存在的域权威部分的 SOA 记录：

```bash
$ dig domaindoesnotexist.info
...
;; AUTHORITY SECTION:
info.         900   IN SOA a0.info.afilias-nst.info. noc.afilias-nst.info.
...
```

由于这告诉您最后一个正确查询的域，因此在追踪故障时，这些信息可能很有用。

**TSIGs** 如果使用 TSIGs（第 845 页）的两个服务器无法通信，请确认两台服务器上的时间是否相同。TSIG 认证机制依赖于当前时间。如果两台服务器上的时钟不同步，TSIG 将会失败。请考虑在服务器上配置 *NTP*（第 1163 页）以防止此问题。

## 设置不同类型的 DNS 服务器

本节描述如何设置全功能名字服务器、从服务器和分裂视界服务器。

### 全功能名字服务器

由于本示例中使用的 IP 地址属于 *私有地址空间*（第 1166 页），您可以复制该示例并运行服务器，而不会影响全局 DNS。此外，为防止全局 DNS 受到污染，每个区域都设置了将 **notify** 选项设为 NO。当您构建与互联网集成的名字服务器时，

