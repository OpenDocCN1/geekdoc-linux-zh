
### Zone 语句选项

在可以在`zone`语句中指定的各种选项中，`type`是一个重要的选项。使用此选项，您可以指定要创建的区域类型，以及该区域是`master`区域还是`slave`区域。

其他一些区域选项包括`allow-query`、`allow-transfer`、`allow-update`、`masters`、`file`和`notify`。

### 区域类别类型

在`zone`语句中，区域名称后面跟着区域类别，您可以在此指定要创建的区域类别类型。`zone`语句中可以指定三种区域类别类型。

| 区域类别类型 | 描述 |
| --- | --- |
| `IN` | 代表互联网。它表示该区域用于互联网服务。`IN`是默认的区域类别类型。 |
| `HS` | 代表 Hesiod，一种名称解析协议。它表示该区域使用 Hesiod 来共享用户、组和打印机等信息。这些信息存储在数据库中，偶尔可能会发生变更。 |
| `CH` | 代表 ChaosNet。它表示该区域使用 ChaosNet 协议，该协议专门用于局域网。该协议的区域信息可以使用`CHAOS`类指定。此外，`BIND`使用 ChaosNet 来获取`BIND`的版本号。 |

指定区域类别是可选的，如果未指定，则假设`zone`语句使用`IN`。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_547_0.png)

## `rndc` 工具

`rndc`工具是一个`BIND`工具，允许从本地或远程主机对`named`守护进程进行命令行管理。此工具通过 TCP 连接进行通信，并发送使用数字签名进行身份验证的命令。它还读取`/etc/rndc.conf`配置文件，以获取如何联系名称服务器的设置，并决定要使用的算法和密钥。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_547_1.png)

图 12-39：`rndc`工具的实现。

`rndc`工具可以与各种命令一起使用。

| 命令 | 描述 |
| --- | --- |
| `reload` | 重新加载配置文件和区域。 |
| `reload zone [class]` | 重新加载指定的区域。 |
| `stats` | 将服务器统计信息写入统计文件。 |
| `status` | 在屏幕上显示服务器状态。 |
| `stop` | 将区域的待处理更新保存到主文件中，然后停止服务器。 |
| `halt` | 停止服务器而不更新更改。 |
| `flush` | 清除所有服务器缓存。 |
| `restart` | 重新启动服务器。 |

`rndc`工具有许多选项。下表列出了其中一些常用的选项。

| 选项 | 功能 |
| --- | --- |
| `-b source address` | 指定建立与服务器连接的源地址。通过提供多个实例，您可以同时指定 IPv4 和 IPv6 地址。 |
| `-c config file` | 指定`rndc`必须使用的配置文件，而不是读取默认的`/etc/rndc.conf`文件。 |

## 选项

| 选项 | 功能 |
|---|---|
| `-k 密钥文件` | 指定`rndc`必须使用的密钥文件，以替代默认的`/etc/rndc.key`密钥。`rndc`仅在配置文件不可用时，才使用默认密钥来对发送到服务器的命令进行身份验证。 |
| `-s 服务器` | 指定响应查询的服务器地址，以替代在`/etc/rndc.conf`配置文件中指定的默认服务器。 |
| `-P 端口` | 指定发送命令所用的 TCP 端口。 |
| `-V` | 指定日志消息应为详细级别。 |
| `-Y 密钥ID` | 指定要使用的密钥 ID，以替代在`/etc/rndc.conf`文件中指定的默认密钥。密钥 ID 用于验证控制消息。 |

## 语法

`rndc`实用程序的语法为`rndc [rndc 选项] [rndc 命令]`。

## `controls` 语句

`controls`语句用于配置`rndc`命令管理`named`服务所需的各种安全要求。`controls`语句也称为控制通道。控制通道被`rndc`实用程序用于向命名服务器发送命令并获取结果。`controls`关键字后跟随一组包含在大括号内的选项。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_548_0.png)

## 语法

`controls`语句的语法如下：

```
controls { 

    option 1;

    option 2;

};
```

## 默认控制通道

如果未提供`controls`语句，则`named`实用程序将设置一个监听回环地址的默认控制通道。如果`controls`语句中没有`key`子句，则`named`实用程序将从`/etc/rndc.key`文件加载命令通道密钥。

# 如何配置 DNS 服务器

## 操作参考：安装 DNS

要在系统上安装 DNS：

1. 以 root 用户登录 Linux 服务器。
2. 输入`rpm -qi bind`以检查是否已安装`bind`软件包。
3. 如果`bind`和相关软件包未安装，则从安装介质中安装它们。
    1. 挂载包含最新版本的`BIND`的 Linux 安装 CD-ROM。
    2. 输入`cd /media/cdrom/Server`以访问安装 CD。
    3. 输入`rpm -ihv bind-({version}).({release}).rpm`以安装`BIND`。
    4. 输入`rpm -ihv caching-nameserver({version}).({release}).rpm`以获取初始配置。
    5. 输入`rpm -ihv bind-chroot-({version}).({release}).rpm`以在`chroot`环境中运行`BIND`。
    6. 输入`rpm -qi bind`以检查是否已正确安装`BIND`软件包。

## 操作参考：配置 DNS 服务

要在系统上配置 DNS 服务：

1. 以 root 用户登录。
2. 输入`cp /etc/named/caching-nameserver.conf /etc/named.conf`以使用`named.cachingnameserver.conf`文件作为模板。
3. 配置 DNS。
    1. 指定全局配置选项。
    2. 为根区域、回环域以及正向和反向区域添加区域语句。
    3. 创建正向和反向区域文件。
4. 输入`named-checkconf -f /etc/named.conf`以检查`named`语法。
5. 启动`named`服务。
    1. 输入`service named start`以启动`named`守护进程。
    2. 或者，如果`named`服务已在运行，输入`service named reload`以重新加载`named`守护进程。
    3. 输入`rndc reload`以重新加载区域文件。
    4. 输入`chkconfig named on`以在系统启动时启动`named`服务。

## 操作参考：配置 DNS 主机名查找

要配置 DNS 主机名查找：

1. 以 root 用户登录。
2. 配置客户端。
    a. 输入`vi /etc/resolv.conf`以编辑解析器配置文件。
    b. 按`I`键进入插入模式。
    c. 输入`nameserver (DNS 服务器 IP 地址)`以定义解析器应查询的命名服务器的 IP 地址。
    d. 保存并关闭文件。
3. 查询 DNS 服务器。
    a. 输入`dig [命令选项] [查询选项] {完全限定域名 | IP 地址}`以解析主机名和 IP 地址。
    b. 或者，输入`host [命令选项] {FQDN | IP 地址}`

## 操作参考：配置主 DNS 服务器

要配置主 DNS 服务器：

1. 以 root 用户登录。
2. 使用`vi`编辑器打开`/etc/named.conf`文件。
3. 添加`include`语句。例如，可以添加`include`语句以包含一个文件，例如`rndc.conf`，其中包含敏感的配置文件语句。

```
include "file_name";
```

4. 添加`options`语句，以包含将存放区域文件和缓存文件的目录位置。

```
options {

    directory "/var/named";

};
```

5. 如有必要，在`options`语句中指定其他全局配置选项，例如`notify`和`listen-on`。

```
options {

    directory "/var/named";

    notify yes;
```
