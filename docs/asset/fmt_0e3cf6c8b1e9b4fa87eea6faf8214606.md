
# forwarders 记录包含了应转发查询的服务器列表。

# 启用此行并修改你的提供商的 IP 地址。

# 最可以列出三个服务器。

```
forwarders { 192.0.2.1; 192.0.2.1; };
```

# 启用下一项以优先使用在 `/named.conf` 第 35-137 行中声明的服务器 

# 810 第 14 章：配置 Linux 网络服务

FIGURE 14-13

创建 nebo-tech.com 区域

![](img/8156850acb7240fabbc4667ef20f2fa8_851_0.png)

表 14-4 定义了 `zone` 指令的组件。在图 14-11 中，你可以看到 `named.conf` 中还定义了三个区域。当安装 BIND 包时，这些区域会自动创建。第一个区域是 `.`，并配置为提示文件（hint file）。该区域的记录指向互联网上的根级服务器。当 `named` 接收到解析非权威区域的主机名请求时，就会使用该区域。这些根级服务器的 IP 地址包含在图 14-8 所示的 `root.hint` 文件中。安装 BIND 包时，`root.hint` 文件会自动复制到 `/var/lib/named`。

| 表 14-4 | 组件 | 描述 |
| --- | --- | --- |
| 在 `named.conf` 中定义区域 | `zone_name` | `zone_name` 位于 `zone` 指令之后。区域名用引号括围。在图 14-13 中，已创建了 nebo-tech.com 区域。 |
| | `name_space` | `name_space` 位于区域名之后。在图 14-13 中，使用了互联网命名空间 (`in`)。在实现 DNS 服务器时，极少遇到其他命名空间。 |
| | `zone_type` | `zone_type` 标识服务器是该区域的主服务器还是从服务器。在图 14-13 中，DNS 服务器将是 nebo-tech.com 区域的主服务器。 |
| | `zone_filename` | `zone_filename` 指定区域数据存储的位置。文件名用引号括围。在图 14-13 中，nebo-tech.com 区域保存在 `master` 子目录下。 |

## 在 Linux 上配置 DNS 服务器

`named.conf` 中定义的下一个区域是 `localhost`。该区域仅包含一条记录，将 `localhost` 映射到 IP 地址 `127.0.0.1`。`named.conf` 中定义的区域是 `1.0.0.127.in-addr.arpa`。这个名字听起来可能有点奇怪，但并不是。这个反向区域将 IP 地址 `127.0.0.1` 映射到 `localhost`。

正如你所注意到的，这三个默认区域并没有像 nebo-tech.com 区域那样定义真实的区域。你可能会惊讶于可以在配置区域的情况下配置强大的 DNS 服务器。在这种配置中，`named` 进程仅作为缓存。记住，当 DNS 服务器被要求解析它不权威的名字时，它会查询根级服务器。DNS 服务器将使用根级服务器提供的信息来定位主机的权威 DNS 服务器。当主机解析完成后，DNS 服务器会将该信息存储在缓存中。下一次收到请求时，它只需从缓存中提取信息。

这种配置适用于你没有域名且只需让用户访问互联网资源的情况。另一方面，如果你想为组织的区域设置 DNS 服务器，你需要创建自己的区域文件并配置 `named` 使用它们。要做到这一点，首先需要编辑图 14-13 所示的 `/etc/named.conf`。接下来的工作是为区域创建一个区域文件。注意图 14-13，我指定了文件名 `master/nebo-tech.com`。由于 `/etc/named.conf` 中的 `directory` 参数指定工作目录为 `/var/lib/named`，因此你的区域文件将是 `/var/lib/named/master/nebo-tech.com`。

保存 `/etc/named.conf` 后，下一步是创建指定的区域文件并添加相应的 IP 信息。这里情况变得有些复杂。图 14-14 显示了我为 nebo-tech.com 区域创建的基础区域文件。在这个区域中，有主机记录：请在表 14-5 的详细区域中查看区域的每个元素。

除了正向区域（lookup zone），你还可以创建反向区域（lookup zone）。反向区域的工作方式与正向区域相反。反向区域不是将主机名解析为 IP 地址，而是将 IP 地址解析为主机名。在你的 `named` 进程执行此类查询之前，你需要为你的正向区域创建一个反向区域。图 14-15 显示了 nebo-tech.com 区域的反向区域示例。

# 812 第 14 章：配置网络服务

图 14-14

一个示例区域文件

![](img/8156850acb7240fabbc4667ef20f2fa8_853_0.png)

表 14-5

区域文件组件

