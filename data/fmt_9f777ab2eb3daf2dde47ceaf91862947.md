
- 5. 显示你系统 DNS 服务器监听的端口。对于 Linux 系统，使用

```bash
# netstat -p -a | grep name
```

对于 Solaris 系统，使用

```bash
# netstat -a | grep domain
```

- 6. 显示你系统的主机名和 IP 地址：

```bash
# nslookup
```

## 知识掌握检查

- 1. DNS 提供了一个 ________命名空间，其中包含域、子域和主机名。
- 2. 对或错：如果两个不同域的公司为它们的其中一个系统选择了相同的主机名，则其中一家公司需要更改主机名以避免 DNS 冲突。
- 3. 从主机名转换为 IP 地址 ________。
- 4. 在此主机名中，域、组织、子域和主机分别？

`www.athletics.indiana.edu`
- 5. 哪个命令提供了从命令行查询 DNS 服务器的机制？
- 6. 在命令模式下使用 `nslookup` 时，将 DNS 服务器更改为 `192.168.1.215` 的 DNS 服务器的命令是什么？
- 7. 你可能考虑使用哪两个命令来代替 `nslookup`，这两个命令都都提供与 `nslookup` 相同的信息以及额外的 DNS 信息？
- 8. 哪个 DNS 配置文件提供了对 NIS 的访问？
- 9. 哪个 DNS 配置文件提供了对 NIS 的访问？

## 模块 14：使用域名系统 450 UNIX 系统管理：入门指南

## 模块 15：使用 NIS 455

## 关键技能

- 15.1 NIS 服务概述
- 15.2 发现 NIS 组件
- 15.3. 设置 NIS 服务器
- 15.4. 配置 NIS 客户端
- 15.5. 设置 NIS 服务器

## 454 UNIX 系统管理：入门指南

同样地，在 UNIX 客户端使用 DNS 服务器之前，`hosts;` 条目必须包含一个 `dns` 指令：

`hosts; dns` 文件

> `/etc/resolv.conf` 文件用于提供本地机器 DNS 配置的特定信息。该文件的基本语法包括添加客户端所属的域以及一个或多个查询的名称服务器。

`domain home.com`
`nameserver 216.155.202.163`

表示本地机器在向 IP 地址为 `216.155.202.163` 的 DNS 服务器进行查询时应使用 `home.com` 域。在实践中，文件中会添加两个 DNS 服务器条目，以便在第一个服务器不可用时客户端查询第二个服务器。

> 提示
> `nameserver` 命令必须通过 DNS 服务器的有效 IP 地址完成，而不是服务器的主机名。为什么？因为如果提供了 DNS 的主机名，将无法将名称解析为 IP 地址，因为该条目旨在为系统提供 DNS 解析。当调用 `nslookup` 或其他 DNS 工具时，它们会查询此文件获取名称服务器和域信息。

## 模块 14：使用域名系统 451

你可以在文件中放置一个或多个名称服务器条目，这样当主 DNS 服务器之一故障时，可以使用另一个来响应客户端请求。通常，每个客户端系统都应至少有两个名称服务器定义，以确保合理的冗余。

![](img/2928fe42a92e6fb43bbbe3768008092f_471_0.png)

## 项目 14-1

在此项目中，你将检查系统上的 DNS 配置并练习使用 DNS 工具。

### 步骤说明

- 1. 显示系统 DNS 配置文件的内容：

```bash
# more /etc/named.conf
```

- 2. 通过查找 `directory` 选项行，识别你系统上存储额外 DNS 配置文件的目录。
- 3. 显示你系统的主区域文件和反向区域文件的内容，将 `/var/named` 替换为正确的目录，并将 `sjmaxwell.org` 和 `192.168.1.in-addr.arpa` 替换为正确的域名和反向域名，记住在后者中使用你网络的 IP 地址：

```bash
# /var/named/sjmaxwell.org
# /var/named/192.168.in-addr.arpa
```

- 4. 验证你的系统 DNS 服务器正在运行。对于 Linux 系统，使用

```bash
# ps -ef | grep name
```

对于 Solaris 系统，使用

