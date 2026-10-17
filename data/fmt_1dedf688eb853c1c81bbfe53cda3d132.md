
ping `server1.example.com`

ping `172.16.0.2`

```
2. 检查链路状态和 IP 地址：
```bash
ip addr show
```
```

3. 检查相关的网络配置文件。你现在识别问题了吗？
```bash
cat /etc/NetworkManager/system-connections/*.nmconnection
```
```

4. 如果你无法识别问题，打开 Network Manager 连接编辑器并查看连接配置中的 /IPv4 设置信息：
```bash
nm-connection-editor
```
```

5. 网络配置由于设置了错误的 IP 地址并删除了默认网关设置而被修改。打开 Network Manager 连接编辑器并手动还原原始配置。

6. 如果仍然遇到问题，从备份文件恢复配置：
```bash
cp /root/backup/*.nmconnection /etc/NetworkManager/system-connections/
reboot
```

# 124 第3章 基础网络管理

## 实验 2

这将禁用系统上所有的活动网络连接配置，并将其配置为重启后不连接。

1. 测试与本地和远程系统的连接，例如本地系统的主机或 FQDN 以及 `/etc/resolv.conf` 中的名称服务器地址：
   `# ping server1.example.com`
   `# ping 172.16.0`
2. 检查状态和 IP 设置：
   `# ip addr show`
   你应该看到接口没有 IP 设置。
3. 打开 Network Manager Editor 并检查连接设置：
   `# nmconnection-editor`
4. 列出活动连接。命令输出应该是：
   `# nmcli show --active`
5. 使用 Network Manager Editor 编辑连接配置，并确保勾选“自动连接”。这将恢复网络连接。
6. 如果仍然存在问题，从备份文件中恢复配置：
   `# cp /root/backup/*.nmconnection /etc/NetworkManager/system-connections/`
   `# reboot`

## 实验 3

本实验移除 DNS 客户端配置。你会发现 IP 连接正常，但名称解析失败。

1. 尝试 ping `www.google.com`。命令应该执行失败：
   `# ping www.google.com`
2. 这表示解析存在问题。如果你检查 `/etc/resolv.conf` 的内容，发现它是空的：
   `# cat /etc/resolv.conf`
3. 打开 Network Manager Editor，在 IPv4 设置标签页中手动编辑 DNS 服务器和域设置恢复原始配置。
4. 如果仍然存在问题，从备份文件中恢复配置：
   `# cp /root/backup/*.nmconnection /etc/NetworkManager/system-connections/`
   `# reboot`

![](img/9c00a7303da5bd3104553e10fe4d_160_0.png)

## 实验 4

在本实验中，你为第一章描述的每个系统设置了 `/etc/hosts` 文件。除了 Network Manager 添加的本地设置外，两个系统的 `/etc/hosts` 数据可能是相同的。具体来说，该文件应包含以下条目：

```
172.16.0.100 server1.example.com server1
172.16.0.050 tester.example.com tester
```

你的 IP 地址可能取决于第一章中讨论的虚拟机程序所设置的虚拟网络。只要数据一致，Network Manager 插入的数据重复并不是问题。事实上，可以为一个 IP 地址设置多个名称；例如，如果你在 `172.16.0.50` 系统上设置了 Web 服务器，你可以在 `/etc/hosts` 中添加以下条目：

```
172.16.0.50 www.example.com
```

完成配置后，从 `server1.com` ping `server1.example.com`（反之亦然）。`/etc/hosts` 中的名称解析应该是正常的：

```
# ping server1.example.com
# ping tester1.example.com
```

## 实验 5 和 6

这些是引导性练习，帮助你熟悉 `nmtui` 和 Network Manager Editor。你应该能够遵循所有步骤并进行配置更改。

1. 修改 IP 配置后，使用 `ping` 命令测试虚拟机之间的连接性（你的 IP 地址可能不同）：
   `# ping 172.16.0.101`
2. 作为额外任务，尝试在测试系统上配置 IPv6 地址。例如，在 `server1.example.com` 上配置 IPv6 地址 `fd00::1/64`，在 `tester1.example.com` 上配置 `fd00::2/64`，并确保从每个主机使用 `ping6` ping 对方的 IP 地址：
   `#`
3. 如果出现问题，可以从备份文件中恢复原始配置：
   `# cp /root/backup/*.nmconnection /etc/NetworkManager/system-connections/`
   `# reboot`

# 第 4 章

## 软件管理

| 认证目标 | | |
|---|---|---|
| 4.01 RPM 包管理器 | 4.04 模块流 (°)) | |
| 4.02 更多 RPM 命令 | ✓ 两分钟演练 |
| 4.03 依赖关系与 dnf 命令 | 问答自测 |

安装完成后、系统加固、文件系统配置完成以及其他初始设置任务完成后，你仍有工作要做。几乎在系统达到你理想状态之前，你会被要求安装或删除软件包。为了确保安装了正确的更新，你需要知道如何让系统与 Red Hat 订阅管理 (`RHSM`) 或与重建发行版相关的仓库工作。

为了完成这些任务，你需要详细了解如何使用 `rpm` 和 `dnf` 命令。虽然这只是“两个”命令，但它们包含非常丰富的细节。有整本书都专门讲解 `rpm`。

### 考试内部

#### 管理技能

由于管理 RPM 是一项基础技能，你应该预期掌握：

- 安装和更新软件
- 使用模块流工作
- 管理配置文件

### RPM 软件包管理器

每个存储库在 `repodata/` 子目录下包含一个软件包数据库。该数据库包含每个软件包的信息，并允许安装请求包含所有依赖项。如果您有 RHSM 订阅，则在 `/etc/dnf/plugins` 目录下的 `product-id.conf` 和 `subscription-manager.conf` 中启用对 Red Hat 存储库的访问。这些文件将在本章稍后部分进行讨论。

依赖项是为了确保目标软件包的所有功能都能按照设计要求工作而需要安装的软件包。

#### 安装 RPM 软件包

有三个基本命令可以安装 RPM。如果 RPM 需要任何依赖项，这些命令将无法工作。例如，如果您没有安装 SELinux 策略 DBUS (`policycoreutils-dbus`) 和开发工具包 (`policycoreutils-devel`)，但尝试安装 SELinux 配置 GUI (`policycoreutils-gui`)，您将收到以下消息（版本号可能有所不同）：

```bash
# rpm -i policycoreutils-gui-3.4-4.el9.rpm
error: Failed dependencies:
  policycoreutils-dbus = 3.4-4.el9 is needed by --
  policycoreutils-gui-3.4-4.el9.noarch
  policycoreutils-devel = 3.4-4.el9 is needed by --
  policycoreutils-gui-3.4-4.el9.noarch
```
