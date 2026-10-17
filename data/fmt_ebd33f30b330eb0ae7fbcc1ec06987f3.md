
这允许 `inetd` 在端口 98 上运行 `Linuxconf`。如果你想通过局域网（LAN）远程管理此系统，可以使用网络地址。例如，我使用了网络地址 `206.171.50.48`。为了启用网络中的所有机器，我在可选掩码框中指定了掩码 `255.255.255.240`。掩码是可选的，因为 `Linuxconf` 可以根据网络地址计算掩码。如果你计划添加多个主机而不是整个网络，可以添加你的 IP 地址。默认情况下，屏幕允许输入两个 IP 地址和两个可选掩码。如果你需要更多空间，点击 `Add`（添加）按钮添加更多主机。

如前所述，默认情况下 `Linuxconf` 仅允许从 `localhost` 访问。为了启用 `Linuxconf` 的远程访问，需要遵循以下步骤：

- 从控制台或 X Windows 运行 `linuxconf`。
- 选择 `Config` 菜单，通过按 Enter（文本模式）或双击（GUI 模式）展开分支。
- 选择 `Misc.`（杂项）选项并展开。现在选择 `Linuxconf network access`；你会看到一个类似于图 6-8 的标签窗口。

![](img/cbfef09f620ba4100baa62876f6f02b1_195_0.png)

图 6-8：配置 `Linuxconf` 的网络访问

- 勾选 `Enable network access` 框。
- 勾选“Log access in `/var/log/htmlaccess.log`”框，允许记录通过网络对 `Linuxconf` 的访问请求。
- 在网络或主机输入框中，输入你允许通过 Web 访问 `Linuxconf` 的主机名称。你也可以在这里输入 IP 或网络地址。
- 输入完主机名、IP 地址或网络/掩码对后，点击 `Activate`（激活）按钮。
- 点击 `Quit`（退出）按钮退出 `Linuxconf`，并在提示时激活当前配置。

# 第三部分：管理用户、进程和网络

## 第 6 章：使用 Linuxconf

这将允许命名主机（或 IP 地址）通过 Web 访问 `Linuxconf`。

如前所述，`Linuxconf` 同时使用内部代码函数和外部模块来执行实际配置。目前，`Linuxconf` RPM 软件包包含了几乎所有可用的模块。这可能会发生变化，因为理想情况下，`Linuxconf` 模块确实应该随各个软件包一起分发。例如，Red Hat 的 Apache 软件包应该包含一个 `Linuxconf` 模块。如果您不使用 Apache Web 服务器，则在您的 `Linuxconf` 配置中不需要 Apache 模块。模块越多，`Linuxconf` 界面看起来就越杂乱。如果应用程序开发者能够自行分发，那么您将只拥有所需的内容。希望 `Linuxconf` 很快就能向这种方式转变。在此之前，您可以手动配置需要哪些模块。

### 配置 Linuxconf 模块

你可以添加新模块或停用现有模块。模块存储在 `/usr/lib/linuxconf/modules` 目录下。要添加新模块，请从 `Linuxconf` FTP 站点下载相应的 RPM 软件包。载有 `Linuxconf` 文件的 FTP 站点列表可以在 `http://dns.solucorp.qc.ca/linuxconf/available.html` 找到。

一旦下载了 `linuxconf` 模块，使用 `rpm -ivh module_package` 命令进行安装。安装完成后，该模块将自动出现在 `Linuxconf` 的模块列表中。它也会被自动激活。要停用一个模块，请执行以下操作：

1. 运行 `linuxconf`。
2. 从 `Control`（控制）菜单中选择 `Configure Linuxconf modules`（配置 `Linuxconf` 模块）选项。你将看到一个与图 6-9 类似的屏幕。
3. 滚动模块列表找到想要停用的模块。切换“module is active”（模块已激活）复选框使模块变为非激活状态。
4. 点击 `Accept`（接受）按钮。
5. 如果在 `Linuxconf` 中没有其他操作，点击 `Quit`（退出）按钮。系统将询问是否激活更改。点击 `Activate the changes`（激活更改）完成过程。

![](img/cbfef09f620ba4100baa62876f6f02b1_197_0.png)

图 6-9：配置 `Linuxconf` 模块

下次运行 `Linuxconf` 时，它将显示一个类似于图 6-10 所示对话框。

![](img/cbfef09f620ba4100baa62876f6f02b1_197_1.png)

图 6-10：重新配置 `Linuxconf` 对话框

这意味着 `Linuxconf` 正在移除与非激活模块相关的菜单项。`Linuxconf` 还允许你创建特权用户账户，这些账户可用于管理 Linux 系统的某些方面。当你的组织中有许多管理员时，此功能将非常有帮助。也许你可能想将一些简单的管理任务分配给初级管理员。在这种情况下，你可以创建具有受限权限集的普通用户账户。将在下一节中讨论这一点。

### 定义用户权限

`Linuxconf` 允许你将某些管理权限与普通用户关联。考虑这个示例：假设你有一个名为 `pibek` 的普通用户账户，并想给该账户分配一些管理权限。执行以下操作：

1. 从 `root` 账户运行 `linuxconf`。
2. 从 `Config`（配置）菜单中选择 `User accounts`（用户账户）选项。
3. 从 `Normal (users)`（普通（用户））选项中选择 `User accounts`。你将看到系统上所有普通用户的列表。找到目标用户（在此例中为 `pibek`）并双击用户记录行。你将看到一个与图 6-11 类似的屏幕。

![](img/cbfef09f620ba4100baa62876f6f02b1_198_0.png)

4. 正如图 6-11 所示，你可以看到 `Base Info`（基础信息）窗口。其子系统。点击 `Privileges`（权限）选项卡以配置可用权限。

