
# 第 VII 部分：网络管理

| 记录 | 类型 | 值 |
| :--- | :--- | :--- |
| ftp | CNAME | turtlemytrek.com |
| www | A | 192.168.0.1 |
| rabbit | A | 192.168.0.2 |
| lizard | A | 192.168.0.3 |
| localhost | HINFO | |
| | A | 127.0.0.1 |

前两行是关于该服务器的注释。注意前两行的 `IN`，表示这些是互联网记录。`SOA` 记录以 `@` 开头；`@` 代表域名。任何主机或域名……在本示例中，`rabbit` 没有点，所以它会自动扩展为 `mytrek.com`。`lizard` 也是如此。这些读取为 `rabbit.mytrek.com` 和 `lizard.mytrek.com`。

## 名称服务器记录

下一条记录指定了该区域的名称服务器。在这里，它是 `mytrek.com.`。注意此记录的注释是空的。如果名称留空，资源记录将继承上一个记录的名称。在这种情况下，`NS` 记录继承了 `SOA` 记录中 `@` 的值。这是区域的域名，`NS` 记录指定 `mytrek.com` 为该区域的名称服务器。

| IN | NS | turtlemytrek.com. |

域名是继承的。该条目的内容读取如下：域名末尾的点：

| mytrek.com. | IN | turtlemytrek.com |

## 地址记录

后续记录为域名本身设置地址。这通常与名称服务器相同，在此处为 `192.168.0.1`（`mytrek.com` 的 IP 地址）。这允许用户引用域名本身，而不是其中的特定主机。随后跟一个邮件交换记录，引导从域到名称服务器的路由。

| IN | A | 192.168.0.1 |

域名是继承的。该条目的内容读取如下：

| mytrek.com. | IN | A | 192.168.0.1 |

## 邮件交换记录

后续记录是邮件交换 (`MX`) 记录，列出 `mytrek.mytrek.com` 和 `fast.mytrek.com` 为该区域的邮件服务器。一个主机可以有多个邮件交换记录。邮件可以通过存在的多个主机进行传输

可以进行路由。这些可以列在邮件交换记录（`MX`记录）中，你可以为它们设置优先级排序（数字越小，优先级越高）。例如，如果 `turtle.mytrek.com` 无法访问，其邮件将通过 `rabbit.mytrek.com` 路由，该主机被设置为也处理 `mytrek.com` 域名的邮件：

```
IN MX 100    turtle.mytrek.com.

IN MX 150    rabbit.mytrek.com.
```

再次，域名是继承的。这些条目可以理解为：

```
mytrek.com IN 100 turtle.mytrek.com.

mytrek.com IN 150 rabbit.mytrek.com.
```

**带有主机名的地址记录**
接下来的资源记录是一个地址记录（`A` 记录），它将 IP 地址与完全限定域名 `mytrek.com` 关联。资源记录名称仅包含 `turtle` 且末尾没有点，因此它会自动扩展为 `turtle.mytrek.com`。该记录提供了 `turtle.mytrek.com` 可以映射的 IP 地址。

```
turtle IN A 192.168.0.1
```

**继承名称**
紧随其后的是几条名称为空的记录。它们继承自前一个完整记录的名称——在本例中为 `turtle.mytrek.com`。实际上这些记录也适用于该主机。使用空白名称是列出同一主机资源记录的简单方法（注意这里发生了明显的缩进）。第一条记录是一条信息记录，提供了该机器的硬件和操作系统。

```
IN HINFO PC-686 LINUX
```

**别名记录**
如果你使用同一台机器来运行多个服务器（例如 Web、FTP 和 Gopher 服务器），你可以为这些服务器分配别名，以便用户更方便地访问。与其使用实际域名（如 `turtle.mytrek.com`）来访问运行在其上的 Web 服务器，用户可能会发现使用以下内容更方便：对于 Web 服务器，使用 `www.mytrek.com`；对于 Gopher 服务器，使用 `gopher.mytrek.com`；在 DNS 中，你可以通过别名记录（alias records）实现这种功能。在区域文件中，`ftp.mytrek.com` 是同一台机器的 `CNAME` 别名记录。这些条目都没有以点结尾，因此它们会自动追加域名 `mytrek.com`。`www.mytrek.com`、`ftp.mytrek.com` 和 `gopher.mytrek.com` 都是 `turtle.mytrek.com` 的别名。输入这些 URL 的用户会自动访问 `mytrek.com` 机器上的相应服务器。

**环回记录**
随后列出了该区域内两个机器的地址和邮件交换记录：`rabbit.mytrek.com` 和 `lizard.mytrek.com`。你可以为这些条目添加 `HINFO`、`TXT`、`MINFO` 或别名记录。`localhost` 的文件条目是一个特殊的环回接口，允许系统对自身进行地址。

## 第七部分：网络管理

### IPv6 区域文件示例

这是一个使用 IPv6 地址的相同区域文件。地址是站点本地的（`FEC0`），而不是全局（3），提供了私有网络地址。环回设备由 IPv6 地址 `::1` 表示。IPv6 地址用于：

```
; turtle.mytrek.com 的权威数据，IPv6 版本

; TTL 1d

@ IN SOA turtle.mytrek.com. 序列号

    93071200 10800 ; Refresh 3 小时

    3600 ; Retry 1 小时

    3600000 ; Expire 1000 小时

    86400 ; Minimum 24 小时

IN NS turtle.mytrek.com.

IN A6 FEC0:8:8:200:417A

IN MX 10 turtle.mytrek.com.

IN MX 15 rabbit.mytrek.com.

turtle IN A6 FEC0:8:8:200:417A

IN HINFO PC-686 LINUX

gopher IN CNAME turtle.mytrek.com.

ftp IN CNAME turtle.mytrek.com.

www IN A6 FEC0:8:8:200:417A
```

```
rabbit IN A6 FEC0::FDC:BA98:7654:3210

lizard IN A6 FEC0::E0:18F7:3466:7D

IN HINFO MAC MACOS

localhost IN A6 ::1
```

## 反向映射

反向映射通过反向映射文件启用。反向映射文件将完全限定域名映射到 IP 地址。反向查找能力不是必须的，但有了它很方便。通过反向映射，用户访问远程主机时，可以使用其域名地址来识别自己的主机，而不是 IP 地址。文件名可以是任何你喜欢的名称。在大多数当前的发行版中，它是该区域的地址（区域 IP 地址的网络部分）。例如，IP 地址为 `192.168.0.1` 的区域的反向映射文件是 `192.168.0.0`。其完整路径将类似于 `/var/named/192.168.0`。在某些使用 `BIND` 实现的系统中，反向映射文件名可能由区域文件的根节点名称加上 `.rev` 后缀组成。例如，如果区域文件名为 `mytrek.com`，则反向映射文件将命名为 `mytrek.rev`。

## IPv4 IN-ADDR.ARPA 反向映射格式

在 IPv4 中，`named.conf` 文件中用于反向映射的区域条目使用特殊的域名，由反向 IP 地址加上 `IN-ADDR.ARPA` 后缀组成。反向 IP 地址成为反向映射文件中 `@` 符号所引用的域名。例如，IP 地址为 `192.168.43` 的区域的反向映射名称为 `43.168.192-IN-ADDR.ARPA`。在以下示例中，地址 `192.168.0` 的反向域名为 `0.168.192-IN-ADDR.ARPA`：

```
zone "192.168.192-IN-ADDR.ARPA" in {

type master;

  file "192.168.0";

}
```
