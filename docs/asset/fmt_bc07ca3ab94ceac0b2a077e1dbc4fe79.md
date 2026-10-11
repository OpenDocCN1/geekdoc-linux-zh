
``` 
options {
    check-names response ignore;    // change fail to ignore
    check-names slave ignore;       // change warn to ignore
    check-names master ignore;      // add this line
}

forwarders 15.253.24.10 15.253.32.10 15.253.24.10 15.253.32.10
directory "/etc/named.data"; // running directory for named

/**
 * If there is a firewall between you and nameservers you want
 * to talk to, you might need to uncomment the query-source
 * directive below.  Previous versions of BIND always asked
 * questions using port 53, but BIND 8.1 uses an unprivileged
 * port by default.
 */
// query-source address * port 53;
**/;
```

这里发生的情况是，对于我们没有权限的域名（基本上是 `baseball.hp.com` 以外的任何东西），我们将查询发送给转发器，让它们来处理。如图所示，有两个转发器，每个都列出了两次。这样做的原因是转发器通常很忙，指定两个可以防止查询超时。请务必将 `*/etc/named.data/named.conf*` 复制到 `*/etc/named.conf*`。所有版本的 BIND 默认都会在 `*/etc/*` 中查找启动文件，因此准备好后不要忘记将其复制到 `*/etc*`。

## 9. 在您的域名服务器以及所有指向该域名服务器的客户端上配置 `/etc/resolv.conf` 和 `/etc/nsswitch.conf`：

`/etc/resolv.conf`

```
domain baseball.hp.com
search baseball.hp.com atl.hp.com hp.com rose.hp.com cup.hp.com external.hp.com
nameserver 15.50.73.92 # authoritative name server 4.atl.hp.com
nameserver 15.51.240.8 # non-authoritative cache only servers
```

`/etc/resolv.conf` 非常简单：`domain` 语句标识系统所属的域名；`search` 语句用于在存在多个域名时简化输入。当您发起查询，例如查询 jugshead 时，它会先在 `baseball.hp.com` 中查找 jugshead，然后是 `atl.hp.com`、`rose.hp.com`，最后是 `cup.hp.com`。`/etc/nsswitch.conf` 修改了查找主机和 IP 地址时使用的开关顺序。此信息有四种可能的来源：1) `/etc/hosts`，2) `nis`，3) `nisplus`，4) 和 `dns`。默认情况下，硬编码的顺序是 `dns nis files`。要修改开关顺序，您需要从 `/usr/newconf/etc/nsswitch.hp_defaults` 复制一个新的 `/etc/nsswitch.conf` 文件，并修改 `hosts` 条目：

```
# /etc/nsswitch.hp_defaults:
#
# An example file that could be copied over to /etc/nsswitch.conf; it
# uses NIS (YP) in conjunction with files.
#
passwd: compat
group: compat

hosts: files [NOTFOUND=return] dns
networks: nis [NOTFOUND=return] files
protocols: nis [NOTFOUND=return] files
rpc: nis [NOTFOUND=return] files
publickey: nis [NOTFOUND=return] files
netgroup: nis [NOTFOUND=return] files
autmount: files nis
```

别名：`files nis`

服务：`nis [NOTFOUND=return] files`

如您所见，`*hosts*` 行已被修改，以便我们首先查询 `/etc/hosts` 文件，如果查询不成功，则继续转向 `*dns*`。更改开关顺序的方式有很多种，还有很多其他方法可能会把事情搞乱。更改开关顺序时请谨慎行事，并查阅 `*switch*` 的手册页以获取更多相关信息。

## 10. 按如下步骤启动 DNS 名称服务器进程：

```
# /usr/sbin/named
# ps -eaf|grep named

root 8074 1 0 08:42 0:08 ? 0:00 /usr/sbin/named <--- 检查以确保它正在运行..
root 8077 8072 2 08:42 0:00 grep named
```

启动名称服务器后，您可以使用 `*sig_named*` 执行各种功能。修改任何 `*db*` 文件或 `/etc/named.boot` 后，您需要告知 `named` 刷新其数据库。您可以使用以下两个命令中的任意一个来实现：

```
# sig_named restart
# kill -HUP /var/run/named.pid
```

这将重新加载数据库，您可以通过查看 `/var/adm/syslog/syslog.log` 文件的末尾来验证，如下所示：

```
Oct 12 08:49:13 m3107ced named[8074]: primary zone "0.0.127.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "baseball.hp.com" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "1.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "2.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "3.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "1.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "2.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "3.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: Ready to answer queries.
```

如您所见，`named` 加载了我们的每个数据库（或区域），并准备就绪以回答查询。

## 11. 测试通过名称和 IP 地址进行的查询。

```
# nslookup atlantabraves
Using /etc/hosts on: wt ec712-rtr
Looking up FILES
Trying DNS
Name: atlantabraves.baseball.hp.com
Address: 10.1.1.1
```

```
# nslookup 10.1.1.1
Using /etc/hosts on: wt ec712-rtr
Looking up FILES
Trying DNS
Name: atlantabraves.baseball.hp.com
Address: 10.1.1.1
```

通过名称和 IP 地址查找 `atlantabraves` 均成功，通常此时我们就完成了。

我们总是检查 `/var/adm/syslog/syslog.log` 以查找来自 `named` 的消息。`named` 记录了很多看似不重要的聊天内容，但至少值得稍作浏览。

### 关于从（二级）名称服务器

一旦您创建了主（一级）DNS 服务器，最艰巨的工作就完成了。创建从服务器和仅缓存服务器很简单。让我们一步步 walkthrough 这个过程：
