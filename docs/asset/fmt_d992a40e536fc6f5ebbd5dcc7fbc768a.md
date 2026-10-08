
系统提示你输入密码，然后你就获得了服务器的 FTP 权限。在这里，你可以使用标准的 FTP 命令上传和下载文件。

如果你在让 FTP 服务器正常运行方面遇到困难，可以遵循以下流程来帮助缩小问题范围。禁用防火墙和 SELinux。然后你可以检查配置文件以确保所有设置都正确（不要忘记选项和值之间不应有空格）。接下来，重启服务器并检查是否可以连接。验证你被允许登录，并且没有通过 `user_list` 或 `fusers` 文件拦截你正在测试的用户。当服务器正常运行时，重新添加防火墙（当然要带有正确的规则）。如果服务停止工作，说明你有防火墙问题，通常意味着端口未打开。当服务在防火墙下再次运行时，重新添加 SELinux 进行最终验证。

## 总结

当文件到处都是时，文件共享会让生活变得更容易。集中文件存储在安全和审计方面也有帮助。了解如何操作文件共享服务器是工作中协作的重要部分。用户总是需要一个存放文件的地方，而安全是一个日益增长的问题。确保你为文件服务器的增长做好计划，并定期测试它们的安全性。确保你擅长故障排除和配置 FTP 服务器，并验证你的客户端可以连接。

## 复习题

1. 用于安装 FTP 的包名称是什么？
2. 使用什么命令可以轻松列出 FTP 主配置文件中的所有选项？
3. 使用哪个选项允许匿名上传到 FTP 服务器？
4. 为了让 FTP 服务器正常运行，防火墙上应该开启哪两个端口？
5. `/etc/vsftpd/user_list` 文件是做什么用的？
6. 你可以使用什么客户端命令来测试你的 FTP 服务器连接？
7. FTP 是三种可用于 kickstart 和/或网络安装的协议之一。对还是错？

## 复习题答案

1. 使用 `vsftpd` 包安装 FTP 服务器。
2. `grep -v '^/etc/vsftpd/vsftpd.conf'` 命令向你显示当前 FTP 服务器正在使用的所有选项。
3. 主配置文件中的 `anonymous_enable=YES` 选项允许匿名加载。
4. 你必须开启 TCP 端口 20 和 21 才能让 FTP 服务器正常工作。
5. `user_list` 文件可以包含禁止登录的用户。
6. `lftp` 命令可以在客户端上使用来测试 FTP 服务器连接。
7. 正确。FTP 是用于 kickstart 和/或网络安装的三个协议之一。另外两个协议是 NFS 和 HTTP。

## 实验 17

### 任务 1 – 匿名 FTP

- 步骤 1。在 RHEL02 上设置匿名 FTP 服务器。
- 步骤 2。将 RHEL01 上 `/opt` 目录中的所有文件复制到 RHEL02 FTP 服务器。

当 RHEL02 上的 FTP 服务器包含来自 RHEL01 `/opt` 目录的所有文件时，任务完成。

### 任务 2 – 安全 FTP

- 步骤 1。在 RHEL01 上设置 FTP 服务器。
- 步骤 2。允许 RHEL01 上所有用户访问 `/home` 目录的 FTP。
- 步骤 3。确保拒绝来自实验室其他系统中所有其他用户的访问。

当 FTP 服务器设置好后，任务完成。

本章涵盖了以下主题：

- 设置 BIND——此部分介绍了如何设置 DNS 服务器。
- 配置 DNS 服务器——此部分讲解了不同类型 DNS 服务器的配置。
- DNS 工具和故障排除——此部分介绍了用于配置和故障排除 DNS 服务器的各种工具。
- BIND 安全——保护服务很重要，此部分涵盖了 DNS 安全细节。

涵盖了以下 RHCE 考试目标：

- 安装提供服务的包
- 配置 SELinux 支持服务
- 配置服务在系统启动时启动
- 配置基于主机的基于用户的安全性
- 配置仅缓存 DNS 服务器
- 配置仅缓存 DNS 服务器以转发查询（转发服务器）

## 第 18 章

### DNS

DNS（域名系统）是一种将人类可读的域名（如 `google.com`）转换为机器可读的 IP 地址的服务。对于人类来说，记住名字比记住 142.250.190 等数字容易得多。DNS 通常被称为“互联网电话簿”。

当服务器作为 DNS 服务器时，它负责回答域名查询。根据处理查询的方式，有不同类型的 DNS 服务器：

- 权威：此 DNS 服务器持有区域的实际记录并提供最终答案。
- 递归：如果缺少答案，此 DNS 服务器代表客户端查询其他 DNS 服务器。
- 缓存：此服务器存储之前的查询结果，为未来的请求提供更快的答案。
- 转发：此服务器仅将查询传递给指定的上游 DNS 服务器。

BIND（Berkeley Internet Name）软件是 Linux 上最广泛使用的 DNS 实现。它支持上述所有类型的服务器。

## 设置 BIND

