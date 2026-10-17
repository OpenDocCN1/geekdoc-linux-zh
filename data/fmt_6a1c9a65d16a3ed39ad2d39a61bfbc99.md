
为确保实际挂载，你可能还需要设置一个在`/etc/fstab`文件中实际挂载的分区。实际上，iSCSI 驱动器的实际设备文件在每次重启时可能不同。因此，此类挂载应使用第 6 章中描述的通用唯一标识符`UUID`编号进行配置。

你不需要为 RHCE 考试创建 iSCSI 目标存储服务器。但由于 iSCSI 服务器的配置相对简单，你可以考虑为此目的创建一个。Red Hat 开发者 Daniel Berrangé 在 `http://berrange.com/tags/tgtadm/` 创建了一个关于 iSCSI 存储服务器创建的优秀入门介绍。

## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要在 `/home` 目录中设置每日备份文件的任务 | 在 `/etc/cron.daily` 目录中设置脚本，使用适当的备份命令复制 `/home` 中的文件。 |
| 已要求你在系统上设置 IPv6 转发 | 在 `/etc/sysctl.conf` 中包含 `net.ipv6.conf.all.forwarding=1` 设置，并使用 `sysctl -p` 命令激活它。 |
| 你需要为单文件 RPM 设置源代码 | 在专用目录中设置单个文件以及可执行的 `configure` 脚本；然后将其设置在压缩的 `tar` 归档中。 |
| 你需要在设备 `eth1` 上设置一条特殊静态路由 | 使用 `Network Connections` 工具设置该特殊路由，提供网络地址、子网掩码和期望的网关 IP 地址。 |
| 你需要将系统设置为 Kerberos 客户端 | 使用 GUI 身份验证配置工具；`realm` 应为域的大写列表。你还需要 KDC 和 Kerberos 管理服务器的 FQDN，可能相同。 |
| 你需要设置 iSCSI 发起程序 | 安装 `iscsi-initiator-utils` 包，使用 `iscsiadm` 命令发现可用的 iSCSI 目标，并确保 `iscsi` 服务在重启时处于活动状态。 |

## 认证总结

Linux 管理员需要定期配置脚本。示例脚本已在不同的 `/etc/cron.*` 目录中可用。通常，脚本以 `#!/bin/bash` 行开头，该行设置了脚本其余部分的语言。管理脚本可以使用 `bash` 命令，以及 `for`、`if`、`do` 和 `test` 等运算符。内核运行时参数可以在 `/proc/sys` 目录中找到。但对这些文件的更改是临时的。对于更永久的更改，你需要在 `/etc/sysctl.conf` 文件中设置选项。对该文件的更改可以使用 `sysctl -p` 命令实现。许多标准选项与网络有关。

RHCE 的一项新要求是从单个文件创建 RPM。为此，你需要知道如何设置源代码归档。`rpmdevtools` 和 `rpm-build` 包可以帮助。`rpmdev-setuptree` 命令可以帮助设置所需的目录。`rpmdev-newspec` 命令可以帮助为 `.spec` 文件创建模板。然后可以使用 `rpmbuild` 命令根据 `spec` 文件中的说明以及打包的源代码处理成 SRPM 和可在不同系统上安装的 RPM 包。

RHCE 目标包括对几种特殊网络选项的要求。在 `Network Connections` 工具的帮助下，可以在 `/etc/sysconfig/network-scripts` 目录中的文件中配置特殊 IP 路由。Kerberos 客户端可以在 `/etc/sssd/sssd.conf` 文件中配置，通过 `/etc/nsswitch.conf` 文件引用。也许使用 GUI 身份验证配置工具配置 Kerberos 客户端是最简单的方法。

## 两分钟速览

以下是第 12 章认证目标中的一些关键点。

### 自动化系统维护

- [ ] 标准管理脚本可以为自定义脚本提供模型，以自动化系统维护任务。
- [ ] 脚本中的各种命令运算符包括 `do`、`for`、`if` 和 `test`。
- [ ] 许多 Linux 管理脚本以 `#!/bin/bash` 开头，这是对 `bash` shell 的引用。

### 内核运行时参数

- [ ] 内核运行时参数位于 `/proc/sys` 目录中。
- [ ] 许多内核运行时参数与转发和安全等网络选项有关。
- [ ] 内核运行时参数可以通过 `/etc/sysctl.conf` 文件的帮助永久配置。

### 创建 RPM 包

- [ ] 可用的源 RPM 可以用作模型，帮助创建自己的 RPM。
- [ ] RPM 源代码组件可以在用户主目录中、`rpmbuild/` 子目录中找到，如 `rpmdev-setuptree` 命令配置的那样。
- [ ] 实际源代码可以在 `rpmbuild/SOURCES` 子目录中找到。
- [ ] RPM 是使用 `rpmbuild` 命令构建的，基于 `rpmbuild/SPECS` 子目录中的 `.spec` 文件。你可以使用 `rpmdev-newspec` 命令创建标准的 `.spec` 模板。
- [ ] 构建的 RPM 可以在 `rpmbuild/SRPMS` 和 `rpmbuild/RPMS` 子目录中找到。

