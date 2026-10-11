
虽然能够从网络上的任何系统进行查询似乎很方便，但记住遍布整个网络的 IP 地址和子网可能会变得非常痛苦。为了缓解这种情况，`BIND` 允许你创建一个 `ACL` 来控制访问并允许使用“名称”代替 IP 地址和子网。

## 步骤 1. 定义 ACL 指令

```conf
acl "home-lab" { 127.0.0.1; 172.168.1.0/24; };

acl "home-lab" { 127.0.0.1; 172.168.1.2; };

acl "home-lab" { 127.0.0.1; };
```

## 步骤 4. 测试区域功能

```bash
# dig rhel01 example.com axfr

; <<>> DIG9.3.6-P1-RedHat-9.3-6.P1.el5 << @rhel01
example.com axfr
; (server found)
;; global options: printcmd
example.com.             86400 IN SOA
rhel01.example.com.
root.example.com.         2010120711 7200 2419200 3600
example.com.             86400 IN NS
rhel01.example.com.     86400 IN A 172.168.1.1
client02.example.com.     86400 IN A 172.168.1.20
client01.example.com.     86400 IN A 172.168.1.20
rhel02.example.com.     86400 IN A 172.168.1.1
rhel01.example.com.     86400 IN A 172.168.1.1
example.com.             86400 IN SOA
rhel01.example.com.
root.example.com.         2010120711 7200 2419200 3600
;; Query time: 50 msec
;; SERVER: 172.168.1.1#53(172.168.1.1)
;; WHEN: Tue Feb 1 10:21:25 2011
;; XFR: 8 records (messages 1)
```

到目前为止，你一直在查询不同的 DNS 服务器并且它们返回了不同的信息？如果你的服务器之间同步出现问题会发生什么？为了解决这个问题并确保所有 DNS 服务器都使用最新的信息，请增加你的主 DNS 服务器的序列号。增加序列号会强制触发 DNS 记录的复制和同步。

如果你还没有为你的系统设置 FDN（完全限定域名），可以使用 `hostname` 命令来设置。

语法：`hostname [FQDN]`

## 步骤 1. 查询你系统的 FQDN

```bash
# hostname
rhel01
```

## 步骤 2. 如果你想更改它，可以再次使用 `hostname` 命令，并在命令后指定 FQDN

```bash
# hostname rhel01.example.com
```

这会将你的系统主机名更改为包含域名的主机名。如果你对主机名进行了任何更改，应该在继续操作之前重启系统。作为最后一步故障排除步骤，请确保你的客户端在 `/etc/resolv.conf` 文件中位置了正确的信息。正如第 5 章“网络”部分讨论的，该文件被客户端用于查询网络上的其他系统以及用于作为主、备服务器的服务器。

## 步骤 3. 为 Client01 修改这些 DNS 设置

```bash
# cat /etc/resolv.conf
search example.com
nameserver 172.168.1.1
```

## BIND 安全性

`BIND` DNS 服务器提供了许多方法来让你的 DNS 服务器更安全。当你创建 `/etc/named.conf` 文件时，有一个部分可以定义你想要与服务器使用的选项（`options`）。我特意在本章的开头省略了这些选项，以展示通过添加它们所提供的安全性。你可以创建一个更精细的主机和子网列表，允许它们访问并对你的 DNS 服务器执行特定的操作或任务。

你可以使用的第一个选项是 `listen-on`，它定义了服务器将监听的端口和 IP 地址。这限制了可以访问到 DNS 服务器的子网。你还可以使用 `allow-query` 选项来限制哪些子网有权访问 DNS 服务器。第三个选项 `allow-transfer` 定义了允许从主服务器查询数据并传输其区域文件的从服务器。这不应允许来自网络中的任何其他主机执行。

以下是 `/etc/named.conf` 文件的部分：

```conf
/* Global options for the BIND Server */
options
{
  listen-port 53 { 127.0.0.1; 172.168.1.1; };
  allow-query { 127.0.0.1; 172.168.1.0/24; };

  allow-transfer { 172.168.1.2; };

  directory "/var/named"; // the default
  dump-file "data/cache_dump.db"
  statistics-file "data/named_stats.txt"
  memstatistics-file "data/named_mem_stats.txt"
};
```

虽然能够从网络上的任何系统进行查询似乎很方便，但记住遍布整个网络的 IP 地址和子网可能会变得非常痛苦。为了缓解这种情况，`BIND` 允许你创建一个 `ACL` 来控制访问并允许使用“名称”代替 IP 地址和子网。

## 步骤 1. 定义 ACL 指令

```conf
acl "home-lab" { 127.0.0.1; 172.168.1.0/24; };

acl "home-lab" { 127.0.0.1; 172.168.1.2; };

acl "home-lab" { 127.0.0.1; };
```
