
`ln -s /etc/init.d/ypbind /etc/rc3.d/S13ypbind`

`ln -s /etc/init.d/ypbind /etc/rc5.d/S13ypbind`

这些命令行的结果是，启动时启动 `ypbind` 守护进程的脚本被分别添加到在运行级别 3 和 5 启动。

有关运行级别脚本的更多信息，请参阅第 12 章。

![](img/380d929a08ad0f9245d542259c5760b8_842_0.png)

## 将 Red Hat Linux 设置为 NIS 主服务器

要将你的 Red Hat Linux 系统配置为 NIS 主服务器，你应该首先将其配置为 NIS 客户端（即，设置 NIS 域名、设置 `yp.conf` 并按前述配置客户端守护进程）。然后你创建 NIS 映射并配置 NIS 服务器守护进程（`pserv` 和 `rpc.yppasswd`）。接下来的章节描述了这些过程。

### 选择 NIS 映射

要创建 NIS 映射以便你的 Red Hat Linux 系统成为 NIS 主服务器，请从终端窗口以 root 用户身份进入 `/var/yp` 目录。在该目录下，一个 `Makefile` 允许你配置哪些文件与 NIS 共享。默认共享的文件列在本章开头以及 `Makefile` 内部。

### 选择要映射的文件

如果你不想共享 `Makefile` 中设置的任何文件，可以阻止其被构建。你可以通过在 `Makefile` 中找到以下行，并简单在想要排除的文件前添加一个注释字符来实现：

```
all: passwd group hosts rpc services netid protocols ethers printcap \
# netgroup shadow publickey networks ethers bootparams \
# amd.home auto.master auto.local passwd.adj \
# timezone location netmasks
```

你可能会注意到 `all:` 行中的并非所有名称都代表精确的文件名。例如，`netgroup` 是 `/etc/netgroup` 文件。每个名称代表的文件列在 `Makefile` 中 `all:` 行的几行下方。你可能注意到许多文件已经被注释掉了，包括 `shadow` 文件。

> NIS-HOWTO 文档建议在 NIS 中使用 shadow 密码“始终是一个坏主意”。`Makefile` 中的（选项（在下一节中描述）允许你自动将 `shadow` 和 `gshadow` 文件分别合并到 `passwd` 和 `group` 文件中。

### 选择映射选项

在 `Makefile` 中，设置了几个选项。你可以选择更改它们或保持原样。以下是这些选项：

- `B=`：你可以使用 `B=` 选项允许 NIS 域名解析器找到不在当前域中的主机。默认情况下，未设置 `B=`。要开启此项功能，请将其设置为 `-b`（`B=-b`）。
- `NOPUSH=true` — 当设置为 `true`（默认值）时，`NOPUSH` 选项防止映射被推送到从服务器。这意味着 NIS 服务器是该 NIS 域的唯一服务器。将其设置为 `false`，并将从服务器的主机名放在 `/var/yp/pservers` 文件中，你不希望主 NIS 是该域的唯一服务器。
- `MINID=500`—为了防止为管理用户分配密码项，`MINID` 设置为 `500`。这假设你想要共享的系统中所有普通用户的 UID 都是 500 或以上。
- `MIGID=500`—为了防止为管理组分配密码项，`MIGID` 设置为 `500`。这假设你想要共享的所有普通组的 GID 都是 500 或以上。
- `MERGE_PASSWD=true`—如果你希望每个用户的密码从 `shadow` 和 `gshadow` 文件合并到 `passwd` 和 `group` 文件，请将此选项保持为 `true`。

*(注：原文文本存在大量重复和 OCR 错误，上述译文已根据逻辑内容进行了清理和整合)*

## 配置 NIS 服务器守护进程

NIS 服务器必须运行几个守护进程才能成为一个 NIS 服务器。Red Hat Linux 提供了若干运行级别脚本（run-level scripts），你可以配置这些脚本来启动 NIS 守护进程。这些脚本位于 `/etc/init.d` 目录，包含以下内容：

