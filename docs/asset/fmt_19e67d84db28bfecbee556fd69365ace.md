
- 2. 以 `majordomo` 用户身份运行 `make install`，将 Majordomo 脚本和可执行文件安装到 `majordomo` 家目录中。
- 3. 以 `root` 用户身份运行 `make install-wrapper`，安装设置 `setuid root` 的 `wrapper` 程序。

![](img/4af9afea53463095bafc6057b1f7b908_481_0.png)

## 高级主题 第三部分

此时，你可以运行 `wrapper` 程序并测试 Majordomo 安装。以没有特殊权限的用户身份登录，并切换到 Majordomo 程序的家目录（在本例中为 `/usr/local/majordomo`）。从那里输入

```
./wrapper config-test
```

这将运行 `wrapper` 程序并测试配置。列表 18.4 显示了 `wrapper` 的部分输出。

### 列表 18.4 wrapper 配置测试输出

测试结束

1

2

3

4 没发现任何问题！Majordomo _应该_ 正常工作。

5 如果没有工作，请仔细检查你的配置文件 (`/usr/local/majordomo/majordomo.cf`)，如果看起来仍然没问题，考虑向邮件列表 "`majordomo-users@examplecircle`" 寻求帮助。务必详细说明你的问题，以及你使用的什么类型的机器（和操作系统）。

11

12

13 享受！

## 为 Majordomo 创建 sendmail 别名

成功安装 Majordomo 软件后，你必须配置 `sendmail` 以识别邮件列表。Majordomo 使用 `sendmail` 别文件处理列表（参见第 17 章“邮件别名与伪装”）。

### 列表 18.5 Majordomo 别名行

```
1 # Majordomo 别名
2 majordomo: "/usr/local/majordomo/wrapper majordomo"
```

# 邮件列表

## 第 18 章

在封装程序（`wrapper program`）之外使用邮件别名有一个技巧。有些安装建议使用 `smrsh` 功能，如第 11 章所示。这种受限的 `shell` 除非程序出现在 `root` 用户拥有的特殊目录，否则拒绝执行程序。如果你的 `sendmail` 配置使用了 `smrsh` 功能，它将引用你放置 `sendmail` 允许运行的可执行文件所在的目录。在 Mandrake Linux 6.0 上，该目录是 `/etc/smrsh`。通过将封装程序从普通位置 `/usr/local/majordomo/wrapper` 复制到（在本例中）`/etc/smrsh` 目录，`sendmail` 将能够运行该封装程序。

第 3 行和第 4 行支持别名。如果列表成员在使用邮件列表时遇到困难，他可以向列表所有者发送邮件寻求帮助、建议等。这些地址指向邮件列表所有者的真实邮箱地址。

# 测试 Majordomo 安装

你可以创建一个测试列表来查看安装是否正确。首先，你必须根据 `majordomo.cf` 文件的指定，在 Majordomo 目录中创建一个虚拟列表文件。在本例中，位置是 `/usr/local/majordomo/lists`。你可以使用以下命令创建测试文件：

```
touch /usr/local/majordomo/lists/test
```

创建文件后，你可以向 `majordomo` 别名发送 `majordomo 'lists'` 命令，以接收可用邮件列表列表。列表 18.6 显示了此的示例。

# 列表 18.6 Majordomo 安装测试

```
1 [richadrich$] echo | mail -v majordomo
2 majordomo... aliased to "/usr/local/majordomo/wrapper majordomo"
3 "/usr/local/majordomo/wrapper majordomo" Connecting to prog.
4 "/usr/local/majordomo/wrapper majordomo" Sent
5 [richadrich$] mail
6 Mail version 8.1/6/93. Type ? for help.
7 /var/spool/mail/rich: 1 message new
8 >N1 Majordomo@smallorg.org Thu Nov 18 18:51 23/736 "Majordomo results"
9 &\n10 Message 1:
11 From Majordomo-Owner@smallorg.org Thu Nov 18 18:51:35 1999
12 Date: Thu, 18 Nov 1999 18:51:34 -0500
13 Authentication-Warning: majordomo.smallorg.org: majordomo set sender to
14 Majordomo-Owner@smallorg.org using -f
15 To: rich@smallorg.org
16 From: Majordomo@smallorg.org
17 Subject: Majordomo results
18 Reply-To: Majordomo@smallorg.org
19
```

![](img/4af9afea53463095bafc6057b1f7b908_483_0.png)

# 高级主题

第三部分

# 列表 18.6 续

```
20 --
21
22 >>>> Majordomo@smallorg.org serves the following lists:
24
25 test
26
27 Use the 'info <list>' command to get more information
28 about a specific list.
29
30 &
```

在列表 18.6 中，第 1 行显示了向 Majordomo 发送 '`lists`' 命令的示例。`-v` 选项让 Linux 邮件程序进入详细模式，你可以看到正在发生什么。第 2 到 4 行显示了邮件的结果。第 2 行表示 `sendmail` 识别了别名。第 3 行显示 `sendmail` 联系封装程序。第 4 行显示 `sendmail` 成功将消息传递给封装程序。消息发送后，你检查发送邮件的用户的邮箱，以获取 Majordomo 的回复。第 5 到 30 行显示了从 Majordomo 返回的邮件邮件，表明 Majordomo 服务器上有一个可用邮件列表。当然，这并不完全真实，因为你还没有正确配置邮件列表。

作为对 Majordomo 系统的最后检查，你发送给 Majordomo 的命令将记录在 Majordomo 日志文件中。检查日志以查看它是否成功。以下内容出现在服务器的 `/usr/local/majordomo/log` 文件中：

```
Nov 18 18:51:34 smallorg.org majordomo[28128] { Rich
-<rich@shachack.smallorg.org> lists
```

日志文件指示了时间、邮箱地址和输入的命令。频繁检查 Majordomo 日志文件有助于发现邮件列表的任何授权活动。

# 配置 Majordomo 邮件列表

安装 Majordomo 程序后，接下来你将配置实际的邮件列表。首先，你必须创建一个文件，用于存储列表中的邮箱地址。文件名必须与邮件列表名称匹配。此示例将使用邮件列表名称 `office-news`。创建文件后，你必须确保设置了正确的访问模式。如果 `sendmail` 尝试使用一个组可写的别名，它会报错。

```bash
touch /usr/local/majordomo/lists/office-news
chmod 755 /usr/local/majordomo/lists/office-news
chmod 644 /usr/local/majordomo/lists/office-news
```

接下来，为邮件列表创建一个信息文件。当有人请求列表信息时，Majordomo 将使用该信息文件。信息文件位于 `/usr/local/majordomo/lists/office-news.info`，包含列表的简单描述。

# 表 18.1 别名

| 别名 | 描述 |
| :--- | :--- |
| `list` | 邮件列表 |
| `owner` | 列表所有者 |
| `request` | 请求地址 |
| `approval` | 审核列表的发布审批人 |
| `digest` | 摘要地址 |
| `digest-request` | 摘要请求地址 |

# 列表 18.7 列表条示例

```
officenames: "/usr/local/majordomo/wrapper majordomo"
owner: rich
request: rich
approval: rich
digest: rich
digest-request: rich /usr/local/majordomo/lists
```
