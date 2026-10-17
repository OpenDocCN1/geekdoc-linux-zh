
要配置默认网关，请从 `linuxconf` 菜单树选择 `Config`（配置） > `Networking`（网络） > `Client Tasks`（客户端任务） > `Routing`（路由） > `Set Defaults`（设置默认）。将出现 `Defaults`（默认）界面；图 9.16 显示该界面的图形化版本。

图 9.16 默认界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_242_0.png)

指定默认网关的 IP 地址。如果你让此系统充路由器，请开启 `Routing`。有关配置路由的更多信息，请参阅第 29 章，“配置路由器”。

### 激活更改

如前所述，当使用 `linuxconf` 更改选项时，该更改可能会立即发生，也可能保持挂起状态直到更改被激活。虽然配置文件会立即更新，但大多数服务在重启之前不会检测到更改。当你指示 `linuxconf` 激活挂起的更改时，会重启已更改配置的服务。

如果你想知道有哪些挂起的更改，点击“Preview What Has Done”（预览已完成）。`linuxconf` 将显示挂起的更改。要激活更改，点击“Activate”。要在不激活任何挂起的更改的情况下退出状态界面，点击“Quit”。

你应该在退出 `linuxconf` 之前激活挂起的更改。如果你忽略了这一点，`linuxconf` 将提示你确认要在不激活更改的情况下退出。

### 总结

在本章中，你学习了如何配置安装时的选项。涵盖了最重要的主题：

- `键盘`：安装完成后，你可以使用 `kbdconfig` 程序配置键盘。
- `鼠标`：安装完成后，你可以使用 `mouseconf` 程序配置鼠标。
- `时区`：安装完成后，你可以使用 `timeconf` 程序配置时区。
- `音频`：安装完成后，你可以使用 `sndconfig` 程序配置音频。
- `默认运行级别`：安装完成后，你可以使用 `linuxconf` 程序配置默认运行级别。
- `身份验证`：安装完成后，你可以使用 `pwconv` 或 `punconv` 程序配置影子密码，或使用 `linuxconf` 程序更改 `root` 密码。
- `LILO 选项`：安装完成后，你可以使用 `linuxconf` 程序配置 LILO 选项。
- `网络`：安装完成后，你可以使用 `linuxconf` 程序配置网络。

### 关键术语

在进入下一章之前，请确保熟悉以下术语：

`Runlevel`（运行级别）

### 更多信息来源

如果你想进一步了解本章介绍的主题，你应该查阅以下资源：

字体 官方 Red Hat Linux 参考指南

- 本章描述的程序和工具的手页 (`man pages`)

### 复习题

请注意，你可能会发现其中几个问题其实非常简单，因为它们纯粹是记忆性问题。但这类问题有时会出现在笔试中。虽然在键盘上回答这些问题很容易，但在闭卷考试中可能会很麻烦。我为了考试突击了这些题目，现在我发现自己正在回过检查答案！即使在键盘前，你也可能花费几分钟来检查一个重要工具的名称，因此最好记住你在性能考试中可能用的所有程序名称。这样，你就可以将精力集中在更重要的问题上。

- 1. 下面哪个程序用于配置键盘？

   A. `kbconfig`

   B. `kbdconfig`

   C. `keyconfig`

   D. `keyboardconfig`

- 2. 下面哪个程序用于配置鼠标？

   A. `mousecfg`

   B. `mouseconfig`

   C. `msectcfg`

   D. `mousetest`

- 3. 下面哪个程序用于配置声音？

   A. `soundcfg`

   B. `sndconfig`

   C. `soundcfg`

   D. `soundconfig`

- 4. 哪个运行级别会导致系统启动时出现基于 X 的登录界面？

   A. 2

   B. 3

   C. 4

   D. 5

- 5. 关于 `linuxconf`，以下哪项是正确的？

   A. 可以通过执行 `linuxconf` 命令启动。

   B. 它在图形模式下运行。

   C. 它在文本模式下运行。

   D. 你必须使用鼠标才能操作它。

