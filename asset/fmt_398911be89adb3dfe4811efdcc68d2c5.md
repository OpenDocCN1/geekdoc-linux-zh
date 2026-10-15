
`root@romans` > `/usr/bin/testys` `/etc/smb.conf`

```

程序在运行时会向你告知状态：

```

Load smb config from

Processing section "homes]"

Processing section "printers]"

Processing section "home]"

```

如果你按下回车，`testpart` 将给出：

## 处理密码加密

如果你从 Windows 2000、补丁到 Service 3 或更高版本的 Windows 4.0、Windows 98 或 Windows 95-OSR/2 连接 Samba 服务器遇到困难，最可能的罪祸首是明文。

你需要自己决定密码加密（这带来了保存到不安全磁盘上的密码）还是明文传输（可能允许密码在网上被捕获）更适合你的情况。我倾向于从客户端启用明文，但如果你没有有效的方法为每个客户端自动化此过程，这是一个令人恼的步骤。

**使用明文密码** 如果你决定使用明文密码，请使用适用于平台的 `regedit` 命令，并更改表 9-3 中的值以允许 Windows 系统传输明文。

**Samba 密码加密** 如果你选择在 Samba 服务器上启用密码加密，按照以下步骤操作：

- 1. 在 `smb.conf` 文件的 `[global]` 部分添加以下行
```conf

crypt passwords=yes

```

| OS | 注册表项 | 名称和数据 |
|---|---|---|
| Win 2000 | `[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkStation\Parameters]` | `"EnablePlainTextPassword"=dword:00000000` |
| WinNT 4.0 | `[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Rdr\Parameters]` | `"EnablePlainTextPassword"=dword:00000000` |
| Win 98 | `[HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\VNETSUP]` | `"EnablePlainTextPassword"=dword:00000000` |
| Win 95 | `[HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\VNETSUP]` | `"EnablePlainTextPassword"=dword:00000000` |

**表 9-3.** 在微软操作系统上启用明文密码

## 第 8 章：第 6 ：与微软混在一起，与 Novell 联网

2. Red Hat 将 `smbpasswd` 密码文件存储在 `/etc/smbpasswd` 中。使用此命令确保该文件仅对 `root` 可读：

```
root@romans > ls -l /etc/smbpasswd

