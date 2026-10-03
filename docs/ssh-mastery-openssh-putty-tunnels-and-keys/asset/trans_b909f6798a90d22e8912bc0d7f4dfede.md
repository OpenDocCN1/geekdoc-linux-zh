
在考虑连通性时，你可能希望对所有内容都使用 IPv6。这里我故意禁用 IPv4。

```
AddressFamily inet6
```

你可以使用 -4 命令行选项仅使用 IPv4。

```
$ ssh -4 lust
```

使用 -6 强制 IPv6。

## 设置源地址

具有单个接口上多个 IP 地址的主机默认从该接口的主 IP 地址发起所有连接。这并不总是理想的。服务可以从一台主机迁移到另一台主机，通常独立于任何防火墙更改。你可以通过 ssh_config 中的 BindAddress 关键字告诉 ssh 使用除主地址之外的源 IP 地址。

```
BindAddress 192.0.2.91
```

BindAddress 必须附加到本地机器。

BindAddress 没有方便的命令行标志。你必须使用 -o 指定它。

## OpenSSH 主机密钥缓存

OpenSSH 客户端会在 $HOME/.ssh/known_hosts 中记录用户批准的主机密钥。每个密钥在 known_hosts 中单独占一行，大致如下。

```
wrath.mw1.io ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTI t...
```

每一行包含机器的主机名（wrath.mw1.io）、主机密钥类型（ecdsa-sha2-nistp256）和公钥本身。

## 密钥缓存

你希望如何更新你的密钥缓存？在某些环境中，用户必须手动验证主机密钥，然后手动将它们添加到密钥缓存中。在其他环境中，自动将新密钥添加到缓存是可以接受的。最常见的是，用户希望 ssh 询问它应该怎么做。StrictHostKeyChecking ssh_config 选项告诉 ssh 如何处理新的主机密钥。

如果你希望 ssh 拒绝连接到 known_hosts 中没有条目的任何主机，请将 StrictHostKeyChecking 设置为 yes。客户端连接的唯一方法是将主机密钥添加到 known_hosts，很可能是从系统管理员提供的中央存储库中获取。这在主机密钥自动分发的环境中最有意义。

如果你处于相反的极端，并且无论主机密钥多么重要都永远不会验证它，那么你也可以将 StrictHostKeyChecking 设置为 accept-new。这告诉 ssh 盲目地用收到的每个新密钥更新 known_hosts。这相当于从不费心给你的家、汽车、办公室和银行保险库上锁——它可能感觉轻松自由，但迟早有人会<|start|>对你的个人物品做出不文明的举动。

默认设置 ask 告诉 ssh 呈现任何未知密钥并询问用户该怎么做。你可以验证密钥、接受它并让 ssh 将其添加到 known_hosts，或拒绝主机密钥。

选择最适合你环境的选项。你的笔记本电脑可能的需求与 NSA 或犯罪集团运行的服务器不同，而所有这些又都与你在测试实验室中的编排系统不同。

## 缓存安全：哈希 known_hosts

known_hosts 文件对入侵你桌面的入侵者非常有用；它是一个方便的 SSH 服务器目标列表。由于你的 SSH 服务器可能共享一个共同的系统管理员，用于渗透你桌面的技术可能适用于这些服务器中的任何一个。此外，系统管理员和其他用户可以查看 known_hosts 的内容。防止窥探的最佳方法是更改 known_hosts，使其不再包含主机名列表。通过哈希主机名来实现这一点，就像 /etc/passwd 对密码所做的那样。

如果你用哈希替换主机名，没有人可以从文件中读取主机名，也无法反向计算主机名。然而，当你连接到主机时，ssh 可以轻松计算服务器主机名的哈希并在 known_hosts 中查找该哈希。

一个哈希的 known_hosts 条目看起来像这样。

```
|1|PBM07JCRBJfg8qOz1BokTtCD1y0=|DVXu0IFq/dC4GMfEbFVkhptVjQ= ecdsa-sha2-nistp256 AAAAE2VjZ...
```

如果你检查该条目，你会看到密钥算法和主机密钥指纹进一步向下。

要让 ssh 自动哈希添加到 known_hosts 的新主机密钥，请使用 ssh_config 关键字 HashKnownHosts。

```
HashKnownHosts yes
```

