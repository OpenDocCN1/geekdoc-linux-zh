
`d)` opening index `/var/lib/rpmbuilddb.13427/Packages` `0x42` `mode0x2`

`d)` opening index `/var/lib/rpmbuilddb.13427/Oxi` `01` `mode0x2`

`2)` adding to `Installed` index.

adding `z7f5e6d5b3e506d474d2e10f8dba52b0` to `Shaheader` index.

`d)` closed index `/var/lib/rpmbuilddb.13427/Packages`

`d)` closed index `/var/lib/rpmbuilddb.13427/Shaheader`

`d)` closed index `/var/lib/rpmbuilddb.13427/Basenames`

`d)` closed index `/var/lib/rpmbuilddb.13427/Collates`

`d)` closed index `/var/lib/rpmbuilddb.13427/Installtd`

`d)` closed index `/var/lib/rpmbuilddb.13427/Triggername`

`d)` closed index `/var/lib/rpmbuilddb.13427/pragma0x0`

`d)` closed index `/var/lib/rpmbuilddb.13427/Packages` `0x42` `mode0x2`

`d)` closed index `/var/lib/rpmbuilddb.13427/Oxi` `01` `mode0x2`

`d)` closed index `/var/lib/rpmbuilddb.13427/Conflictname`

`d)` closed index `/var/lib/rpmbuilddb.13427/manifest`

`d)` closed index `/var/lib/rpmbuilddb.13427/Mqueryname`

`d)` closed index `/var/lib/rpmbuilddb.13427/requirements`

`d)` closed index `/var/lib/rpmbuilddb.13427/rsdbmd`

`d)` closed index `/var/lib/rpmbuilddb.13427/specname`

`d)` closed index `/var/lib/rpmbuilddb.13427/Packages`

`d)` closed index `/var/lib/rpmbuilddb.13427/environment`

`d)` closed index `/var/lib/rpmbuilddb.13427`

### 更多内容...

如果由于某种原因，你无法恢复 `RPM` 数据库，还存在最后一个选择。企业通常倾向于使用标准化的构建，许多服务器安装了相同的软件包，因此可以从另一个具有相同软件包`set`的服务器拷贝健康的 `/var/lib/rpm` 目录到损坏的服务器上，并执行之前的配方步骤以确保一切正常。

虽然你会发现其他可以救急的额外工具（例如 `RPM` `cron`），但通常拥有一个良好的备份更具实用性。

# 加固 `RHEL` 7

在本章中，你将学习到：

- 安装和配置 `IPA`
- 加固系统登录
- 使用 `sudo` 配置权限提升
- 使用 `firewalld` 加固网络
- 使用 `kdumpump` 和 `SysRq`
- 使用 `ABRT`
- 审计系统

### 简介

安全是你环境中的一个重要方面。本章提供的配方并非详尽的操作指南合集；而是处理环境中安全问题的起点，因为每个环境都是不同的。本章旨在让你了解使用 `Red Hat Enterprise Server 7` 内置包含的一组简单工具可以做什么。

在本章中，我将不会尝试解释系统何处存储 `syslog` 日志以及它们的含义，因为这可能是一个详尽的话题。最重要的安全相关的 `syslog` 日志可以在 `/var/log/secure` 和 `/var/log/audit/audit.log` 中找到。

# 安装和配置 `IPA`

`IPA`（身份策略审计）服务器允许你在一个中心位置管理 `kerberos`、`DNS`、主机、用户、`sudo` 规则、密码策略和自动挂载（`automounts`）。`IPA` 是多个包的组合，包括但不限于 `bind`、`ldap`、`pam` 等。它整合了所有内容为你的环境提供身份管理。

### 准备工作

在这个配方中，我将选择集成 `DNS` 设置，尽管也可以使用现有的 `DNS` 基础设施。

### 如何操作...

首先，通过遵循在 `IPA` 客户端上需要的操作来安装服务器组件。

# 安装 `IPA` 服务器

