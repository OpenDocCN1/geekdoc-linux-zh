
- 6. 回到你的 Windows 95 电脑，双击“网络邻域”中的 `Linux-Samba` 电脑图标。你应该看到一个标记为 `etc` 的图标——除了 `root` 图标之外。双击 `etc` 图标，你应该看到 `/etc` 目录，如图 6-5 所示。

## 第 6 章：通过示例自定义你的 Samba 服务器

## 223

![](img/29df11d9c5c608cff7b4fa65d0c78e37_246_0.png)

图 6-5：显示 `/etc` 目录的内容。

7. 运行 `smbdstatus` 命令显示 Samba 如何识别你。结果应该类似于列表 6-10 所示。

列表 6-10：执行 `smbdstatus` 的结果

`Samba version 1.9.17p4`

| Service | uid | gid | pid | machine |
| --- | --- | --- | --- | --- |
| etc | root | root | 126 | maggie (192.168.1.2) Fri Dec 12 20:27 |

没有锁定的文件

- 8. 在我的情况下，Samba 将我识别为用户 – 组 – `root`，从名为 `maggie` 的机器连接进来。我正在使用 `[etc]` 服务，该服务指向 `/etc` 目录（`smbdstatus` 输出中未显示）。
- 9. `/etc` 目录由 `root` 所有，`root` 写入权限。如果你对 `smb.conf` 文件进行长列表 – `ls -l /smb.conf` – 你会看到只有 `root` 写入权限：

```
-rw-r--r-- 1 root root 6549 Dec 12 20:19 smb.conf
```

- 10. 在你的 Windows 95 电脑上双击 `smb.conf` 图标以打开 `smb.conf` 文件。

## 224 第三部分：重要的客户端-服务器网络

- 11. 然而，如果你尝试以任何方式修改该文件，你会得到如图 6-6 所示的响应。尽管 Samba 将你识别为 `root` 且 `root` 拥有 `smb.conf`，但你无法操作它。

![](img/29df11d9c5c608cff7b4fa65d0c78e37_247_0.png)

- 12. 如果你想进行实验，可以关闭只读选项并将 `[etc]` 更改为可写。

## 看看你做了什么

> 挂载点可能会让人困惑。挂载点（例如 `/mnt/cdrom`）只是简单的目录。你可以像使用其他目录一样使用它们。但是，当你使用它们来挂载另一个设备时，在卸载该设备之前，其内容将是不可的。

## 第 6 章：通过示例自定义您的 Samba 服务器

1997年5月版《系统管理员》杂志有一篇名为《Samba — 调整 NT/UNIX 之舞》的文章，提供了一个简洁且信息丰富的教程，介绍了如何配置 Samba 以供 Windows NT 使用，它似乎也非常适用于 Windows 95。它有一个有趣的特性，即包含了一个 `smb.conf` 模板，你可以在其中取消你所需的服务的注释。作者 Mark Nassal 还提供了一个基于菜单的 `smb.conf` 配置系统，你可以通过以下 URL 访问：

```
http://www.tlac.net/users/nassalm/index.html
```

我刚刚尝试了一下它，并创建了几个运行良好的简单示例。请看一看。

## 创建需要进行 Linux 更改的 Samba 共享

接下来的 Samba 示例需要添加用户共享和打印机共享。添加用户和打印机共享要求 Linux 显式识别用户和打印机。因此，你需要了解一些 Linux 管理任务。现在是处理这些任务的好时机，因为你已经很久没有碰过 Linux 了。

## 向 Linux 中添加用户

为了提供 Samba 共享，你必须向你的 Linux 添加一个或多个用户。用户定义在 `/etc/passwd` 和 `/etc/group` 文件中。

Red Hat 建议你使用控制面板管理工具的用户配置 GUI，或者使用命令行程序 `/usr/sbin/useradd` 和 `/usr/sbin/userdel` 来添加、删除和修改用户。这两种都是好方法，但用户配置功能运行在 X 下（我还没有介绍过，有关配置 X 的更多信息，请参见第 7 章“使用 Xconfigurator 配置 X Window 系统”部分），我更希望你至少手动操作一次，以理解添加用户需要执行的操作。现在，我将解释密码文件，并提供修改 `/etc/passwd` 和 `/etc/group` 文件以添加用户的指令。

所有 Linux 发行版具有相同的 `/etc/passwd` 文件格式，字段用冒号 (:) 分隔，顺序如表 6-1 所示（表中的第一项对应最左侧的项目，最后一项对应最右侧的项目）。

## 第三部分：重要的客户端-服务器网络

| 表格 6-1 `/etc/passwd` 文件格式 |
| 字段 | 说明 |
| :--- | :--- |
| 登录名 | 用户登录系统时名称。 |
| 加密密码 | 如果用户没有密码，则此字段为空。星号 `*` 表示非登录账户。否则，此字段将显示一组看似随机的字符组合，代表加密后的密码。（如果你使用 shadow 密码，加密密码将移动到 `/etc/shadow` 文件，该文件除 `root` 外任何人不可读取，因此更安全。） |
| 用户 ID (UID) | 在 `passwd` 文件中设置后，用户标识数字与登录名相对应。可以使用 `ls` 命令配合 `-n` 和 `-l` 选项来显示数字用户 ID（即 `ls -n -l` 或 `ls -nl`）。 |
| 组 ID (GID) | 默认组标识数字。该数字标识用户所属的默认组；然而，你可以属于多个组，但 Red Hat 使用个人组惯例，即每个用户属于一个唯一且排他的组。过去，用户可能属于一个或多个通用组，这导致了问题。组定义在 `/etc/group` 文件中。 |
| 姓名和/或注释 | 此可选字段应包含用户的全名和其他相关信息，如办公室地点、电话号码和寻呼号码（这对系统管理员特别重要）。用逗号分隔这些信息。 |
| 主目录 | 用户的默认目录。 |
| Shell | 你的默认登录 shell。所有 Linux 发行版（包括 Red Hat）都包含 `bash`，`bash` 是 Linux 世界中最常用的 shell。你可以将 shell 更改为 `ksh`、`csh`、`sh` 或你任何想要或需要的 shell，并访问 |

列表 6-13 显示了 Red Hat 提供的默认 `/etc/passwd` 文件。大多数 Linux 发行版在前十个左右的用户中使用相同的登录名、用户 ID 和组 ID（但在某些目录上有所不同）。从那里开始，发行版根据其自己的需求而异。不要担心，细节可能会不同，但它们是供系统使用的，不会影响你的设置。

## 第 6 章：通过示例自定义您的 Samba 服务器

列表 6-13：定义所有用户的 `/etc/passwd` 文件

```
root:yTSdWTprhi7u:0:0:root:/bin/bash
bin*:1:1:bin:
demon:2:2:daemon:/sbin:
adm*:3:4:adm:/var/adm/
lp*:4:7:lp:/var/spool/lpd
sync*:5:0:sync:/sbin/sync
shutdown*:6:0:shutdown:/sbin/sbin/shutdown
halt*:7:0:halt:/sbin/halt
mail*:8:12:mail:/var/spool/mail:
news*:9:13:news:/var/spool/news
uucp*:10:14:uucp:/var/spool/uucp
operator*:11:0:operator:/root/
games*:12:100:games:/usr/games/
gopher*:13:30:gopher:/usr/lib/gopher-data:
ftp*:14:50:FTP User:/home/ftp
nobody*:99:99:Nobody/:
```
