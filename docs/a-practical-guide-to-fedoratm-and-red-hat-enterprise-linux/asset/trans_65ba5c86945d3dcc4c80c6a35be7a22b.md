

在上一条命令中，将 `keyname` 替换为一个独特但具有意义的字符串。此命令会创建一个文件，其名称类似于字符串 `Kkeyname.+157+47586.private`，其中 `keyname` 被替换为密钥的名称，`+157` 指示所使用的算法，而 `+47586` 是密钥的哈希值。如果你再次运行相同的命令，哈希部分将会不同。

密钥文件不会直接使用。使用 `cat` 命令并传入私有文件名称作为参数，以显示你在下一步中所需的算法和密钥信息：

```bash
$ cat Kkeyname.+157+47586.private
Private-key-format: v1.3
Algorithm: 157 (HMAC_MD5)
Key: uNPDOuqQwR7Fvo/zFyjKqKbQhCTd6Prm... 
...
```

## 使用共享密钥

下一步是告知名称服务器有关共享密钥的信息，方法是在两台服务器的 `/etc/named.conf` 文件中插入以下代码。此代码是 `named.conf` 中的顶级子句；请将其插入在 `Options` 子句之后：

```dns
key  keyname  {
    algorithm  "hmac-md5";
    secret  "uNPDOuqQwR7Fvo/zFyjKqKbQhCTd6Prm...";
};
```

`keyname` 是你创建的密钥的名称。`algorithm` 是上述 `cat` 输出中括号内出现的字符串。`secret` 是 `cat` 输出中 `Key:` 后面的字符串。你必须用双引号将每个字符串括起来。复制密钥时要小心；虽然它很长，但你不能将其分成多行。

由于密钥名称是唯一的，你可以将任意数量的 `Key` 子句插入到 `named.conf` 中。为了保持密钥的机密性，请确保除 `root` 外的其他用户无法读取它： 要么赋予 `named.conf` 权限，使得除了 `root` 外没有其他人可以访问它，要么将密钥放入只有 `root` 可以读取的文件中，并使用 `include` 语句将其纳入 `named.conf`。

一旦两台服务器都知道该密钥，请使用 `named.conf` 中的 `server` 语句来告知它们何时使用该密钥：

```dns
server  1.2.3.4  {
# 1.2.3.4 是使用此密钥的另一台服务器的 IP 地址
    keys  {
        "keyname";
    };
};
```

每台服务器都必须有一个 Server 子句，每个子句包含另一台服务器的 IP 地址。只有在首先使用共享密钥相互验证后，服务器之间才会相互通信。

## 在 chroot 监狱中运行 BIND

为了增加安全性，你可以在 chroot 监狱中运行 BIND。有关 chroot 监狱的安全优势及设置方式的信息，请参阅第 487 页。另请参阅第 865 页关于 SELinux 的说明以及 named 手册页，以了解有关 BIND、SELinux 和 chroot 监狱的信息。当你启动 named-chroot 服务（第 865 页；named-chroot 包的一部分）时，它会设置 BIND 在 chroot 监狱中运行，创建一个名为 `/var/named/chroot` 的目录，该目录作为所有 BIND 文件的根目录（`/`）的替代。

当 named-chroot 和 named 正在运行时，所有控制 BIND 的文件都挂载在两个位置（可用）。例如，`/var/named` 目录也挂载在 `/var/named/chroot/var/named`：

```bash
# ls -li /var/named /var/named/chroot/var/named

/var/named:
2102980 drwxr-x--- 7 root  named  4096  06-28  16:08 chroot
2102872 drwxrwx--- 2 named named  4096  06-28  16:17 data
2102968 drwxrwx--- 2 named named  4096  06-28  16:22 dynamic
2102971 -rw-r---- 1 root  named  2076  01-28  06:38 named.ca
2102972 -rw-r---- 1 root  named   152 2009-12-15 named.empty
2102973 -rw-r---- 1 root  named   152 2007-06-21 named.localhost
2102974 -rw-r---- 1 root  named   168 2009-12-15 named.loopback
2102975 drwxrwx--- 2 named named  4096  05-05  01:31 slaves

/var/named/chroot/var/named:
2102980 drwxr-x--- 7 root  named  4096  06-28  16:08 chroot
2102872 drwxrwx--- 2 named named  4096  06-28  16:17 data
2102968 drwxrwx--- 2 named named  4096  06-28  16:22 dynamic
2102971 -rw-r---- 1 root  named  2076  01-28  06:38 named.ca
2102972 -rw-r---- 1 root  named   152 2009-12-15 named.empty
2102973 -rw-r---- 1 root  named   152 2007-06-21 named.localhost
2102974 -rw-r---- 1 root  named   168 2009-12-15 named.loopback
2102975 drwxrwx--- 2 named named  4096  05-05  01:31 slaves
```

