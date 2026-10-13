
## 练习 4-4

### 配置 EPEL 仓库

在此练习中，你将配置访问 EPEL。这将手动配置仓库。

- 1. 登录到系统 `system1.example.com`。
- 2. 运行以下命令：
  ```bash
  # dnf install https://dl.fedoraproject.org/pub/epel-release-9.noarch.rpm
  ```
- 3. 该命令在 `/etc/yum.repos.d` 中创建了一个名为 `repo` 的文件。
- 4. 安装软件包：

```bash
# dnf install https://dl.fedoraproject.org/pub/epel-release-9.noarch.rpm
```

## 基础 dnf 命令

如果你想了解更多关于 `dnf` 命令的细节，直接运行该命令。你会看到以下输出，可能太快了。当然，你可以将输出通过给 `less` 命令。

```bash
# dnf
Updating Subscription Management repositories:
usage: dnf [options] COMMAND
```

常用命令：

你将在后续章节中检查这些命令和选项是如何工作的。虽然在红帽考试期间你可能没有互联网访问，但你可能连接到本地配置的仓库。考试期间，`dnf` 是管理红帽系统的基本工具。

从简单的命令开始：`dnf list`。它将返回软件包列表（无论已安装还是可用），以及它们的版本号和仓库。`dnf list | grep packename` 告诉你通过 `dnf install` 将获得哪个版本的。如果你想显示所有已配置的仓库，可以使用 `dnf repolist`。关于特定软件包的更多信息可以通过 `dnf info` 命令获取。例如，该命令在功能上等同于 `rpm -qpi samba`：

### 安装模式

有两个基本的安装命令。如果你以前没有安装过软件包，或者你想将其更新到最新稳定版本，请运行 `dnf install packename`。你不需要指定版本或发布版本。只需要包名。例如，如果你正在检查 Samba RPM 的最新版本，以下命令将更新它，或者在目标系统上尚未安装时添加它：

## 第4章 软件管理

如果您想将系统上的软件包更新到最新版本，请运行 `dnf update packageName` 命令。例如，如果您已经安装了 Samba RPM，以下命令将将其更新到最新版本：

```bash
# dnf update samba
```

如果您尚未安装 Samba，此命令不会将其添加到已安装的软件包中。通过这种方式，`dnf update` 命令类似于 `rpm -F` 命令。当然，如果没有可以移除软件包的选项，`dnf` 命令就是不完整的。第一个选项非常直观，因为它会卸载 Samba 软件包以及任何依赖项：

```bash
# dnf remove samba
```

`dnf update` 本身强大；如果您想确保所有已安装软件包都更新到最新版本，请运行以下命令：

```bash
# dnf update
```

`dnf update` 可能需要一些时间，因为它需要与 Red Hat Portal 或其他存储库通信。它可能需要下载包含所有依赖关系的当前软件包数据库。它会找到所有可用更新的软件包并将其添加到待更新列表中。如果它发现了依赖包，这些包尚未包含在更新列表中。

如果您想查看更新列表怎么办？`dnf list updates` 可以为此提供帮助。它在功能上等同于 `dnf check-update` 命令。但如果您不确定安装什么呢？例如，如果您想安装 Evince 阅读器，并认为操作命令包含“evince”一词，那么 `dnf` 提供的 `/evince*` 命令可以提供帮助。

或者，要搜索所有以 `.repo` 扩展名的文件实例，请运行以下命令：

```bash
# dnf provides "*.repo"
```

它列出了所有以 `.repo` 扩展名结尾的软件包实例以及相关的 RPM 软件包。需要通配符是因为该选项需要文件路径。它接受部分文件名；例如，`dnf provides "/etc/systemd/**"` 会返回与 `/etc/systemd` 目录下的文件相关的 RPM。一旦安装了软件包，您就可以继续执行 `dnf install packageName` 命令。

在许多情况下，`dnf` 的问题可以通过 `dnf all` 命令来解决。如果 Red Hat 软件包（或第三方存储库）有最近更新，此命令将刷新元数据缓存，允许您与配置的存储库同步元数据，而无需等待缓存在 24 小时后自动刷新。

![](img/9c00a73030da5bd310455c3e10fece4d_192_0.png)

https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

## 安全与 dnf

GPG 数字签名可以验证 `dnf` 更新的完整性和真实性。这与本章早期描述的 RPM 软件包系统是相同的。作为一个示例，查看第一次在 RHEL 9 上通过网络安装新软件包的情况：

```bash
# dnf install samba
```

软件包下载后，您将看到类似下面所示的消息：

```
Importing GPG key 0XFD431D51:
User: "Red Hat, Inc. (release key 2) <security@redhat.com>
Fingerprint: 56E7 347A 00D4 4ADE 55D6 6F13 8A5F 29F1 43D1
From: /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
Is this ok [y/N]: successfully
Key imported
Importing GPG key 0X5A640B3:
User: "Red Hat, Inc. (auxiliary key 3) <security@redhat.com>
Fingerprint: 7E46 2425 8C40 6535 D5D6 5054 E4A4 5A63 40B3
From: /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
Is this ok [y/N]:
```

如果您从其他存储库安装软件包，可能会出现额外的 GPG 密钥供审核。正如该行所示，`N` 是默认响应；您实际上必须输入 `y` 才能继续下载和安装——不仅是 GPG 密钥，还包括针对涉及的软件包。
您可能会注意到，该 GPG 密钥与本章早期与 `rpm` 命令相关的密钥来自同一个域名。

## 更新与安全修复

Red Hat 在 https://access.redhat.com/search/ 维护了一个按 RHEL 版本分类的公共错误列表（errata）。如果您有 RHEL 订阅，受影响的软件包通常通过 Red Hat Portal 提供；对于连接到 RSM 的机器，您只需要定期运行 `dnf update` 即可。对于使用 RHEL 源码的第三方（如 AlmaLinux 和 Oracle Linux）非常有用；RHEL 重构会在 Red Hat 发布后不久提供错误修复。

## 软件包组与 dnf

`dnf` 命令可以做到这一点。它可以按组安装和删除软件包。通过以下命令，您可以从配置的存储库中识别可用软件包组：

```bash
# dnf group list
```

### 158 第4章 软件管理

图 4-8

```
[root@server1 ~]# "Virtualization Host"
Updating Subscription Management repositories.
Last metadata check: 00:33 ago Mon 15
Group: Virtualization Host
Description: Minimal
Mandatory Groups:
Base
Core
Optional Groups:
Debugging
Virtualization Hypervisor
Virtualization Platform
[root@server1 ~]#
```

图 4-9

```
[root@server1 ~]# dnf group info "Virtualization Host"
Updating Subscription Management repositories.
Last metadata check: 08:33 ago Mon 15 May 2023 03:51 AM CDT.
Group: Virtualization Host
Description: Minimal
Mandatory Groups:
Base
Core
Optional Groups:
Debugging
Virtualization Hypervisor
Virtualization Platform
[root@server1 ~]#
```

图 4-10
```
