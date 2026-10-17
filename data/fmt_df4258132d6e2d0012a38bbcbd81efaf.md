
| `quest` | 4,996 | 2002-04-23 | `driver/x/` |
| `kermac` | 4,996 | 2002-03-05 | `driver/x/` |
| `Desktop` | 4,996 | 2002-03-25 | `driver/x/` |
| `Documents` | 4,996 | 2002-03-25 | `driver/x/` |
| `CC_server_mouse` | 595 | 2002-04-25 | `driver/x/` |
| `CAuthority` | 209 | 2002-04-27 | `driver/x/` |
| `Xauthority` | 5,742 | 2002-03-25 | `driver/x/` |
| `Xmodmap` | 1,305 | 2002-03-05 | `driver/x/` |
| `history` | 744 | 2002-04-20 | `driver/x/` |
| `Temporary Files` | 1,802 | 2002-04-25 | `driver/x/` |
| `bash_profile` | 204 | 2002-04-23 | `driver/x/` |

1. 点击主目录。
2. 输入新文件名：`.bash_profile`。在文件名名前加点号会使其成为隐藏文件；当启动新的 BASH 壳时，`.bash_profile` 将处于隐藏读取状态。
3. 点击“保存”将文件写入磁盘。

图 2-27 KWrite 的保存对话框

注销并重新登录以使更改生效。

> **注意：** 如果你启动了 X-Windows，请确保你是注销而不是重启 X-Windows。要注销，请使用 `exit` 命令或 `ctrl-d`。

你可以通过启动壳并在提示符输入 `echo $SPATH` 来检查 `PATH` 变量是否设置正确。要验证你正在使用 Domino 服务器可执行文件，输入 `which server` 并检查路径。

```
$Shell - Console
Session Edit View Settings Help
itdom6@itsorted:> echo $SPATH
/usr/local/bin:/usr/bin:/usr/X11R/bin:/usr/games:/opt/kd\e3:/bin:/usr/lib/java:/bin:/opt/lotus/bin::/
itdom6@itsorted:> which server
/opt/lotus/bin
itdom6@itsorted:>
```

图 2-28 `echo` 和 `which` 命令

在启动 Domino 安装程序之前，请切换到你的 Domino 数据目录（在本例中，它是 `/local/notesdata` 目录）。启动服务器时你必须位于 Domino 数据目录中。

106 Linux 版 Lotus Domino 6

**注意：** 在设置 `notes` 用户账户时，主目录应该设置为 Lotus Domino 数据路径：`/local/notesdata`。

## 2.2.5 远程设置

**注意：** 我们建议使用远程设置，因为它让你能够将服务器文件和认证器 ID 文件下载到你的本地工作站。

新的 Java 安装程序也支持远程配置。安装过程与本地安装几乎相同。

1. 要运行远程设置，你必须在你的工作站上安装了带有远程服务器设置选项的 Lotus Administrator（见图 2-29）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_120_0.png)

图 2-29 Lotus Administrator 远程服务器设置选项

第 2 章 安装 Linux 版 Domino 6 107 页

2. 使用 Domino 用户账户 (`itsdom6`) 登录服务器，切换到 Domino 数据目录 (`/local/notesdata`) 并使用 `listen` 选项启动 Domino 服务器（见图 2-30）。

**重要：** 确保系统 `LANG` 变量已根据你的语言正确设置，例如 `LANG=en_US`、`LANG=de_DE@euro`。要设置系统变量 `LANG`==

```
[NOTESWHOM: notesdata$ /opt/lotus/bin/server -listen
./java -ss512k -cp cfgdomserver.jar:Notes.jar lotus.domino.setup.ManagerDomino -data /local/notesdata -listen
远程服务器设置现在已在端口 8085 启用。
```

Domino 安装服务器现在处于监听模式。

远程客户端现在可以连接到此服务器并配置 Domino。

要连接到此服务器，请通过以下命令启动远程 Domino 设置程序：

从 Domino 管理员客户端：`serverset -remote`

从 Domino 服务器：`server -remote`

要结束此服务器，请从命令提示符通过以下命令启动远程 Domino 设置程序：

从 Domino 管理员客户端：`serverset -q`

从 Domino 服务器：`server -q`

有关更多信息，请参阅打印指南《Setting Up Domino Networks and Services rs》。

图 2-30 带有 `listen` 选项的 Domino 服务器

3. 进入命令提示符，切换到 Domino 目录，并如第 9 页的图 31 所示启动 Java 配置器 (`serverset.exe`)。

```
C:\WINDOWS\System32\cmd.exe
e:\lotus>serverset.exe
e:\lotus>
```

图 2-31 `serverset.exe`

4. 在 Host 字段输入服务器名称或 IP 地址并点击“Ping”。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_122_0.png)

图 2-32 连接远程

5. 如果远程设置正确，你应该看到类似第 10 页图 33 所示的消息。

如果通用名称与主机名，即使服务器位于不同的域，客户端也能找到它。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_123_0.png)

图 2-33 Ping 成功

6. 现在点击“确定”。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_124_0.png)

图 2-34 开始配置

7. 你正在设置你的新域。你必须为服务器提供一个唯一的名称；之后无法轻易更改。记住，你需要认证器 ID 来创建后续的组织单元 (OU)。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_125_0.png)

图 2-35 服务器名称

8. 我们将服务器名称设置为与主机名相同。这样做有很多理由，其中当 Lotus Client 尝试查找服务器时，它将使用服务器的通用名称查询 DNS。标题让你有机会对服务器或所属组织进行简洁描述。

9. 设置有意义的组织名称，并确保为认证器 ID 输入安全的密码，点击“下一步”继续。

如果你正在重建 Domino 域，可以勾选“我想使用现有的认证器 ID 文件”来执行。

### 选择你的组织名称

组织名称通常是你的公司名称。它将成为每个服务器和用户名的一部分。不要选择过长的组织名称。例如，与其使用 Acme Corporation，不如使用 Acme。

| 组织名称 | ITSO |
| --- | --- |
| 服务器的最终名称将是... | `itsored/ITSO` |
| 典型的用户名将是 | `notes/ITSO` |
| 组织认证器密码 | `**********` |
| 确认密码 | `**********` |

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_127_0.png)

图 2-38 Domino 域名

10. 为了便于管理和使用，我们将 Domino 域名设置为与组织（Organization）名称相同。

**提示：** 如果您打算拥有多个域名，现在就应该决定命名方案，并确保第一个域名符合您之后所有域名都将使用的方案。

输入您想要使用的名称并点击 `Next`（下一步）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_128_0.png)

11. 输入管理员名称和密码，然后点击 `Next`（下一步）。

我们选择创建一个通用的管理员 ID 并通过 Web 浏览器将其下载到客户端。如果您打算在本地使用该 ID，请勾选“同时保存 ID 文件的本地副本”选项，这样就可以方便地访问 ID。由于管理员 ID 拥有 Domino 目录的完全权限，我们在下载之后已从人员（Person）文档中删除了该 ID。

> **重要：** 如果您正在运行远程安装，请勿勾选“同时保存 ID 文件的本地副本”，因为它会尝试访问您无权限的服务器本地文件系统。在远程设置的后续，有一个选项可以将 ID 文件复制到您的本地工作站。