- 6. 使用 `linuxconf` 时，必须显式激活等待更改何时？

   A. 如果另一个用户正在运行 `linuxconf`

   B. 如果必须重启一个或多个系统服务使更改生效

   C. 如果更改影响用户账户

   D. 如果更改很复杂

### 复习题答案

- 1. B. `kbdconfig` 程序配置键盘。
- 2. B. `mouseconfig` 程序配置鼠标。
- 3. B. `sndconfig` 程序配置声音系统。
- 4. D. 运行级别 2 是无网络的多用户模式。运行级别 4 基本上与运行级别 3 相同。
- 5. A、B 和 C。`linuxconf` 程序既可以在文本模式图形图形模式运行；它不需要鼠标。
- 6. B. 在你指示执行之前，`linuxconf` 程序不会自动重启你已更改了配置的服务。

## 第 10 章

## 管理用户账户和组

本章涵盖的 RHCE 备考主题：

- 理解并了解如何创建不同类型的用户账户。
- 理解并了解如何配置用户环境。
- 熟悉系统和用户的 bash 配置文件。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_248_0.png)

Linux 系统管理员的主要任务之一是用户账户的创建和配置。红帽 Linux 提供了多种用户账户，因此红帽 Linux 系统管理员必须知道如何为特定用户选择合适的账户类型，并知道如何创建和配置账户。与用户账户相关的是组，组定义了可以向其扩展权限和许可的用户集。本章将解释红帽 Linux 提供的用户账户类型，以及创建和配置用户账户和组的。

## 用户账户

`/etc/passwd` 文件定义了 Linux 用户账户。文件中的每一行描述一个用户。以下是一个典型的 `/etc/passwd` 文件：

```
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:
demon:x:2:2:daemon:/sbin:
mad:x:3:4:adm:/var/adm/
lpd:x:4:7:1:/var/spool/lpd
sync:x:5:0:sync:/bin/sync
shutdown:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool/mail
news:x:9:13:news:/var/spool/news
uucp:x:10:14:uucp:/var/spool/uucp:
```

```
operator:x:11:0:operator:/root/
games:x:12:100:games:/usr/games/
gopher:x:13:30:gopher:/usr/lib/gopher-data/
ftp:x:14:50:FTP User:/home/ftp/
nbody:x:99999:Nobody:/
xfs:x:100:233:X Font Server:/etc/X11/fs:/bin/false
bill:x:500:500:Bill McCarthy/home/bill:/bin/bash
```

每行包含多个字段，并用冒号分隔。以下是这些字段的列表以及每个字段的解释。

**用户名 (User name)**：与用户账户关联的登录名。

**密码 (Password)**：与用户账户关联的登录密码。

**用户 ID (User ID)**：与用户账户关联的唯一 ID。

**组 ID (Group ID)**：与用户相关的数字 ID。

**全名 (Full name)**：用户的全名。

**主目录 (Home directory)**：为用户设置的目录。

**Shell**：用户使用的命令解释器。

### 通过工具管理用户账户

账户最账户的方法是通过 `linuxconf` 工具。然而，如果你使用的是 X 环境，菜单看起来会有所不同。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_250_0.png)

`linuxconf` 程序提供了另一种访问 `userconf` 方法。通过 `linuxconf` 访问 `userconf`，执行命令：

```
linuxconf
```

然后，通过选择 `Config` ➤ `Users Accounts` 导航到用户账户菜单。图 10.2 显示了 `linuxconf`。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_251_0.png)

### 创建用户账户

普通用户账户（通常称为 shell 账户允许用户登录并使用系统。按照以下步骤创建普通用户账户：

- 1. 启动 `linuxconf`。
- 2. 选择 `Users Accounts` 并按回车。如果你使用的是 X，点击 `Users Accounts`。图 10.3 显示的 `Users Accounts` 屏幕将出现。