```bash
# ps -ef | grep in.named
```

- 5. 显示你系统 DNS 服务器监听的端口。对于 Linux 系统，使用

```bash
# netstat -p -a | grep name
```

对于 Solaris 系统，使用

```bash
# netstat -a | grep domain
```

- 6. 显示你系统的主机名和 IP 地址：

```bash
# nslookup
```

## 知识掌握检查

- 1. DNS 提供了一个 ________命名空间，其中包含域、子域和主机名。
- 2. 对或错：如果两个不同域的公司为它们的其中一个系统选择了相同的主机名，则其中一家公司需要更改主机名以避免 DNS 冲突。
- 3. 从主机名转换为 IP 地址 ________。
- 4. 在此主机名中，域、组织、子域和主机分别？

`www.athletics.indiana.edu`
- 5. 哪个命令提供了从命令行查询 DNS 服务器的机制？
- 6. 在命令模式下使用 `nslookup` 时，将 DNS 服务器更改为 `192.168.1.215` 的 DNS 服务器的命令是什么？
- 7. 你可能考虑使用哪两个命令来代替 `nslookup`，这两个命令都都提供与 `nslookup` 相同的信息以及额外的 DNS 信息？
- 8. 哪个 DNS 配置文件提供了对 NIS 的访问？
- 9. 哪个 DNS 配置文件提供了对 NIS 的访问？

# 456 UNIX 系统管理：初学者指南

当主 NIS 服务器上进行更改时，信息会自动“推送”到备服务器。

当客户端系统启动时，它会绑定到客户端域内的一台 NIS 服务器。所有对数据库信息的请求（例如 UNIX 身份验证或主机名解析）都会发送到客户端所绑定的服务器。

## 15.2 发现 NIS 组件

一个 NIS 服务器包含以下内容：

- 数据库
- 进程
- 工具

### 数据库

NIS 服务器为 UNIX 上可用的种类型文件或网络服务维护一个数据库。例如，对于名称解析，`/etc/hosts` 文件被使用，NIS 数据库就是根据该文件构建的。在设置 NIS 服务器时，NIS 服务器上的每个本地文件都被用作 NIS 数据库的基础。NIS 服务器提供的每个映射称为 NIS 映射（NIS map），这些映射位于 `/var/yp` 目录中。对于每个 NIS 服务，会创建一个或多个 DBMS 文件以提供对内容的快速访问。例如，对于 `/etc/hosts` 文件，会创建以下 DBMS 文件：

```
-rw-- 1 root 4096 root Feb 25 22:06 hosts.byaddr.dir
-rw-- 1 root 4096 root Feb 25 22:06 hosts.byaddr.pag
-rw-- 1 root 4096 root Feb 25 22:06 hosts.byname.dir
-rw-- 1 root 3072 root Feb 25 22:06 hosts.byname.pag
```

这些文件支持构成数据库的键/值对。`.dir` 文件包含文件数据的位图，而实际数据存储在 `.pag` 文件中。对于 `/etc/hosts` 文件，维护着两个独立的数据库文件：一个按 IP 地址排序数据库（`hosts.byaddr`），另一个按主机名排序（`host.byname`）。

要确定特定的 NIS 服务器支持哪些服务和/文件，请检查 `/var/yp/<domain>` 目录，其中 `<domain>` 是 NIS 域——例如 `home.com`。因此，命令

```
ls -l /var/yp/home/*/.pag
```

# 模块 15：使用 NIS 457

显示了 `home.com` 域的所有映射：

```
/var/yp/home.com/auto.home.pag
/var/yp/home.com/auto.master.pag
/var/yp/home.com/group.bygid.pag
/var/yp/home.com/group.byname.pag
/var/yp/home.com/hosts.byaddr.pag
/var/yp/home.com/hosts.byname.pag
/var/yp/home.com/ipnodes.byaddr.pag
/var/yp/home.com/ipnodes.byname.pag
/var/yp/home.com/mail.aliases.pag
/var/yp/home.com/mail.byaddr.pag
/var/yp/home.com/netgroup.byhost.pag
```
