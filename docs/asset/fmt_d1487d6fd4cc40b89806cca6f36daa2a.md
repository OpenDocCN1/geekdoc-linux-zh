
# 将聊天机器人嵌入网站

要将你的聊天机器人嵌入到基于 `HTML` 的简单网站，请进入“Room Settings（设置）”中的“Share & Embed（共享与嵌入）”选项卡。向下滚动到嵌入代码，复制并将其粘贴到 `HTML` 中 `<head>` 标签之前。只需如此；你的访问者现在就可以看到你聊天机器人的微型版本。你还可以限制聊天机器人可以嵌入的域名。如果你留空该字段，则确保它可以被嵌入到任何地方、任何地方。

有些人倾向于使用 `blogger.com` 而不是费力托管自己的 `WordPress` 或或其他 `CMS` 网站。让我们看看如何将 `Scrollback` 添加到你的 `blogger` 网站。你首先需要从 `Scrollback.com` 账户复制代码段，然后遵循 `Layout（布局）> Add Gadget（添加小组件）`。然后只需将代码粘贴到内容部分并点击 `Save（保存）`。你的 `blogger.com` 网站现在已与 `Scrollback` 集成。

![](img/6e6bbc2d7ddad215386a38abf7a3b0b7_35_2.png)

# WordPress 网站

# 将 IRC 链接到 Scrollback 房间

# 索引搜索

你可以选择哪些页面用于搜索索引。

要启动索引引擎，请进入 `Settings（设置）` 菜单 > `Search visibility（搜索可见性）` 并启用搜索引擎索引。

# Linux 技巧、妙招、进阶与应用

## 房间设置 (ROOM SETTINGS)

- 常用 (`General`)
- IRC 集成 (`Integration`)
- Twitter 集成 (`Integration`)
- 权限 (`Permissions`)
- 垃圾信息控制 (`Spam control`)
- 可见性 (`Visibility`)
- 讨论 (`Discussions`)
- 共享与嵌入 (`Share & Embed`)

![](img/6e6bbc2d7ddad215386a38abf7a3b0b7_36_0.png)

| 完成 (`DONE`) | 取消 (`CANCEL`) |
|---|---|
| 标签 (`Hashtags`) | `Scrollback` |
| 账户 (`ACCOUNT`) | |

# Twitter 集成

## 概述

`Scrollback` 提供了与 `Twitter` 的紧密集成，你可以通过它查看你的推文。只需在 `Twitter` 集成标签页下查看所有推文，就可以进入你的聊天机器人。

> “可能会出现人们在讨论不同的事情。如果你关注 `IRC` 频道，这很常见”

当你的聊天机器人中有你想查看的推文时，只需在页面右侧查看。然后刷新页面，你就可以点击“你的账户 (`Your account`)”。

## 审核功能 (Moderation features)

在 `General（常用）` 设置标签下。`Scrollback` 的设计非常有利于搜索。`Permissions（权限）` 允许你决定谁可以发布、编辑或封禁任何人，或者仅限登录用户。聊天室的一个功能允许你控制垃圾信息。只需在 `Settings（设置）` 标签下启用垃圾信息控制，`Scrollback` 就会阻止垃圾邮件发送者在你的房间发布。你现在还可以通过在自定义区域输入词汇来设置屏蔽列表。即使你把词汇放入聊天室，它们也不会可见。

## 讨论 (Discussions)

聊天室的一个主要问题是人们在讨论不同的事情。当一个聊天室有很多人在讨论时，获取有用信息变得困难。`Scrollback` 通过简单的滚动解决了这个问题。进入 `Discussions（讨论）` 标签页查看分组。`Scrollback` 根据聊天消息和用户输入的内容对讨论进行分组。任何时候都可以点击聊天窗口中的 `Discussions` 轻松创建讨论。在设置中添加 `Twitter` 标签即可查看聊天机器人中的相关推文，它们在 `Discussion` 标签页中存档。

![](img/6e6bbc2d7ddad215386a38abf7a3b0b7_37_0.png)

# 使用 BIND 创建查询请求 DNS 服务器

运行自己的 `DNS` 服务器以减少网络流量并节省 `DNS` 请求