### 特殊网络选项

- 默认到外部网络的网络路由通过网关 IP 地址。
- 到不同网络的特殊路由可以通过某些特定 IP 的网络设备配置。
- 要配置 Kerberos 客户端，你需要修改 `/etc/sssd/sssd.conf` 文件。
- Kerberos 客户端的连接还要求连接到 LDAP 等网络身份验证服务。
- 要配置 iSCSI 客户端，你需要 `iscsi-initiator-utils` 包，可以使用 `iscsiadm` 命令连接到 iSCSI 存储。
- 为了确保 iSCSI 连接在重启后仍然存在，你需要激活 `iscsi` 服务。

![](img/9139201cfcaf4292284a0eed074928e5_711_0.png)

## 自测

以下问题将帮助衡量你对本章所介绍材料的理解。由于 Red Hat 考试中没有多项选择题，本书中也没有多项选择题。这些问题专门测试你对本章的理解。如果你有另一种执行任务的方法是可以的。Red Hat 考试看重的是结果，而不是死记硬背琐碎知识。

### 自动化系统维护

1. 脚本中与成功关联的退出编号是多少？

2. 什么运算符表示“任何其他”？

### 内核运行时参数

3. 与 `net.ipv4.ip_forward` 参数关联的文件的完整路径是什么？

### 创建 RPM 包

4. 当用户 `stephanie` 在其主目录中从 SRPM 安装源代码时，实际源代码的完整路径是什么？

5. 可以使用其中的命令创建 spec 文件模板的包的名称是什么？

6. 在源代码目录中处理标准源代码包所需的一个常见文件是什么？附加：与普通文件相比，该文件的权限应该有什么不同？

7. 可以使用什么命令仅从源代码创建常规 RPM，基于 `rpmbuild/SPECS` 子目录中的 `test.spec` 文件？假设所有必需的源代码都在正确的位置。

8. 当用户 `tim` 构建与 64 位系统关联的常规 RPM 时，该 RPM 的目录的完整路径是什么？

### 特殊网络选项

9. 与特殊路由关联的三种 IP 地址类型是什么？

10. Kerberos 客户端在哪个文件中配置？

11. `server1.example.com` 系统的标准 Kerberos realm 是什么？

12. 在正确配置的 iSCSI 目标上重启时应该运行什么服务脚本？

## 实验问题

其中一些实验涉及配置练习。你应该只在测试机器上执行这些练习。假设你正在虚拟机如 KVM 上运行这些练习。Red Hat 以电子方式提供考试。出于这个原因，本章及以后章节的实验可在随书附带的 CD 上获得，位于 `Chapter12/` 子目录中。如果尚未在系统上设置 RHEL 6，请参阅第 1 章的安装说明。实验的答案在填空题的自测答案之后。

## SELF TEST ANSWERS

### Automate System Maintenance

- 1. 脚本成功时关联的退出号码是 `0`。在脚本中，表示“非”的运算符是感叹号 `!` 。（在 Linux 世界中它也被称为“bang”。）

### System Run-Time Parameters

- 2. 与 `net.ipv4.ip_forward` 参数关联的文件的完整路径是 `/proc/sys/net/ipv4/ip_forward`。

### Create an RPM Package

- 3. 由用户 `stephanie` 从 SRPM 安装的实际源代码的完整路径是 `/home/stephanie/rpmbuild/SOURCES`。
- 4. 可用于创建 spec 文件模板的命令所对应的软件包名称是 `rpmdev-newspec`。
- 5. 标准源代码软件包中需要的常见文件名为 `configure`。奖励：该文件还应具有可执行权限。
- 6. 在给定条件下可用于仅从源代码创建常规 RPM 的命令是 `rpmbuild -ba rpmbuild/SPECS/test.spec`。
- 7. 当用户 `tim` 构建与 64 位系统关联的常规 RPM 时，该 RPM 所在目录的完整路径是 `/home/tim/rpmbuild/RPMS/x86_64`。

### Special Network Options

- 8. 与特殊路由关联的三种 IP 地址类型是网络地址、网络或子网掩码以及网关地址。
- 9. 在 RHEL 6 上，Kerberos 客户端通常在 `/etc/sssd/sssd.conf` 文件中配置。
- 10. `server1.example.com` 系统的标准 Kerberos 领域是 `EXAMPLE.COM`。
- 11. 在配置正确的 iSCSI 目标上，应在重启时处于活动状态的服务脚本是 `iscsi`。

## LAB ANSWERS

### Lab I

本实验的成功应该很直接。如果您已按实验正文中建议的方式运行 `date` 命令，则 `/etc` 目录中的文件应在一分钟后复制到 `/backup` 目录。

将该脚本设置为按每小时运行的最简单方法是将其配置在 `/etc/cron.hourly` 目录中。该脚本只需要两行。以下是该脚本配置的一个示例：

```
```