![](img/cbfef09f620ba4100baa62876f6f02b1_198_0.png)

5. 正如图 6-11 所示，你可以看到 `Base Info`（基础信息）窗口。点击 `Privileges`（权限）选项卡以配置可用权限。

表 6-2

| 功能 | 解释 |
| :--- | :--- |
| May use | 如果你希望用户运行 `Linuxconf` |
| May activate | 如果你希望用户激活更改 |
| May shutdown | 如果你希望用户关机 |
| May switch | 如果你希望用户启用/禁用网络 |
| May view | 如果你希望用户查看日志 |
| SuperUser | 如果你希望用户拥有特权访问 |

正如表 6-2 所示，“Granted”（已授予）和“silent”（静默）的区别在于后者不需要密码。

如果你希望用户管理服务，点击 `Services` 选项卡。你系统上的可用服务取决于你安装的内容。图 6-13 显示了可用服务。

![](img/cbfef09f620ba4100baa62876f6f02b1_200_0.png)

1. 如果你希望用户成为 POP 的账户管理员，点击 `User accounts` 选项卡授予权限。
2. 点击 `Accept`（接受）按钮并点击按钮退出 `Linuxconf`。

退出 `Linuxconf` 后，以用户身份登录系统并运行 `linuxconf`。测试你的新权限。确保它们是你想要的。

现在来看看 `Linuxconf` 的一个非常酷的功能，它允许为你的 Red Hat Linux 系统创建多个系统配置。

### 使用多系统配置

很久以前，微软发布了 MS-DOS 6.2，带有 `AUTOEXEC.BAT` 和 `CONFIG.SYS` 语法，用户可以创建配置。为单个系统创建多个配置允许 DOS 用户更好地利用资源。`Linuxconf` 的多系统配置功能与微软提供的非常相似。唯一的区别是 `Linuxconf` 提供了更高级的系统配置功能。

`Linuxconf` 将系统配置定义为子系统的集合。子系统是一组配置文件。例如，`mail` 是一个子系统，在 `/etc/aliases`、`/etc/mail/verifytable` 和 `/var/lib/mailterd` 等处具有文件。`Linuxconf/archive` 将每个定义的子系统存储在子目录下。如果定义了子系统，也就是说，它被赋予了作为子目录名。例如，如果 `mail` 是配置中子系统的族名，`/etc/linuxconf/mail` 将包含邮件相关的配置文件。这种技术当你要在两个或多个系统配置之间共享配置文件时非常有用。

默认情况下，`Linuxconf` 提供两个系统配置：`Office` 和 `Home`。你可以在 `Linuxconf` 中找到可用的系统配置。点击 `Control` 菜单，选择 `Control files and systems`（控制文件和系统）选项，然后选择 `Configure system profiles`（配置系统配置）选项。你将看到图 6-14 所示的可用配置列表。

![](img/cbfef09f620ba4100baa62876f6f02b1_201_0.png)

图 6-14：可用的（默认）系统配置

要确定 `Linuxconf` 当前正在使用哪个系统配置，点击控制（`Control`）菜单，选择控制面板（`Control panel`）选项，然后选择切换系统配置（`Switch system profile`）选项。你将看到如图 6-15 所示的可用配置列表。

![](img/cbfef09f620ba4100baa62876f6f02b1_202_0.png)

图 6-15：确定当前系统配置

你创建自己的系统配置。方法如下：

- 1. 点击控制（`Control`）菜单，选择控制文件和系统（`Control files and systems`），并选择配置系统配置（`Configure system profiles`）。你会看到一个与图 6-14 所示的窗口。
- 2. 点击添加（`Add`）按钮添加新的系统配置。系统将要求为新系统配置输入名称，如图 6-16 所示。名称必须单个单词，不能包含任何空格字符。输入你选择的名称并点击接受（`Accept`）。
- 3. 系统将要求为你的新配置输入标题。可以是任何你想要的内容；它仅用于帮助你将该配置与其他区分。根据你的需求输入有意义的内容。
- 4. 现在你需要为各种子系统提供存档族名称（即 `/etc/linuxconf/archive/subsystem-family-name`），例如 `cron`、`PPP/SLIP/PLIP`、`DNS` 服务器、防火墙规则、`wu-ftpd` 服务器、`gated`、`inet`、`httpd`、`lpd` 等。你也可以提供一个默认存档族，以便在未为特定子系统显式定义存档族时使用。如果你不设置默认族或提供显式族，子系统数据将存储在 `/etc/conf.linuxconf` 文件。如果你想使用另一个配置中的现有子系统，只需输入该配置的现有族即可。请注意，如果子系统在多个存档之间共享，则对子系统配置文件的任何更改将对所有使用该子系统的系统进程生效。

![](img/cbfef09f620ba4100baa62876f6f02b1_203_0.png)

- 5. 一旦指定了存档族，点击接受（`Accept`）按钮。你的新配置将被添加到可用配置列表中。再次点击接受（`Accept`）按钮。
- 6. 要使用新创建的配置，点击控制（`Control`）菜单，选择控制面板（`Control panel`）选项，然后选择切换配置（`Switch profile`）选项。现在点击你的配置进行切换。一旦切换到新配置，当你切换回另一个配置时，它将自动存档。如果你想手动存档，点击控制（`Control`）菜单，选择控制面板（`Control panel`）选项，然后选择存档配置（`Archive configurations`）。

如你所示，`Linuxconf` 提供了一种非常强大的手段，让你实验各种配置而不必担心丢失现有配置。如果你感兴趣以不同的配置启动系统，`Linuxconf` 可以提供帮助。这将在下一节中讨论。

### 在系统启动时使用 Linuxconf

当你安装 `Linuxconf` 时，它会通过插入如下行来修改 `/etc/rc.d/rc.sysinit` 文件：
```
