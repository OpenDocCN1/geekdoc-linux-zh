
Total size: 476 k
Installed size: 1.1 M
Is this ok [y/n]:

你已经在本地 DVD 上设置了仓库。

- 15. 通过从 `/etc/yum.repos.d` 目录删除 `rhel9.repo` 文件来恢复原始配置。

## 第4章 软件管理

### 第三方仓库

其他组的的第三方开发者为 RHEL 9 创建了软件包。它们包含了某些红帽不支持的流行软件的软件包。这三个三方之一的网站可以在 https://docs.fedoraproject.org/en-US/epel/ 找到。

若要向系统添加第三方仓库，你会在 `/etc/yum.repos.d` 中创建一个自定义的 `.repo` 文件。

*(注：原文中存在大量重复的句子，关于创建 .repo 文件，已按要求翻译)*

其他组的第三方开发者为 RHEL 9 创建了软件包。它们包含了某些红帽不支持的流行软件的软件包。这三个三方之一的网站可以在 https://docs.fedoraproject.org/en-US/epel/ 找到。若要向系统添加第三方仓库，你会在 `/etc/yum.repos.d` 中创建一个自定义的 `.repo` 文件。 (此处省略重复部分)

要向系统添加第三方仓库，你会在 `/etc/yum.repos.d` 中创建一个自定义的 `.repo` 文件。 (此处省略重复部分)

EPEL (Extra Packages for Linux)

如果你要禁用 `/etc/yum.repos.d` 目录下的任何仓库，添加以下指令：

```
enabled=0
```

## 练习 4-3

### 从 RHEL 9 DVD 创建 dnf

此练习需要访问 RHEL 9 DVD。你将使用在第 1 章中安装的 `test1.example.com` 系统。该系统未订阅红帽订阅管理（如果已订阅，请运行 `subscription-manager unregister` 取消注册），你将创建一个 `dnf` 仓库来从 RHEL 9 DVD 安装本地软件包。

- 1. 在 VMware Workstation（或你的托管虚拟机程序）中，选择你的 `test1` 虚拟机并点击“设置”。
- 2. 挂载你在第 1 章中下载的 RHEL 9 ISO 文件。为此，在“设置”中选择“CD/DVD (SATA)”并点击“使用映像”。浏览并选择 RHEL 9 镜像的路径。确保选中了“连接”选项。

```
https://t.me/CCNA_SECURITY

https://t.me/CCNPSECURITY
```

- 3. 登录系统并输入 `df` 命令。如果 DVD 已自动挂载，你应该在 `df` 的输出中看到一个条目，显示 DVD 可位于如 `/run/media/yourusername/RHEL-9-1-0-BaseOS-x86_64` 的目录路径。如果由于原因没有看到 DVD 挂载，可以通过输入以下命令（作为 root）手动挂载它：

```
mount /dev/cdrom /media
```

在练习中，我们假设 DVD 挂载到 `/run/media/yourusername/RHEL-9-1-0-BaseOS-x86_64`。如果不是如此，请相应调整你的命令。

- 4. 导航到 `/etc/yum.repos.d` 目录。
- 5. 在文本编辑器中打开新文件并将其命名为（例如）`rhel9.repo`。
- 6. 编辑 `rhel9.repo` 文件。创建一个新的指令节。使用适当的节标题作为 `[rhel]`。
- 7. 指定 `BaseOS` 作为仓库的 `name` 指令。
- 8. 包含 `baseuri` 指令以设置：`file:///run/media/yourusername/RHEL-9-1-0-BaseOS-x86_64/BaseOS`。
- 9. 包含 `enabled=1` 指令。
- 10. 添加 `gpgkey=0`。
- 11. 保存并关闭文件。
- 12. 运行 `dnf clean all` 和 `dnf update` 命令。
- 13. 接下来，尝试以下命令：

```
# dnf install tmux
```

- 14. 如果成功，你应该看到以下输出：

|================================================================================|
| Package | Architecture | Version | Repository | Size |
|================================================================================|
| Installing: | | | | |
| tmux | x86_64 | 3.2a-4.el9 | rhel | 476 k |
|================================================================================|

```
=================================================================================

Transaction Summary

=================================================================================

Install 1 Package
```

Total size: 476 k
Installed size: 1.1 M
Is this ok [y/n]:

你已经在本地 DVD 上设置了仓库。

- 15. 通过从 `/etc/yum.repos.d` 目录删除 `rhel9.repo` 文件来恢复原始配置。

## 第4章 软件管理

### 第三方仓库

其他组的第三方开发者为 RHEL 9 创建了软件包。它们包含了某些红帽不支持的流行软件的软件包。这三个三方之一的网站可以在 https://docs.fedoraproject.org/en-US/epel/ 找到。若要向系统添加第三方仓库，你会在 `/etc/yum.repos.d` 中创建一个自定义的 `.repo` 文件。 (此处省略重复部分)

EPEL (Extra Packages for Linux)

如果你要禁用 `/etc/yum.repos.d` 目录下的任何仓库，添加以下指令：

```
enabled=0
```