- `ypserver` — 该脚本启动 `ypserver` (`/usr/sbin/ypserver`) 守护进程。它从 `/etc/ypserver.conf` 文件读取信息以确定执行的操作。然后它监听网络上 NIS 客户端计算机的请求。
- `yppasswd` — 该脚本启动 `rpc.bypasswd` (`/usr/sbin/rpc.bypasswd`) 守护进程。该守护进程处理来自 NIS 客户端计算机想要更改用户密码的用户请求。

除非这些脚本被配置为在安装 Red Hat Linux 时在启动时运行，否则它们不会自动启动。你可以使用 SYSV 运行级别管理器（SYSV Runlevel Manager）来设置脚本自动启动。要打开 SYSV 运行级别管理器，请在终端窗口中（以 root 用户身份）输入以下命令：

```
/usr/X11R6/bin/tksys&
```

图 23-1 显示了 SYSV 运行级别管理器的窗口示例。

![](img/380d929a08ad0f9245d542259c5760b8_846_0.png)

图 23-1：通过 SYSV 运行级别管理器设置脚本自动启动。

我们感兴趣的运行级别是 3 和 5。级别 3 是 Red Hat Linux 默认启动的运行级别，而级别 5 是在你希望 Red Hat Linux 启动到图形登录界面时可能更改的级别。你可以在第 3 和第 5 列看到 `ypserv` 和 `yppasswd` 配置为在该级别停止。（你可能需要滚动 Start 列来找到这些脚本。）要让它们在运行级别 3 或 5 启动，你必须先从 Start 行中删除删除它们（点击每个脚本，然后点击 Remove）。按照以下步骤将它们添加到 Start 列：

1. 向下滚动 Available 列，当看到 `yppasswd` 时，点击它。
2. 点击 Add。出现一个 Add 弹出窗口，询问你是否要启动或停止 `yppasswd` 以及在哪些级别启动。
3. 在弹出窗口中，点击 Start `yppasswd`。
4. 点击数字 3 旁按钮。
5. 点击 Done。出现一个弹出窗口，询问在运行级别脚本列表中你是否想要启动这一个。它应该会推荐数字 6，这应该可以正常工作。
6. 点击 Add。`yppasswd` 脚本现在应该出现在 Start 行的第 3 列中。
7. 重复这些步骤将 `yppasswd` 设置为运行级别 5 启动。
8. 重复相同的步骤配置 `ypserv` 脚本。

> 注意：你只需要将 `yppasswd` 和 `ypserv` 添加到你启动的运行级别即可。如果你是启动到 GUI (X11)，则应仅对运行级别 5 执行上述操作。无论何种情况，请查看 `/etc/inittab` 的值以确定你的默认启动运行级别是什么。

此时，你可以从窗口同时启动这两个 NIS 脚本（从 Available 格中点击每一项，点击 Execute，然后点击 Start），或者重启系统。当系统在下次重启后启动时，`ypserv` 和 `rpc.bypasswd` 应该处于运行状态。

NIS 主服务器应该已经启动并运行。如果有任何 NIS 从服务器，你现在应该配置它们。

## 生成 NIS 映射数据库

要安装并构建 NIS 数据库，请运行 `ypinit` 命令。要启动 `ypinit` 程序，输入以下命令：

```
/usr/lib/yp/ypinit -m
```

`ypinit` 命令会自动选择你的主机名作为 NIS 服务器。之后，它会要求你添加从服务器。一个接一个添加；在输入最后一个从服务器后按 Ctrl+D。验证 NIS 服务器列表是否正确（输入 y）。

此时数据库已构建完成。在 `/var/yp` 中会创建一个以你的 NIS 域命名的新目录。例如，如果你的 NIS 域名是 `trident`，那么目录就是 `/var/yp/trident`。所有构建的映射（maps）随后都会放置在该目录下。

## 将 Red Hat Linux 设置为 NIS 从用服务器

要设置 NIS 从用服务器，你必须像配置 NIS 主服务器一样配置它，但有一个例外：你不是创建 NIS 映射，而是运行 `ypinit` 命令，以便 NIS 映射可以从服务器复制。你给 `ypinit` 提供的选项是 `-s master` 选项，其中 `master` 被替换为你的 NIS 主服务器名称。以下是运行 `ypinit` 的示例，NIS 服务器名为 `maple`：

```
/usr/lib/yp/ypinit -s maple
```