rw------- 1 root      root 208 May 12 14:01 smbpasswd
```

如果文件权限与在该行中看到的不符，请使用此命令进行修正：

```
root@romans > chmod 600 /etc/smbpasswd
```

3. 填充 `smbpasswd` 文件。虽然有一个 shell 脚本可以从 `/etc/passwd` 文件完成此操作，但我更倾向于有选择性地添加用户（也许现在是让你的用户纠正自己的账户的好时机，这样你就可以清理掉不需要的了？）。`smbpasswd` 程序可以毫不费力地完成这一点。

```
root@romans > smbpasswd -add karen honeybunny
```

这个命令很容易理解：它添加了一个名为 `karen` 的用户，并设置了极其容易记住的密码 `honeybunny`。你可以从你的用户账户列表和一些不错的工业级密码对这些添加操作进行脚本化。

4. 现在，你可以通过启用 `/etc/smbpasswd` 文件上的特殊用户 ID 权限，允许用户修改自己的密码：

```
root@romans > chmod u+s /etc/smbpasswd
```

现在你应该可以在你的 Samba 服务器及其客户端上使用这些加密后的密码了！

## 确保打印机被识别

也许我指出这一点有点操之过急了，因为我还没有在一个地方讨论所有的 Samba 信息，这里有一个简单的方法，可以确保 Samba 识别你认为它应该识别的打印机名称：使用 `testprns` 程序。给这个小工具提供你尝试访问的打印机名称，以及你 Linux 系统 `printcap` 文件的位置，它就会告诉你 Samba 是否知道如何使用打印机（我们将在第 10 章讨论 `printcap` 文件）。

```
millerm@romans > testprns lj4500 /etc/printcap
```

在这个示例中，我正尝试确定我认为名为为 `lj4500` 的打印机是否可以通过 `/etc/printcap` 中的信息进行访问。如果可以，我应该会看到这条消息：

Printer name lj4500 is valid.

但如果我记错了名称，我会得到另一条消息：

Printer name lj4500 is not valid.

## Windows 成瘾者的 Linux 之路：十二步程序

如果情况确实如此，那么我无法从 Windows 客户端找到打印机的原因是 Linux 系统不认识该名称的打印机。

## 连接到 Novell 系统

虽然连接基于微软的系统占据了本章的大部分，但我不想完全忽视 Novell 的 NetWare。我离开担任 NetWare 管理员的苦日子已经很多多年，以至于我对这个网络操作系统（NOS）感到相当淡然，而且事实是，自从我离开后，公司一直在改进其产品线。你可能有一些想要从你的 Linux 工作站访问的 NetWare 系统。如果你周围有 NetWare 客户端，你可能会发现，在某些情况下，让你的 Linux 系统模拟一个 NetWare 服务器比到处去修改每一个客户端要容易得多。因此，为了处于这两种情况的人考虑，我想谈谈解决这两个问题的方案。

## 作为客户端连接

如果你有正确的工具，从 Linux 客户端连接到 Novel 服务器是很容易的。也许在你的 NetWare 服务器卷上加载 NFS 命名空间是此此最简单的方法，但并不是所有人都有选择。坦率地说，Red Hat 有 `ncps` 包，它完全胜任这项工作的正确工具。如果你在构建内核时包含了 IPX 协议，并使用 `Linuxconf` 进行了配置（如第 7 章所述），那么你就稳妥了。

## 使用 ncpmount

如果 IPX 在你的系统中运行正常，你可以使用 `ncpmount` 从你的 Linux 系统挂载和卸载 NetWare 卷。例如，如果你想访问名为 `TITUS` 的 NetWare 服务器，你可以使用以下命令：

```
root@romans -> ncpmount -S TITUS -U supervisor /mnt/titus
```

这将提示你输入 `TITUS` 的密码；如果你输入得正确，你就可以从指定的挂载点 `/mnt/titus` 访问 `TITUS` 卷。`TITUS` 上的每个卷在挂载点都会有一个独立的子目录。

使用 `ncpmount` 连接到 NetWare 服务器时还有许多其他选项。表 9-4 描述了一些更实用的选项，但你可以查看 `man` 页面以获取更多细节。

通过包含传递密码等功能，`ncpmount` 给了你完全脚本化 Linux 和 NetWare 系统之间连接的机会，尽管这自然意味着你必须保护脚本，特别是如果你计划使用 NetWare Supervisor 密码的话。

## 第 9 章：第 6 ：与微软混在一起，与 Novell 联网

| 选项 | 描述 |
| :--- | :--- |
| `-S server` | NetWare 服务器名称 |
| `-U username` | 登录 NetWare 服务器的用户名 |
| `-P password` | NetWare 用户账户的密码 |
| `-V volume` | 要挂载的卷（默认挂载所有卷） |
| `-b` | 强制 |
| `-u uid` | 用户 ID |
| `-g gid` | 组 ID |
| `-f mode` | 文件模式 |
| `-d mode` | 目录模式 |

表 9-4：常用的 `ncpmount` 选项

通过包含传递密码等功能，`ncpmount` 给了你完全脚本化 Linux 和 NetWare 系统之间连接的机会，尽管这自然意味着你必须保护脚本，特别是如果你计划使用 NetWare Supervisor 密码的话。

## Windows 成瘾者的 Linux 之路：十二步程序

第一行提供了默认连接，将尝试连接到服务器。第一行可以由一个命令调用：

```
garsoto@james > ncpmount /mnt/titus own
```

第二行指定了具有相同用户名的不同服务器，并为该用户名提供了密码。连接到此服务器的命令可能如下：

```
garsoto@james > ncpmount -S TITHY /mnt/timothy
```

最后，最后一个选项使用连字符表示 `GUEST` 账户不需要密码。根据你的环境，文件可以让生活变得更容易，或者没有任何优势。

## 作为服务器运行

如果说如何连接 NetWare 服务器是本书关注的边缘，那么完全可以说 NetWare 仿真是在范畴之外。这是一个足够酷的功能，值得简要提及。但 Martin Stover 的模拟 NetWare 的 `mars_nwe` 包包含在 Red Hat 中，你可能对此尝试。

在你的 Linux 机器上设置 `mars_nwe` 包以模拟 NetWare 服务器需要两个简单的步骤。首先，你应该配置 `/etc/nwserver.conf` 文件以满足你的需求。其次，你需要启动服务。

## 配置 nwserver.conf

如果你在 Red Hat 服务器上安装了 `mars_nwe` 包，`/etc/nwserver.conf` 文件就会默认存在。它有详尽的注释，所以你应该能够遵循文件的布局逻辑。以下几行是一个极简的版本，包含了我所用系统中 `nwserver.conf` 文件的未注释部分：

```
# 定义一个只读的、小写的 SYS 卷

1 SYS /var/mars/nwe/sys

# 定义一个只读的、小写的、可移动媒体 CDROM 卷

1 CDROM /mnt/cdrom2

# 定义一个文件名全小写的 HOME 卷

1 HOME /home

# NetWare 服务器名称为 ROMANS828

2 ROMANS828

# 自动配置内部网络号和节点

3 auto 1

# 自动设置网络号和设备，设置帧类型和交付技巧

4 0x0 * snap 1
```

## 第 8 章：第 6 步：与微软交流，与诺威联网

```
5 0

# 声明为 NetWare 3.11 服务器

6 1

# 强制通用密码加密

7 0

# 将默认 UID 和 GID 设置为 'nobody'

10 99

11 99

# 将 SUPERVIS 用户与密码及 Linux 账户关联

12 SUPERVISOR nw-super a8g3RT39A

# 关联 NetWare 和 Linux 之间的登录名称

13 WIINNKA ian

# 不要使用临时方案将 Linux 登录映射到 NetWare 登录

15 0

# 在启动时进行简单的合理检查

16 1

# 配置 NetWare 打印到 Linux 打印机

21 LP SYS:/PRINT/LP 1pr -Plp

# 设置调试信息 - 保留推荐的默认值

100 0

101 1

102 0

103 0

104 0

105 0

106 1

# 将 nwserv 作为守护进程运行，启用日志并追加到日志文件

200 1

201 /var/log/mars_nwe.log

202 0

# 在发出关闭命令 15 秒后关闭服务器

210 5

# 每 120 秒发布一次广播

211 120

# 每 5 次广播记录一次路由信息，每次重写日志文件

300 1

301 /var/run/mars_nwe.routes

302 1

# 不使用看门狗

310 -1

# 定义特殊站点文件 ...

400 /etc/nwserv.stations

# ... 但通过获取最近的响应来忽略它
```

# Windows 痴迷者的 Linux：12 步计划

```
# 曾经给过的“请求最近的服务器”

401 0
```