| 区域文件组件 | 描述 |
| --- | --- |
| `$TTL` | 代表生存时间（time to live）。此值指定了每个记录的默认生存时间。如果记录有显式的时间值，则其优先级指定的 `TTL` 值。如果没有单位，则假设该值指秒。图 14-14 中的示例显示 `TTL` 值为二天。 |
| `IN` | 指定该区域使用互联网命名空间。 |
| `SOA` | 代表权威性（authority）。`SOA` 记录有特殊用途，就像文件中其他记录一样。然而，`SOA` 记录必须紧跟在 `$TTL` 参数之后。`SOA` 记录标识：<br>- 作为该区域权威服务器的 DNS 服务器。在图 14-14 中，`linux1.nebo-tech.com` 被标识为 nebo-tech.com 的权威 DNS 服务器。记得使用末尾的点！<br>- 维护该区域的系统管理员电子邮件。在示例中，它是 `root@linux1.nebo-tech.com`。<br>- 区域序列号，从服务器使用该号来判断是否应该更新数据库。你可以使用任何值；但通常做法是使用文件的创建日期并补零。在图 14-14 中，区域文件创建于 2007 年 2 月 8 日。如果你更新了区域，应该将数字的最后一位加 1（这就是为什么在末尾添加零）。这告诉 DNS 服务器区域文件已发生变化，它们需要从主服务器更新数据库。<br>- 从服务器从主服务器更新数据库的间隔时间（刷新）。在图 14-14 中，刷新间隔被设置为三小时。<br>- 从服务器在尝试从主服务器更新数据库失败时，在放弃前应该尝试的次数（重试）。在图 14-14 中，这设置为一小时。<br>- 从服务器上的数据在过期前允许的时间（过期）。在图 14-14 中，这设置为一天。<br>- 从服务器在缓存中存储失败的主机解析请求的时间（最小）。在图 14-14 中，这设置为一天。 | |

# 在 Linux 上配置 DNS 服务器

表 14-5 区域文件组件（续）

| 区域文件组件 | 描述 |
|---|---|
| `SOA` 记录之后是用于名称解析的主机记录。主机记录的通用语法为：`host_name namespace record_type IP_address` 或 `host_name` | 这里是这些参数的说明：`host_name` 指定系统的主机名。`namespace` 指定用于记录的命名空间（通常为 `IN`）。`record_type` 指定 DNS 记录类型。使用了以下类型：`NS` 将主机名映射到 IP 地址。`CNAME` 记录是一个别名。它将别名映射到区域内的另一个主机名。`MX` 代表邮件服务器。它将主机名映射到区域内的另一个主机名。`IP_address or host_name` 指定你要将主机名映射到的 IP 地址或主机名。 |

注意图 14-15，`TTL` 参数和 `SOA` 记录与我们之前审查过的正向查找区域几乎相同。找到图 14-15 中的 `NS` 记录。注意所使用的奇特区域名称。在 `nebo.com` 中，区域名称是 `1.168.92.in-addr.arpa`。反向查找区域名称按照以下方式构造：`reversed_network_address.in-addr.arpa`。

![](img/8156850acb7240fabbc4667ef20f2fa8_854_0.png)

# 814 第 14 章：配置 Linux 网络服务

例如，如图 14-15 所示，区域内主机的网络地址为 `192.168.1.0`。因此，区域名称为 `1.168.12.in-addr.arpa`。相应的，区域内的主机通过其 IP 地址的最后一个字节进行引用，例如：

```
10 IN PTR linux1.nebo-tech.com
```

此记录将主机 `10.168.192-in-addr.arpa` (192.168.1.10) 发布到 `linux1.nebo-tech.com`。配置了反向查找区域后，你可以使用 DNS 服务器反向将 IP 地址解析为域名。

定义区域后，你现在可以使用其脚本启动守护进程。你还应该配置工作站使用你的新 DNS 服务器来解析主机。在 Linux 系统上，你需要编辑 `/etc/hosts` 或 `/etc/resol.conf` 文件，并添加运行 `named` 守护进程的系统 IP 地址。在 Windows 系统上，你使用网络属性指定 DNS 服务器。

你必须在系统防火墙中打开 53 端口，以便客户端能够向你的 DNS 服务器发送请求。

完成后，你可以使用各种 Linux 命令行工具来测试你的系统。接下来让我们讨论如何操作。

# 使用 dig 和 nslookup

Linux 为你提供了几个工具用来向 `named` 守护进程发送名称解析请求。第一个是 `nslookup` 实用。要用它发送名称解析请求，请完成以下操作：

1. 在 shell 提示符处输入 `nslookup`。
2. 在 `>` 提示符处输入你想让 DNS 服务器解析的主机名或 IP 地址。
3. 你系统上的 `named` 守护进程应响应请求的映射。例如，在图 14-16 所示，linux1 主机已发送了

![](img/8156850acb7240fabbc4667ef20f2fa8_855_0.png)

# 在 Linux 上配置 DNS 服务器

对于位于端口 53 的 `127.0.0.1`（本地）DNS 服务器的解析。本地主机上的 `named` 守护进程返回了主机 `192.168.1.10` 的 IP 地址。

4. 完成后，在 `>` 提示符处输入 `exit`。