按照以下指令安装 `IPA` 服务器：

1. 通过以下命令安装必要的软件包：

   ```bash
   # yum install -y ipa-server bind-dyndb-ldap
   ```

2. 软件包安装完成后，按如下方式调用 `ipa` 安装程序：

   ```bash
   # ipa-server-install
   ```

3. 如下所示配置集成 `DNS`：
   你是否想配置集成 `DNS` (`BIND`?) [no]: yes

4. 检测到已存在 `/etc/resolv.conf`，覆盖吗？
   检测到已存在 `BIND` 配置，覆盖吗？ [no]: yes

5. 如下所示提供 `IPA` 服务器的主机名：
   `Server host name [localhost.localdomain]: master.example.com`

6. 现在，如下所示确认 `IPA` 服务器的 `DNS` 域名：
   请确认域名 `[example.com]:`

# 第 9 章

7. 如下所示为 `IPA` 服务器提供 `IP` 地址：

   请提供用于此主机名的 `IP` 地址：
   `192.168.0.1`

8. 接下来，如下所示提供 `Kerberos` 域名称（`realm`）：

   请提供 `realm` 名称 `[EXAMPLE.COM]:`

9. 如下所示创建并确认目录管理员密码：

   `Directory Manager password:`

10. 如下所示创建并确认 `IPA` 管理员密码：

    `IPA admin password:`

11. 现在，如下所示配置 `DNS` 转发器（`forwarders`）：

    你是否想配置 `DNS` 转发器？ [yes]: no

12. 最后，如下所示配置反向 `DNS` 区域：

    你是否想配置反向区域？ [yes]:
    请指定反向区域名称 `[0.168.192.in-addr.arpa]:`

安装程序现在将提供类似下面的概述：

`IPA` 主服务器将将配置为：
`Hostname: master.example.com`
`IP address: 192.168.0.1`
`Domain name: example.com`
`Realm name: EXAMPLE.COM`

`BIND DNS` 服务器将配置为服务 `IPA` 域：
`Forwarders: No forwarders`
`Reverse zone: 0.168.192.in-addr.arpa.`

13. 现在，通过输入 `"yes"` 确认信息，如下：

    使用这些值继续配置系统吗？ [no]: yes

此时，你将看到大量信息在屏幕上滚动，表示安装程序正在执行：安装或配置 `NTP`、`LDAP`、`BIND`、`Kerberos`、`HTTP`、证书服务器以及对之前示例中 `IPA` 相关的修改。

安装和配置过程可能需要一些时间，请耐心等待。

![](img/a6dbf7df749be83c0faae2334e970c0b_935_0.png)

# 加固 `RHEL` 7

# 安装 `IPA` 客户端

执行以下步骤在你的系统上安装并配置 `IPA` 客户端：

> 确保你的系统主机名与 `localhost.local` 不同。如果不是，客户端配置将失败。

1. 通过以下命令确保安装必要的软件包：

   ```bash
   # yum install -y ipa-client
   ```

2. 通过以下操作确保 `IPA` 服务器作为 `DNS` 服务器：

   ```bash
   # cat /etc/resolv.conf
   search example.com
   nameserver 192.168.0.1
   ```

3. 通过运行此命令行涉及 `IPA` 客户端配置：

   ```bash
   # ipa-client-install --enable-dns-updates
   ```

安装程序现在将显示检测到的 `IPA` 服务器概述，并要求提供用户（`IPA` 管理员）和密码来注册你的系统，后续变更集如下：

```text
#ipa-client-install --enable-dns-updates

发现成功：

Domain: example.com

Master: example.com

Realm: EXAMPLE.COM

IPA Server: example.com

BaseDN: example.com

使用这些值继续配置系统吗？ [no]: yes

用户已在 realm 授权：admin@EXAMPLE.COM

admin@EXAMPLE.COM 的密码： 

成功注册服务器。

Certificate: Certificate Authority,EXAMPLE.COM

Subject: Certificate Authority,EXAMPLE.COM
```
