
Repo URL: https://cdn.redhat.com/content/dist/hel9/release/x86_64/appstream/os

Enabled: 1

9. 你可以使用以下命令启用额外的存储库：
```bash
# subscription-manager repos --enable=REPOID
```

10. 使用以下 `dnf` 命令确认系统已订阅到 BaseOS 和 AppStream 存储库：
```bash
# dnf repolist
```
命令输出应类似于：
```text
Updating Subscription Management repositories.

repo id repo name

hel-9-x86_64-appstream-rpm Red Hat Enterprise Linux for x86_64 AppStream (RPMs)

hel-9-x86_64-base-rpm Red Hat Enterprise Linux for x86_64 BaseOS (RPMs)
```

11. 系统现在准备好安装新软件包。尝试运行以下命令安装软件包：
```bash
# dnf install wireshark
```
结果应类似于所示。在此示例中，`dnf` 命令不仅下载并安装了 `wireshark` RPM，还安装了依赖包以满足所有的软件依赖。
```text
Updating Subscription Management repositories.

Last metadata expiration check: 2:15:00 ago on Mon 15 May 2023 01:45:27 AM CDT.

Dependencies resolved.

| Package | Version | Repository | Size |
| :--- | :--- | :--- | :--- |
| Installing: wireshark | 1:3.4.10-el9 | hel-9-for-x86_64-appstream-rpm | 3.9 M |
| Installing dependencies: | | | |
| libsmi | 0.4.10-el9 | hel-9-for-x86_64-appstream-rpm | 2.2 M |
| openssl | 1.19.1-el9 | hel-9-for-x86_64-appstream-rpm | 539 K |
| pre-rex | 0.6.3-el9 | hel-9-for-x86_64-appstream-rpm | 20 M |
| qt-base | 5.15.3-el9 | hel-9-for-x86_64-appstream-rpm | 3.7 M |
| qt-base-common | noarch | hel-9-for-x86_64-appstream-rpm | 13 K |
| qt-base-devel | 5.15.3-el9 | hel-9-for-x86_64-appstream-rpm | 6.1 M |
| qt-declarative | 5.15.3-el9 | hel-9-for-x86_64-appstream-rpm | 4.2 M |
| qt-multimedia | 5.15.3-el9 | hel-9-for-x86_64-appstream-rpm | 822 K |
| wireshark-cli | 3.0.7-el9 | hel-9-for-x86_64-appstream-rpm | 18.2 M |
| xcb-util-image | 0.4.19-el9 | hel-9-for-x86_64-appstream-rpm | 22 K |
| xcb-util-keysym | 0.4.0-179 | hel-9-for-x86_64-appstream-rpm | 16 K |
| xcb-util-renderutil | 0.3.20-el9 | hel-9-for-x86_64-appstream-rpm | 20 K |
| xcb-util-wm | 0.4.1.22-el9 | hel-9-for-x86_64-appstream-rpm | 35 K |
```

# 基础 dnf 配置

现在你进入了细节部分。它从 `/etc/dnf/dnf` 配置文件开始，并继续 `/etc/dnf` 和 `/etc/yum.repos.d` 目录下的文件。如你所，尽管 `dnf` 是当前的工具，但目录名称仍然带有 `yum` 字样。要获取 `dnf` 配置指令完整列表及其当前值，请运行以下命令：
```
# dnf config-manager --dump
```

## 基础 dnf 配置文件：dnf.conf

本节逐行分析 `/etc/dnf/dnf.conf` 文件的默认版本。虽然在大多数情况下你不会对此文件进行更改，但如果出现问题，你至少需要理解文件中的标准指令。以下行直接节选自该文件的默认版本。第一个指令是一个包头：`[main]` 包头意味着后续的所有指令都全局作用于 `dnf`：
```
[main]
```
`gpgcheck` 布尔值指令使 `dnf` 命令实际上会检查下载软件包的 GPG 签名：
```
gpgcheck=1
```
`installonly_limit` 指令指定了 `installonlypkgs` 选项中列出的软件包（通常是内核）可以同时安装的数量：
```
installonly_limit=3
```
`clean_requirements_on_remove` 布尔值指令允许 `dnf` 在删除软件包时检查每个软件包的依赖关系。如果此配置设置为 `true`，任何不再被其他软件包需要的依赖项也将被移除。
```
clean_requirements_on_remove=True
```
如果启用，`best` 指令会告诉 `dnf` 在升级期间始终尝试安装软件包的可用最高版本：
```
best=True
```

## `/etc/dnf/plugins` 目录下的配置文件

`/etc/dnf/plugins` 目录下的默认文件配置了 `dnf` 与 Red Hat Portal 或 Satellite 服务器之间的连接。如果你正在学习如 AlmaLinux 这样的 RHEL 重构型发行版，你会在该目录下看到一组不同的文件。然而，这是一本关于 Red Hat 的书，重点将放在 RHEL 9 安装中的两个基础文件上。

### 依赖关系与 dnf 命令

#### Spacewalk 插件

如果你通过旧版本的 Red Hat Satellite Server 订阅订阅了 RHEL，那么该目录下的 `spacewalkplugin.conf` 文件尤为重要。接下来显示的指令启用了该插件并检查 RPM 包的 GPG 签名：
```
[main]
enabled = 1
gpgcheck = 1
timeout = 120
```

#### Red Hot 订阅管理插件

`subscription-manager.conf` 和 `product-id.conf` 文件旨在通过订阅管理将 `dnf` 系统连接到 Red Hat Portal。正如本章讨论，订阅管理用于将系统订阅到 RHEL 以进行系统更新。`subscription-manager.conf` 文件非常直观。第一个指令启用该插件。最后一个指令如果设置，将禁用所有未受订阅管理管理的仓库。当系统运行 Fedora 且你不想使用默认系统仓库（因为系统由 Red Hat Satellite 或 Katello 管理）时，此设置非常有用。
```
[main]
enabled=1
disable_system_repos=0
```