当服务器作为 DNS 服务器时，它负责回答域名查询。要开始操作，你需要安装 BIND 包。

- 步骤 1。安装所需的包：

```bash
# yum install -y bind bind-utils
```

- 步骤 2。验证包已安装：

```bash
# rpm -qa | grep bind
```

- 步骤 3。在 RHEL01 系统上，你可以配置 BIND 服务随系统启动：

```bash
# systemctl enable bind
```

- 步骤 4。启动 BIND 服务：

```bash
# systemctl start bind
```

- 步骤 5。验证服务正在运行：

```bash
# systemctl status bind
```

BIND 配置文件位于 `/etc/bind/`。主配置文件是 `named.conf`，定义了全局选项和区域。每个区域通常定义在 `/etc/bind/zones/` 自己的文件中。

首先，编辑 `/etc/bind/named.conf` 文件来定义全局选项。具体指定 BIND 应监听哪些接口以及允许哪些客户端查询。

```bind
options {
    directory "/var/named";
    recursion-file "/var/named/rnd.keys";
    allow-query { 192.168.1.0/24; };
    allow-recursion { none; };
    listen-port { 53; };
    listen-on { any; };
};
```

接下来，在 `named.conf` 中定义区域。例如，为 `example.com` 添加一个区域：

```bind
zone "example.com" {
    type master;
    file "/etc/bind/zones/example.com.db";
};
```

最后，在 `/etc/bind/zones/example.com.db` 创建区域文件。此文件包含区域的资源记录，如 A、CNAME 和 MX 记录。

```bind
$TTL 86400
@   IN  SOA  ns1.example.com. admin.example.com. (
    2023101001 3 3600 1800 604800 8600 )
@   IN  NS   ns1.example.com.
ns1  IN  A    192.168.1.10
www  IN  A    192.168.1.11
```

string 这些更改后，重启 BIND 服务以应用它们：

```bash
# systemctl restart bind
```

你可以使用 `dig` 工具测试你的 DNS 服务器是否正确回答查询：

```bash
# dig @192.168.1.10 example.com
```

Red Hat 考试实战指南：RHCSA™ 和 RHCE® 认证指南和实验手册

## DNS 服务器

此时，你需要决定设置哪种类型的 DNS 服务器。根据 Red Hat 的说明，有两种类型的 DNS 服务器：

- 权威：这些 DNS 服务器回答区域的实际记录并提供最终答案。
- 递归：当没有答案时，这些 DNS 服务器代表客户端查询其他 DNS 服务器。

还有另一种分类 DNS 服务器的方法：

- 主（Master）：此 DNS 服务器存储特定命名空间的原始和权威区域记录。每个域名都必须至少有一个主服务器。
- 从（Slave）：虽然此 DNS 服务器从主 DNS 服务器接收命名空间信息，但该服务器可以回答它拥有的查询。
- 缓存（Caching）：此服务器存储之前的查询结果，为未来的请求提供更快的答案。
- 转发（Forwarding）：此服务器仅将查询传递给指定的上游 DNS 服务器。

## 排除

DNS 故障排除可能很棘手，但有几种工具可以帮助你：

- `dig`：DNS 查询最强大的工具。
- `nslookup`：较旧但仍被广泛使用的工具。
- `trace`：用于跟踪 DNS 查询的路径。
- `named-checkconf`：检查 BIND 配置文件错误的实用程序。

如果你的 DNS 服务器没有按预期响应，请检查配置文件、防火墙设置和 SELinux 状态。

## 步骤 3. 重启防火墙服务使更改生效：

```
# service iptables restart               [ OK ]
iptables: Flushing firewall rules:      [ OK ]
iptables: Setting chains to policy ACCEPT: filter [ OK ]
iptables: Unloading modules:             [ OK ]
iptables: Applying firewall rules:      [ OK ]
```

对于 DNS 服务器，您只有一个可以更改的 SELinux 布尔值（Boolean）：

`named_write_master_zones` 允许对主区域文件进行写入

如果您希望拥有动态 DNS 服务器或允许区域文件，则需要禁用此值；否则，您可以保持默认保护设置不变。

## 迁移提示

在 RHEL5 中，有一个额外的 SELinux 布尔值为 DNS 服务提供保护。您需要对其进行调整以确保 DNS 服务能够正常工作。

## 步骤 1. 查询您需要更改的布尔值：

```
# getsebool -a | grep named_dis
named_disable_trans -> off
```

## 步骤 2. 禁用 SELinux 保护：

```
# setsebool -P named___trans=1
```

## 步骤 3. 验证布尔值已更改：

```
# getsebool -a | grep named_dis
named_disable_trans -> on
```

提示：为了额外的安全，您可以设置 SELinux 仅允许系统用户读取 `/etc/named.conf` 文件。这确保了您可能需要的额外安全性。若要仅允许 named 用户读取 `/etc/named.conf` 文件，请使用以下命令：

```
# chcon -t named_conf_t /etc/named.conf
```

使用命令验证此操作：

