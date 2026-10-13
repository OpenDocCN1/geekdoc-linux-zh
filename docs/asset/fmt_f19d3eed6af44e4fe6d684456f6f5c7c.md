
# 术语表

## `Red Hat Virtualization (RHEV)`
`RHEV` 是一种基于 `KVM` 的虚拟化解决方案。它是一个独立产品，通过提供易于使用的管理界面脱颖而出。

## `Red Hat Package Manager (RPM)`
`Red Hat Package Manager` 是一种用于捆绑软件的标准。它是一个管理软件包的工具。

## `referral`
`referral`（重定向）在 `LDAP` 中，`referral` 是指向另一个服务器的指针。

## `relaying`
`relaying`（转发）在电子邮件中，`relaying` 是转发电子邮件的过程。

## `replication`
`replication`（复制）在 `LDAP` 中，`replication` 是创建相同数据库的多个副本。

## `repositories`
`repositories`（仓库）在包管理中，`repositories` 是一个安装源。它可以是本地目录或包含包的远程服务器。

## `resource records`
`resource records`（资源记录）在 `DNS` 中，`resource records` 是数据库中的记录。有多种类型，例如解析名称的 `A`，或解析 IP 地址的 `PTR`。

## `RGManager`
`RGManager`（资源组管理器）在高可用性集群中，`RGManager` 是资源组。它决定了集群资源的位置。

## `RHEV Manager (RHEV-M)`
`RHEV Manager (RHEV-M)`（RHEV 管理）在 `Red Hat Virtualization` 中，`RHEV-M` 是提供管理虚拟机的主机。

## `RHEV-H`
在 `Red Hat Virtualization` 中，`RHEV-H` 是虚拟机程序主机。它是运行 `KVM` 的主机。

## `ricci`
在高可用性集群中，`Ricci` 是提供基于 Web 的管理界面的平台。`Ricci` 是运行在所有节点上的代理，并由界面进行管理。

## `root domain`
`root domain`（根域名）在 `DNS` 中，`root domain` 是所有名称解析的起点。它位于包含顶级域的层次结构顶端。

## `rotating log file`
`rotating log file`（滚动日志文件）滚动日志文件是根据旧日志文件年龄或大小等标准，关闭旧日志文件并打开新日志文件的过程。滚动日志用于确保磁盘不会被日志文件完全填。

## `rsyslog process`
`rsyslog process`（`rsyslog` 进程）`rsyslog` 进程负责记录系统消息。为了指定它应该做什么，它使用配置文件，在其中使用设施和优先级来定义日志记录的位置。

## 设置组 ID (SGID)
`SGID` 是一种权限，它确保执行文件的人将以该文件所有者所在组的权限执行文件。此外，当应用于目录时，`SGID` 会设置该目录的组所有权的向下继承。这意味着在该目录及其子目录中创建的所有项都将具有相同的组所有者。

## 设置用户 ID (SUID)
`SUID` 权限使得执行文件的用户将以该文件所有者的权限执行文件。这是一种具有潜在危险的权限，由于某些原因，系统管理员通常不会使用它。

## 共享内存 (shared memory)
`shared memory` 是进程之间共享的内存。`shared memory` 非常有用，例如当多个进程需要访问同一个库时。与其多次加载该库，不如在进程之间共享它。

## shebang
`shebang` (`#/bin/bash`) 用于 shell 脚本的第一行。它指示了应该使用哪种 shell 来解释 shell 中的命令。

## shell
`shell`（外壳/解释程序）是解释用户命令并与计算机硬件界面的用户界面。

## shell 脚本 (shell script)
`shell script` 是一个包含一系列命令的文件，其中可以使用条件语句，以便在特定情况下执行某些命令。
