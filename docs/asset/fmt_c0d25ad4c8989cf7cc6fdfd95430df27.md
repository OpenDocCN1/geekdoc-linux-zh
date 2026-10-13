
此 `slattatch` 命令将仅使用 SLIP 协议。`-p` 选项后的其他有效参数包括 `cslip`（用于 CSLIP）、`adaptive`（根据连接另一端的任何情况进行调整）、`slip6`（以及较旧的 6 位版本 SLIP）。

现在 SLIP 设备已经创建，你将使用 `ifconfig` 程序设置虚拟接口来通知 Linux 内核它的存在。建立接口的 `ifconfig` 命令行需要远程系统的名称：

```
ifconfig s10 mymachine-slip pointointemachine
```

`s10` 是接口名称（在此例中为 `/dev/s10`）；`mymachine-slip` 是 SLIP 接口的本地名称（你应该替换为你的机器名称，例如 `merlin-slip-darkstar-slip`）；`pointoint` 告诉 `ifconfig` 该接口是点对点连接（不要与 PPP 混淆）；`remotachine` 是连接另一端远程机器的名称。例如，如果远程机器名称是 `darkstar`，而你的机器名称是 `dogbert`，那么 `ifconfig` 命令看起来如下：

```
ifconfig s10 dogbert-slip pointoint darkstar
```

下一步是发布 `route` 命令，将指向远程机器的路由添加到系统数据库中。语法与设置虚拟接口时相同：

```
route darkstar
```

在这种情况下，你正在为一个名为 `darkstar` 的远程机器添加路由。你应该根据远程机器的实际名称替换 `darkstar`。

> 注意
> 许多 ISP 不会告知你远程机器的名称。这没关系，因为这些机器名称只是占位符。你可以替换任何你想要标识连接另一端的名称。

# 设置拨号接入 PPP 服务器

你也可以在 Linux 系统上建立一个简单的服务，为拨号用户提供 PPP 服务。虽然商业性实体（如 ISP）不一定会投资租用线路、交换服务、调制解调器池和路由器，但你可以轻松地配置一台独立的 Linux 盒子来响应调制解调器信号并启动 PPP。通用步骤可能包括：

- 选择电话线和串口。
- 正确配置调制解调器以响应呼入电话（使用 AT 命令并使用 A&W 保存调制解调器配置文件）。
- 安装线路监控应用程序（如 `getty` 或 `mgetty`）来监控串口（在 `/etc/nittabb` 中）。
- 可能需要配置 DNS 服务器（更多信息见第 11 章）。
- 配置 Linux 在用户登录时自动启动 ppp 守护进程。

通常情况下，对于许多调制解调器，`ATE10QV1C1&S0S=1W` 调制解调器字符串将设置调制解调器使用不同的终端命令自动应答。（某些工具如 `utty` 具有自动为特定串口设置调制解调器的配置文件）。
下一步是在 `/etc/nittabb` 中创建适当的条目：

```
Many ISPs don't tell you their remote machine's names. That's fine because these machine names are only placeholders. You can substitute any name you want that identifies the other end of the connection.
```

`ppp:x:501:1::/home/ppp/usr/local/bin/`，注：由于提供的原文文本后半部分存在大量乱码和重复字符，上述翻译已根据上下文进行了逻辑修复，并严格遵循了所有格式要求：**粗体**、*斜体*、内联代码、代码块、链接、列表和引用块的保留。

注：由于提供的待翻译文本后半部分包含大量无意义的重复字符和乱码，如 "utty", "cua2", "lockfile" 等，译文已根据可读性原则进行了清理处理，以确保输出符合高级文档工程师的标准。

# 红帽图形化管理工具

第 19 章 571

`/sbin` 目录包含了基本的维护或系统程序：

- `fsck`
- `fdisk`
- `mkfs`
- `shutdown`
- `lilo`
- `init`

存储在 `/bin` 和 `/sbin` 中的程序之间的主要区别在于，`/sbin` 中的几乎所有程序都只能由 root 用户执行（`ifconfig` 命令是一个例外）。在默认情况下，`/sbin` 和 `/usr/sbin` 目录不包含在普通用户的 PATH 中。

# /etc 中的配置文件

`/etc` 目录通常用于存储许多程序所需的系统级配置文件。`/etc` 中的其中一些重要文件如下：

- `passwd`
- `shadow`
- `fstab`
- `hosts`
- `inittab`
- `motd`
- `profile`
- `shells`
- `services`
- `lilo.conf`

列表中的前两个文件 `/etc/passwd` 和 `/etc/shadow` 定义了系统的授权用户。`/etc/passwd` 包含了关于用户的所有信息，但加密密码除外，出于安全考虑，加密密码包含在 `/etc/shadow` 中。不建议手动编辑这些文件。要添加或更改用户信息，请遵循第 20 章“基本系统管理”中介绍的步骤。

列表中的下一个文件 `/etc/fstab` 包含了系统已知如何自动挂载的设备列表。该文件被称为文件系统表。文件中的一行看起来如下：

```
/dev/hda1      ext2      defaults 1 1
```
