

- 5. 运行 `make` 命令来开始编译 Samba：

```bash
[root@server source]# make
```

- 6. 接下来，运行 `make install`：

```bash
[root@server samba-4]# make install
```

你将发现所有的 Samba 二进制文件和配置文件都安装在 `/usr/local/samba/` 目录下。你可以像通过 RPM 安装 Samba 一样继续使用它们。

你应该注意，`/usr/local/samba/bin` 目录通常不在大多数 shell 的搜索路径中。你可以将其添加到你的路径中，或者简单地将二进制文件从 `/usr/local/samba/bin` 复制到会被搜索的位置（例如 `/usr/sbin/` 或 `/usr/bin/`）。

## Samba 配置 (--configure) 选项

### 描述

| 选项 | 描述 |
| :--- | :--- |
| --prefix=PREFIX | |
| --with-pam |  PAM 支持（默认 = no）。 |
| --with-ads | Active Directory 支持（默认 = auto）。 |
| --with-ldap | LDAP 支持（默认 = yes）。 |
| --with-pam_smbpass | 构建用于对密码后端认证的 PAM 模块。 |
| --with-systemd | 启用 systemd 集成 / 禁用 systemd 集成。 |
| --enable-cups | 开启通用 UNIX 打印系统 (CUPS) 支持（默认 = auto）。 |

表 24-1 常用 Samba 配置 (--configure) 选项

## Samba 管理

本节描述了一些典型的 Samba 管理功能。你将学习如何启动和停止 Samba，如何使用 Samba 执行常见的管理任务，如何使用 smbclient 等。

## 启动和停止 Samba

大多数 Linux 发行版都带有脚本和程序，可以启动和停止 Samba 而无需任何特殊操作。它们会处理启动时的启动和关机时的停止。在我们通过 RPM 安装 Samba 的运行 systemd 的 Fedora 示例系统上，`systemctl` 工具可以管理 Samba 的启动和停止。

例如，要启动 smbd 守护进程，你可以执行此命令：

```bash
[root@server ~]# systemctl start smbd.service
```

停止该服务，输入：

```bash
[root@server ~]# systemctl stop smbd.service
```

在对 Samba 进行任何配置更改后，你可以使用此命令重启它以使更改生效：

```bash
[root@server ~]# systemctl restart smbd.service
```

默认情况下，该服务可能在下次重启时不会自动启动。对于像 Fedora 等启用 systemd 的 Linux 发行版，你可以使用 `systemctl` 命令来确保 samba 单元在系统启动时自动启动，只需输入：

```bash
[root@fedora-server ~]# systemctl enable smbd.service
```

> 在未使用正确脚本的情况下停止 Samba 稍微复杂一些。但通常情况下，你可能需要使用 `ps` 命令列出所有的 Samba 进程。从列表中找到由 root 拥有的 samba 实例并杀掉该进程。这将杀死所有其他 Samba 连接。

- 你可以通过以下命令从命令行启动我们之前从源码安装的 Samba 守护进程：
```bash
# /usr/local/samba/sbin/smbd -D
```
这里使用的唯一命令行参数 (-D) 告诉 smbd 作为守护进程运行。

以相同的方式启动 nmbd：
```bash
# /usr/local/samba/sbin/nmbd -D
```

## 创建共享

我们将演示在 `/tmp` 目录下创建一个并在 Samba 上共享目录的第一个过程。我们将首先创建要共享的目录，然后编辑 Samba 的配置 (etc/samba/smb.conf) 来为该共享创建一个条目。

如果你安装并运行了任何主流的图形化桌面环境，你通常可以使用环境内置的工具来完成 Samba 的简单文件共享任务，或使用任何可用的 Web 工具来管理你的 Samba 服务器。然而，了解如何以最原始的形式配置 Samba 对你非常有帮助，这会让你更容易理解 GUI 工具在后台做了什么。此外，你永远不知道自己何时会被困在没有任何 GUI 配置工具的亚马逊亚马逊丛林中。因此，让我们开始吧：

- 在 `/tmp/` 文件夹下创建一个名为 `testshare` 的目录：
```bash
[root@server ~]# mkdir /tmp/testshare
```

- 在步骤 1 创建的目录下创建一些空文件（foo1, foo2, moo3）：
```bash
[root@server ~]# touch /tmp/testshare/{foo1,foo2,moo3}
```

- 设置 `testshare` 文件夹的权限，以便系统上的其他用户可以浏览其内容：
```bash
[root@server ~]# chmod -R 755 /tmp/testshare
```

- 使用文本编辑器打开 Samba 配置文件 (/etc/samba/smb.conf) 进行编辑。滚动到文件末尾，在文件底部添加列出的条目。（请忽略仅为了可读性而添加的 1–5 行号。）

```ini
[samba-share]
comment=This folder contains shared
path=/tmp/testshare
guest ok=yes
writable=no
```

> 在 Samba 术语中，“service”是 SMB 客户端在尝试浏览 Samba 服务器上的共享时看到的名称。第 2 行是用户在浏览时看到的 comment。第 3 行非常重要。它指定了文件系统上存储共享的位置。第 4 行是 guest ok。第 5 行是 writable。

> 了解如何以最原始的形式配置 Samba 对你非常有帮助，这会让你更容易理解 GUI 工具在后台做了什么。此外，你永远不知道自己何时会被困在没有任何 GUI 配置工具的亚马逊丛林中。因此，让我们开始吧：

（注：第 4-5 行翻译根据上下文逻辑推断，原文中未提供完整描述，此处保持格式对应）

（注：由于原文文本包含部分重复或重复或乱码，，根据指令，译文已翻译翻译逻辑）

