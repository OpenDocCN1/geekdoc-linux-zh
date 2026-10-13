
接下来，你为你的域名设置一个从主或从服务器。该过程与本章之前描述的操作相似，并且并不困难。你已经准备好了三个文件，只需稍稍修改 `/etc/named.conf` 文件并添加两个文件即可完成从服务器配置。

在你想要作为从服务器的服务器上，进入 `/etc/named.conf` 文件并添加两个区域，一个用于你服务器的正向查找，另一个用于反向查找。对于正向查找，你需要添加以下内容（在本例中，主服务器名为 `main.tactechology.com`，从服务器为 `p200.tactechology.com`。请务必使用你自己的域名和 IP 地址，而不是示例所示内容）：

```
zone "tactechtechnology.com" {
notify no;
type slave;
file "tactech.com";
masters ( 192.168.1.1 );
}
```

对于反向查找，你添加此部分：

```
zone "1.168.192.in-addr.arpa" {
notify no;
type slave;
file "tac.rev";
masters ( 192.168.1.1 );
}
```

修改 `/etc/named.conf` 文件后，从服务器的配置现在已完成，你可以继续配置主服务器了。

### 配置主主服务器

主服务器上的 `/etc/named.conf` 文件也需要进行修改。假设你已经将此服务器设置为仅缓存服务器，你只需要向 `/etc/named.conf` 中添加以下几行。（此示例使用了本章早些描述的名称；请务必使用你自己的名称和 IP 地址。）

```
zone "tactechtechnology.com" {
notify no;
type master;
file "tactech.com";
}
```

对于反向查找，你添加以下内容：

```
zone "1.168.192.in-addr.arpa" {
notify no;
type master;
file "tac.rev";
}
```

## 检查你的配置

完成主服务器配置后，可以检查配置以确保其正常工作。你可以使用几种工具进行检查。这里我介绍其中两种。运行命令时请务必替换为你的域名和 IP 信息。如果系统设置正确，你应该获得类似的结果。

### host 程序

`host` 允许你查找指定域名的 IP 地址。这只需要远程主机的域名，如下所示，第一行是命令，第二行是命令的输出。

```
[laptop@root]# host tactechnology.com
tactechnology.com has address 12.129.206.112
```

你还可以使用 `-t` 选项和要查找的资源记录类型来搜索资源记录类型。例如，如果你想查找某个域的邮件服务器信息：

```
[terry@named]# host -t mx tactechnology.com
tactechnology.com mail is handled by 10 mail.tactechology.com.
```

### dig 程序

`dig` 用于调试和获取其他有用信息。基本语法为

```
dig (@Server) domain name (type)
```

括号中的项目是可选的。列表 12-4 显示了使用 `dig` 请求学校 DNS 服务器信息的示例。

## 200 第四部分：配置你的企业互联网服务

## 列表 12-4：使用 dig 搜索 IP 地址

```
[@terrynamed]# dig muhlenberg.edu

:: <<>> DIG 9.2.P3 <<>> muhlenberg.edu
:: global options:
:: printcmd
:: Got answer:
:: >>HEADER<< opcode: QUERY, status:NOERROR, id: 50760
:: flags: qr aa rd ra: QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 1

:: QUESTION SECTION:
muhlenberg.edu.                               IN      A

:: ANSWER SECTION:
muhlenberg.edu.                86400 IN      A       192.104.181.5

:: AUTHORITY SECTION:
muhlenberg.edu.                86400 IN      NS      hal.muhlenberg.edu.

:: ADDITIONAL SECTION:
hal.muhlenberg.edu.             86400 IN      A       192.104.181.5

:: Query time: 5 msec
:: SERVER: 192.104.181.5#5953(IN) 2004
:: WHEN: Time Sep 9 14:37:54 2004
:: MSG Size rcvd: 82
```

`dig` 可以通过 `-x` 选项并指定 IP 地址来执行反向查询，如列表 12-5所示。列表中的第一行是在命令行提示符处输入的命令，剩余行是命令的输出内容。

## 列表 12-5：使用 dig 搜索域名

```
[@terrynamed]# -x 192.104.181.5

:: <<>> DIG 9.2.P3 <<>> 192.104.181.5
:: global options:
:: printcmd
:: Got answer:
:: >>HEADER<< opcode: QUERY, status:NOERROR, id: 26961
:: flags: qr aa rd ra: QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

:: QUESTION SECTION:
181.104.192.in-addr.arpa.      IN      PTR

:: ANSWER SECTION:
181.104.192.in-addr.arpa. 86400 IN      PTR     hal.muhlenberg.edu.

:: AUTHORITY SECTION:
181.104.192.in-addr.arpa. 86400 IN      NS      hal.muhlenberg.edu.
181.104.192.in-addr.arpa. 86400 IN      NS      stimpy.nwip.muhlenberg.edu.

:: ADDITIONAL SECTION:

hal.muhlenberg.edu. 86400 IN A 192.104.181.5

stimpy.nwip.muhlenberg.edu. 86400 IN A 192.104.181.207

:: Query time: 6 msec

:: SERVER: 192.104.181.5#5953(192.104.181.5)

:: WHEN: Thu Sep 9 14:39:46 2004

:: MSG SIZE rcvd: 170
```

这两个列表提供了关于完全相同服务器的信息。在列表 12-4 中，我使用域名进行搜索并获取了与域名相关的 IP 地址。在列表 12-5 中，我使用 IP 地址进行搜索，并获取了服务器的主机和域名。

## 第 12 章：配置和管理 DNS 服务器 201

# 第 13 章

## 配置和管理电子邮件服务器

### 本章内容

- 电子邮件的工作原理
- 配置你的邮件服务器
- 维护电子邮件安全

通过计算机，你可以向世界上任何地方的其他计算机用户发送和接收消息。众所熟知的电子邮件（E-mail）是一个非常强大且实用的工具。在本章中，我将向你展示电子邮件是如何工作的，然后展示如何配置你的系统让电子邮件为你服务。

## 电子邮件的工作原理

电子邮件就像通过普通邮寄寄出的信件一样，始于发送者，结束于接收者。在这两个人之间有许多邮递人员确保信件被妥善处理。尽管发送者和接收者可能永远不会见到这些工作人员，但他们的功能对于邮件传递至关重要。电子邮件的工作原理，虽然发送者和接收者之间并没有很多人，但程序执行相同的功能。这些程序使用网络协议来确保消息从发送者到达接收者。在本章中，我将向你展示如何配置电子邮件运行 TCP/IP 协议。

在配置电子邮件客户端或服务器之前，你需要了解电子邮件的工作原理，以及要供用户使用或提供的程序。几个关键组件对于电子邮件的正常运行至关重要。作为一个系统管理员，你的责任是配置以下项目，这些将在章节后部分详细介绍：

- 供用户读写电子邮件的邮件用户代理（MUA）
- 用于传输邮件的邮件传输代理（MTA）
- 用于存储邮件的本地投递代理（LDA）
- 用于传递邮件的 TCP/IP 协议

## 第四部分：配置你的企业级 Linux 互联网服务