同样，`/etc/named.conf` 也挂载在 `/var/named/chroot/etc/named.conf`：

```bash
# ls -li /etc/named.conf /var/named/chroot/etc/named.conf
1969014 -rw-r----- 1 root named 1540 05-03 03:26 /etc/named.conf
1969014 -rw-r----- 1 root named 1540 05-03 03:26 /var/named/chroot/etc/named.conf
```

当你停止 named-chroot 服务时，它会取消挂载文件的第二个副本：

```bash
# systemctl stop named-chroot.service
# ls -li /etc/named.conf /var/named/chroot/etc/named.conf
ls: cannot access /var/named/chroot/etc/named.conf: No such file or directory
1969014 -rw-r----- 1 root named 1540 05-03 03:26 /etc/named.conf
```

**可选** *named-chroot* 服务使用 *mount*—*bind* 选项将目录层次结构的一部分（可以是单个文件）重新挂载到另一个位置。此选项允许你执行硬链接无法执行的操作：从文件系统中的另一个位置访问目录层次结构。它还绕过了符号链接的一些限制，包括权限问题。然而，它并不创建指向文件的另一个链接——参见前面 *named.conf* 的列表。每个文件的链接计数（第 192 页）为 1。有关更多信息，请参阅 *mount* 手册页。

## 故障排除

当你启动 DNS 缓存时，`/var/log/messages` 文件包含类似于以下内容的行：

```log
# cat /var/log/messages
...
17:00:51 guava systemd[1]: Starting Berkeley Internet Name Domain (DNS)...
17:00:52 guava named-checkconf[2003]: zone localhost.localdomain/IN: loaded serial 0
17:00:52 guava named-checkconf[2003]: zone localhost/IN: loaded serial 0
17:00:52 guava named-checkconf[2003]: zone 1.0.0.127.in-addr.arpa/IN: loaded serial 0
17:00:52 guava named-checkconf[2003]: zone 0.in-addr.arpa/IN: loaded serial 0
17:00:52 guava named[2008]: starting BIND 9.9.3-r1.156.01-P1-8dHat-... P1.fc19 -u named
17:00:52 guava named[2008]: adjusted limit on open files from 4096 to 1048576
17:00:52 guava named[2008]: found 1 CPU, using 1 worker thread
17:00:52 guava named[2008]: using 1 UDP listener per interface
17:00:52 guava named[2008]: using up to 4096 sockets
17:00:52 guava named[2008]: loading configuration from '/etc/named.conf'
17:00:52 guava named[2008]: reading built-in trusted keys from '/etc/named.iscdlv.key'
17:00:52 guava named[2008]: using default UDP/IPv4 port range: [1024, 65535]
17:00:52 guava named[2008]: using default UDP/IPv6 port range: [1024, 65535]
17:00:52 guava named[2008]: listening on UDP IPv4 interface lo, 127.0.0.1#53
17:00:52 guava named[2008]: listening on IPv6 interface lo, ::1#53
17:00:52 guava named[2008]: generating session key for dynamic DNS
17:00:52 guava named[2008]: sizing zone task pool based on 6 zones
17:00:52 guava named[2008]: using built-in DLV key for view '_default'
17:00:52 guava named[2008]: automatic empty zone: 125.100.IN-ADDR.ARPA
17:00:52 guava named[2008]: automatic empty zone: 126.100.IN-ADDR.ARPA
17:00:52 guava named[2008]: automatic empty zone: 255.255.255.255.IN-ADDR.ARPA
17:00:52 guava named[2008]: automatic empty zone: D-F.IP6.ARPA
17:00:52 guava named[2008]: automatic empty zone: 8-E-F.IP6.ARPA
17:00:52 guava named[2008]: automatic empty zone: 9.E.F.IP6.ARPA
17:00:52 guava named[2008]: automatic empty zone: A.E.F.IP6.ARPA
17:00:52 guava named[2008]: automatic empty zone: B.E.F.IP6.ARPA
17:00:52 guava named[2008]: automatic empty zone: 8.B.D.0.1.0.0.2.IP6.ARPA
17:00:52 guava named[2008]: command channel listening on ::1#953
17:00:52 guava named[2008]: command channel listening on 127.0.0.1#953
17:00:52 guava named[2008]: managed-keys-zone: journal is out of date: removing journal
17:00:52 guava named[2008]: zone managed-keys-zone: loaded serial 3
17:00:52 guava named[2008]: zone 0.in-addr.arpa/IN: loaded serial 0
17:00:52 guava named[2008]: zone 1.0.0.127.in-addr.arpa/IN: loaded serial 0
17:00:52 guava named[2008]: zone localhost.localdomain/IN: loaded serial 0
```