## 资源 (Resources)

### `BIND` 首页

`https://www.isc.org/bind/`

### `RFC` 1034, 域名

### `RFC` 5936, `AXFR`

`tools.inet/html/rfc5936`

`DNS`（域名系统）是将人类可读的名称转换为 `IP` 地址（反之亦然）。如果它无法正常工作，你就无法浏览互联网或获取电子邮件。所谓的服务器或简单的名称服务器支持域名系统。网络设备必须至少配置一个 `DNS` 服务器才能正常运行，但为了冗余，你会使用多个名称服务器，以确保无论任何一个服务器失效，网络设备都能运行。它始终可以使用 `IP` 地址陈述。`DNS` 区域是域名的一个部分，其管理已被委派。例如，`.uk` 域名区域。`.uk` 域名管理委托所有子域名是非常合理的，否则它将管理所有的 `.uk` 域名，你可以想象，这些域名非常多。

38 Linux 技巧、妙招、应用与进阶

# 技巧 | 窍门 | 黑科技 | 应用

| `HOST(1)` | `BIND9` | `HOST(1)` |
| --- | --- | --- |
| 名称 | `host -dns lookup` | 03 `host` 实用工具 |
| 概览 | `host [-all] [-c] [-w] [-n] [-u] [-t] [-wait] [-f] [-g] [-name] [server]` | |

`host` 是一个用于执行 `DNS` 查询的简单实用工具。它通常用于检索 `DNS` 记录的信息。然而，它也可以用于显示其命令行参数和选项的简要摘要。

`name` 是要查询的域名。它可以是一个不带点的小进制名称，也可以是一个 `IP` 地址。如果提供了 `IP` 地址，`host` 将对该地址执行反向查询。回答查询的服务器名称即为服务器记录（`server record`）。

`-all` 选项等同于设置 `-a` 选项并要求 `host` 执行类型查询。

当使用 `-c` 选项时，`host` 将尝试显示该区域的 `SOA` 记录。它还会列出所有记录及其 `TTL`。名称服务器列表由找到的对应记录定义。

`-c` 选项会对类（`class`）进行 `DNS` 查询。这可以用于查找 `MX` 或 `Chaos` 类记录服务器。默认类为 `IN`。

# 01 BIND 服务器

`BIND` 代表 Berkeley Internet Name Domain（伯克利互联网域名），是 `DNS` 对象的实现。在 `Unix` 系统上，你可以使用以下命令安装最新版本的 `BIND`：

```bash
# apt-get install bind9
```

要查找 `BIND` 的版本，请执行以下命令：

```bash
# -version
BIND 9.8.16-1ubuntu4.4
```

![](img/6e6bbc2d7ddad215386a3b0b7_38_0.png)

# 03 host 实用工具

`host` 输出非常干净，这是它被广泛使用的原因——它可以方便地在 `shell` 脚本中使用。最后一个参数是服务器名称。如果没有给出，`host` 将查看 `/etc/resolv.conf` 来寻找 `DNS` 服务器。

与 `-mx` 参数配合使用时，`host` 显示域名或子域的邮件服务器

```bash
# host -mx linuxux.com
linuxux.com is handled by 10 mail1-linux-publishing.com.
linuxux.com is handled by 20 mail2-linux-publishing.com.
```

“handled”后面的数字是用于邮件交换器（`mail exchanger`）优先级的偏好值。偏好值并不重要，重要的是交付的可靠性。

邮件服务器应该首先投递到值最低邮件交换器。如果两个或多个邮件交换器具有相同的偏好值，则由主邮件服务器负责投递。主邮件服务器负责域名或子域的邮件。

与 `-t` 参数配合使用时，`host` 显示域名的 `DNS` 服务器。

# 02 什么是 DNS 服务器？

缓存 `DNS` 服务器不包含域名信息；它只包含基于其已执行的 `DNS` 查询结果的信息。缓存之所以有效，是因为 `DNS` 数据不会频繁变化。

# 04 dig 实用工具

`dig` 允许你查看与主机相关的 `DNS` 信息。它的输出比 `host` 更详细。它显示了你所执行的查询的 `DNS` 服务器，并可以通过执行以下命令帮助你调试问题：