另一个可以使用的工具是 `dig`：它的用法与 `nslookup` 类似，但提供了更多关于请求的主机名或 IP 地址的信息。在图 14-17 中，在 shell 提示符处执行了 `dig linux1.nebo-tech.com`。注意 `dig` 的输出比 `nslookup` 显示的详细得多。它返回了与 `ANSWER` 部分主机相关的 IP 地址，还列出了 `AUTHORITY` 部分的服务器。

现在你已经了解了 DNS 的工作原理，这里有一些场景和答案。

# 场景 & 解决方案

你的工作站向你组织的 DNS 服务器发送 `www.nebo-tech.com` 名称解析请求。该服务器不是 `com` 区域的权威服务器。你的 DNS 服务器将如何解析此域名？

你的 DNS 服务器向根服务器发送 `.com` 请求。根服务器向你的 DNS 服务器返回了 `.com` 区域权威服务器的 IP 地址。然后你的 DNS 服务器向该服务器发送 `www` 请求。该权威服务器向你的 DNS 服务器返回了相应的 IP 地址。你的 DNS 服务器将此地址返回给工作站，工作站使用该 IP 地址。

你正在为网络配置 DNS 服务器。你的网络地址是 `192.168.1.0`。你的反向查找区域将是什么？

你的反向查找区域将是 `1.168.92.in-addr.arpa`。

# 16 第 14 章：配置 Linux 网络服务

图 14-17

使用 dig

```
linux1@hostname ~ # Shell

linux1@hostname ~ # dig linux1.nebo-tech.com

DIG 9.3 >> linux1.nebo-tech.com

options: print

got answer:

HEADER: QUERY, status: NOERROR, id: 4287

flags: aa QUERY 1, ANSWER: 1, OPTIONAL: 0

QUESTION SECTION:

linux1.nebo-tech.com IN A

ANSWER SECTION:

nebo-tech.com. 7200 IN A 192.168.1.10

AUTHORITY SECTION:

nebo-tech.com. 7200 IN NS linux1.nebo-tech.com.

QUERY time: 0 msec

SERVER: 127.0.0.1:53

WHEN: Thu Feb 8 15:38:12 2007

MSG SIZE recvd: 68
```

让我们在下面的练习创建一个 DNS 服务器。

# 练习 14-2

![](img/8156850acb7240fabbc4667ef20f2fa8_857_0.png)

# 配置 DNS 服务器

在此练习中，你将在 Linux 系统上安装并配置 `named` 守护进程。此练习假设你的系统中已安装并配置了以太网。完成以下操作：

1. 启动你的 Linux 系统并以标准用户登录。如果你使用了第 3 章的练习进行安装，可以使用 `tux` 登录，密码为 `linux273`。
2. 打开终端会。
3. 输入 `su -` 后跟 root 用户密码切换到 root 用户。
4. 使用 `rpm` 工具在系统中安装以下包：
   - `bind`
   - `bind-libs`
   - `bind-chroot`
   - `bind-utils`

# 在 Linux 上配置 DNS 服务器

5. 使用文本编辑器打开 `/etc/named.conf`。
6. 添加以下行：

```
zone "my-zone.com" {

    file "master/my-zone.com";

    type master;

}
```

7. 将更改保存到 `/etc/named.conf` 文件。
8. 使用文本编辑器打开新文件 `/var/lib/named/master/my-zone.com`。
9. 在你的 `my-zone.com` 文件中添加以下行：

```
$TTL 2d

@ IN SOA

your_hostname.my-zone.com. root.your_hostname.my-zone.com. (

2007020800 ; serial

3h ; refresh

1h ; retry

1w ; expiry

1d ; minimum
```

```
my-zone.com. IN NS your_hostname.my-zone.com.

your_host IN A your_host_IP_address
```

10. 将更改保存到文件。
11. 使用文本编辑器打开 `/etc/resolve.conf`。
12. 在文件中添加以下行：

```
domain my-zone.com

nameserver your_host_IP_address
```

13. 如果你的系统运行着主机防火墙，请为 IP 端口 53 创建异常。
14. 在 shell 提示符处，使用 `/etc/init.d` 或 `/etc/rc.d/init.d` 中的初始化脚本启动 `named` 守护进程。
15. 使用 `dig` 命令解析你的系统主机名。验证是否返回了正确的 IP 地址。
16. 使用 `dig` 解析互联网上的域名，例如 `yahoo.com`。

# 在 Linux 819 上配置 Apache Web 服务器

# 图 14-18

```
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.0 Transitional//">

<html

<head>

<meta http-content="text/html; charset=iso-8859-1">

<meta http-type="text/html">

<title>HTML Sample Web page</title>

</head>

<body>

<p>This is a sample web page. It uses HTML to format the text and layout

of the document. A web page can include elements such as:<br>

<ull>

<li>Text</li>

<li>Graphics</li>

<li>Hyperlinks</li>

<li>Forms</li>

</ull>

</p>

</body>

</html>
```