这不会哈希现有条目。然而。使用 -H 标志对 ssh-keygen(1) 来哈希你现有的 known_hosts。

```
$ ssh-keygen -H
/home/mwlucas/.ssh/known_hosts updated.
Original contents retained as /home/mwlucas/.ssh/known_hosts.old
WARNING: /home/mwlucas/.ssh/known_hosts.old contains unhashed entries
Delete this file to ensure privacy of hostnames
```

哈希你的 known_hosts 会将现有缓存复制到 known_hosts.old，然后对 known_hosts 内的所有内容进行哈希。验证 ssh 仍能连接到你所有的常用主机。一旦你确信你的密钥缓存仍然可用，就删除未哈希的 known_hosts.old。

要在哈希的 known_hosts 文件中找到单个主机条目，请使用 ssh-keygen -F 和目标主机名。

```
$ ssh-keygen -F avarice.mwl.io
# Host avarice.mwl.io found: line 17
|1|5hcRwDHWwxwCWrFTngG4jT40hJ0=|TyJXB6z+oEJXSP5MzakulFWgPDI= ecdsa-sha2-nistp256...
```

你现在知道该条目在文件的第 17 行，可以轻松复制它。

要删除一个哈希的主机名，请使用 ssh-keygen -R。

```
$ ssh-keygen -R avarice.mwl.io
# Host avarice.mwl.io found: line 17
/home/mwlucas/.ssh/known_hosts updated.
Original contents retained as /home/mwlucas/.ssh/known_hosts.old
```

如果你还没有删除未哈希的 *known_hosts.old*，好吧，它现在没了。

当从中央系统（第 11 章）分发 *known_hosts* 时，没有理由不提供哈希版本。

## PuTTY 客户端

PuTTY 是一个 SSH、telnet 和串行客户端，也是 Windows 和类 Unix 系统的终端仿真器。它可在 https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html 获取，或通过网络搜索“putty SSH”即可找到。虽然它不是由 OpenBSD 团队中的专业偏执狂编写的，但 PuTTY 的自由可用源代码已被多次审计。PuTTY 可能是部署最广泛的 Windows SSH 软件。

PuTTY 下载页面提供几种选择。我推荐包含 PuTTY 及其所有相关程序的全功能安装程序。你不需要所有东西，但这样比单独下载各种实用程序更容易、更快。PuTTY 本身并不真正需要安装程序；如果你愿意，可以下载纯 PuTTY.exe。安装程序会在开始菜单中创建快捷方式，将程序注册到操作系统，并处理所有其他 Windows 琐事。

PuTTY 可以在命令行上运行。参数和命令行标志与 OpenSSH 非常相似。如果你正在运行 Windows，你可能对 PuTTY 作为图形程序感兴趣。我们将重点关注点选式界面，但你应该知道命令行也是一个选项，如果需要的话。

如果你感觉大胆，你也可以下载 PuTTY 开发快照。这包含了 PuTTY 的最新补丁和功能，但也可能包含全新的错误。

启动 PuTTY，你会得到类似图 5-1 的屏幕。

![](img/66dbcb7210a5fe0a8b3a1ecd91eb0e6d_47_0.png)

图 5-1：PuTTY 启动屏幕

在右侧，你将配置到不同服务器的连接。我们现在只有一个连接，Default Settings。它不会连接到任何东西，但你将用它来设置你的 PuTTY 默认值。你可以随时通过点击左侧的 Session 返回此屏幕。

在左侧，你配置 PuTTY 的呈现方式以及它如何处理支持的协议。PuTTY 支持多种协议。如果你需要一个灵活的通用终端仿真器，PuTTY 很可能能满足你的需求。我们只会涵盖 SSH。然而。注意倒数第二个的 SSH 选项。点击那里，或展开那个小“加号”，以查看和编辑 PuTTY 执行 SSH 的详细信息。

如果你在左侧选择某项，右侧会更改以显示所选选项的详细信息。选择 SSH，右侧会显示一些基本协议选项，例如协议版本和共享 SSH 连接（参见本章后面的“Connection Multiplexing”。）

我们将使用这些设置来建立我们的 PuTTY 默认值。

## 设置 PuTTY 默认值

你的全新 PuTTY 安装只列出一个连接，Default Settings。你创建的每个新连接都以复制 Default Settings 中的所有内容开始。点击 Default Settings 连接并点击 Load。你可以然后编辑并保存