```
# ls -Z /etc | grep named.conf
```

## 配置 DNS 服务器

要开始配置 DNS 服务器，请查看用于 BIND 服务器的这些关键配置文件：

- `/etc/named.conf`    主配置文件
- `/etc/rndc.key`    密钥文件
- `/etc/rndc.conf`    密钥配置文件
- `/usr/share/doc/bind-9*/sample` 存放示例文件的目录

在执行任何操作之前，您应该应该对 `/etc/named.conf` 文件进行备份：

```
# cp /etc/named.conf /etc/named.orig
```

您现在应该删除此文件，因为您将在接下来的章节中创建一个新的：

```
# rm /etc/named.conf
```

> 迁移提示
对于 RHEL5 用户，默认不存在 `/etc/named.conf` 文件，因此您不需要担心备份或删除它。

配置的第一步是确保您的系统具有静态 IP 地址，并且 `/etc/resol.conf` 文件指向本地（localhost）作为名称服务器：

**步骤 1.** 验证 RHEL01 使用 localhost 进行 DNS 查询：

```
# cat /etc/resol.conf
search example.com
nameserver 127.0.0.1
nameserver 192.168.1.1
```

这里列出的次要服务器实际上是我个人的路由器，它也可以提供 DNS 服务。在继续操作之前，您还应该理解 DNS 中使用的不同类型的资源记录，以及每种记录的重要性。

- A记录将主机名映射到 IP 地址
- NS 包含名称服务器的 IP 地址或 CNAME
- MX 定义特定域名的邮件去向哪里
- PTR 将 IP 地址映射到主机名
- SOA 包含对该域的通用管理控制
- CNAME 用作别名

有四种不同的 DNS 服务器类型，让我们从每种类型的配置开始。

### 主服务器 (Master Server)

主服务器是 DNS 基础设施的基础。它提供了一个定义所有 DNS 记录的地方并将其扩展到辅助服务器，有助于负载均衡和冗余。对于此主服务器配置，您需要创建一个新的 `/etc/named.conf` 文件。可以使用示例的 `/etc/named.conf` 文件来开始。以下是 `named.conf` 的外观：

```
/* BIND 服务器的全局选项 */
options
{
    directory "/var/named"; // 默认值
    dump-file "data/cache_dump.db";
    statistics-file "data/named_stats.txt";
    memstatistics-file "data/named_mem_stats.txt";
}
```

```
/* 日志选项，以便您知道日志去向哪里 */
logging
{
    channel default_debug {
        file "data/named.run"
        severity dynamic;
    }
}
```

```
/* 在这里定义我们的示例域名 example.com */
zone "example.com" {
    type master;
    file "example.com.zone"
    allow-update { none; };
}
```

```
/* 这是针对我们的子网 172.168.1.0/24 的反向查找 */
zone "1.1.168.172.in-addr.arpa" {
    type master;
    file "example.com.revzone"
    allow-update { none; };
}
```

/* 包含根提示（直接指向根 DNS 服务器）的文件 */

```
zone ". IN {
    type hint;
    file "named.ca";
};
```

```
/* 我们的 localhost 区域文件（适用于排故障） */
zone "localhost" IN {
    type master;
    file "named.localhost";
    allow-update { none; };
}
```

```
/* 我们 localhost 的反向查找（有助于排故障） */
zone "0.0.0.127.in-addr.arpa" {
    type master;
    file "named.localhost";
    allow-update { none; };
}
```

## 迁移 (TIP)

在 RHEL5 中，有一个额外的 SELinux 布尔值为 DNS 服务提供保护。您需要对其进行调整以确保 DNS 服务能够正常工作。

## 步骤 1. 查询您需要更改的布尔值：

```
# getsebool -a | grep named_dis
named_disable_trans -> off
```

## 步骤 2. 禁用 SELinux 保护：

```
# setsebool -P named___trans=1
```

## 步骤 3. 验证布尔值已更改：

```
# getsebool -a | grep named_dis
named_disable_trans -> on
```

提示：为了额外的安全，您可以设置 SELinux 仅允许系统用户读取 `/etc/named.conf` 文件。这确保了您可能需要的额外安全性。若要仅允许 named 用户读取 `/etc/named.conf` 文件，请使用以下命令：

```
# chcon -t named_conf_t /etc/named.conf
```

使用命令验证此操作：

```
# ls -Z /etc | grep named.conf
```

## 配置 DNS 服务器

要开始配置 DNS 服务器，请查看用于 BIND 服务器的这些关键配置文件：

- `/etc/named.conf`    主配置文件
- `/etc/rndc.key`    密钥文件
- `/etc/rndc.conf`    密钥配置文件
- `/usr/share/doc/bind-9*/sample` 存放示例文件的目录

在执行任何操作之前，您应该对 `/etc/named.conf` 文件进行备份：

```
# cp /etc/named.conf /etc/named.orig
```

您现在应该删除此文件，因为您将在接下来的章节中创建一个新的：

```
# rm /etc/named.conf
```
