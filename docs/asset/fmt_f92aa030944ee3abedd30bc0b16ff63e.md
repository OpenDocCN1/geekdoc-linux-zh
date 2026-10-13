
在需要自动更新更新和安装安全补丁时，RHEL 9 提供了一个名为 DNF Automatic 的便捷工具。该工具的参数在配置文件中设置，命令将根据文件中设置的信息或数据执行。DNF Automatic 可以设置为执行以下结果：

- 通知并退出：在运行 DNF Automatic 工具检查更新后发送通知。
- 下载更新：仅下载更新的软件包。
- 下载并安装更新：下载包然后进行安装，类似于您按需运行 `dnf`。

# 配置软件存储库 RHEL 9 更新 95

要启用 DNF 自动更新（Automatic），请从控制台安装 `dnf-automatic` 软件包：

1. `[Jsg@rhel_9-bpb ~$]$ sudo rpm install dnf-automatic`
2. 名称：`dnf-automatic`
3. 版本：`4.12.0`
4. 发布版本：`4.el9`
5. 架构：`noarch`
6. 安装日期：`2023年1月14日 周六 12:58:22 PM PST`
7. 组：未指定
8. 大尺寸：`53144`
9. 许可证：`GPLv2`
10. 签名：`RSA/SHA256, 2022年9月15日 周四 10:39:24 PM PST, Key ID 199e2f91fd43d51`
11. 源 RPM：`dnf-4.12.0-4.el9.src.rpm`
12. 构建日期：`2022年9月15日 周四 08:05:47 PM PST`
13. 构建主机机：`x86-64-02.build..2.redhat.com`
14. 打包员：`Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla/>`
15. 供应商：`Red Hat, Inc.`
16. URL：`https://github.com/rpm-software-management/dnf`
17. 摘要：包管理器 - 自动升级
18. 描述：定期下载包更新并应用它们的系统单元。

接下来，在 `dnf-automatic` 已安装的情况下，使用 `rpm` 命令进行验证：

验证通过后，用文本编辑器打开 `/etc/dnf/automatic` 文件，并按照您希望 `dnf-automatic` 运行的方式设置工具的操作和行为。配置文件对您设置的参数有详细注释，并默认包含以下设置的四个关键部分：

### [commands_type]

`upgrade_type = default`（此默认设置执行所有可用的更新。此项也可以设置为 `security` 以仅执行安全更新）。

`network_online_timeout = 60`（定义工具连接到 Red Hat 存储库的最大秒数。默认设置为 `60 秒`）。

`download_updates = yes`（当更新可用时将下载更新。将其设置为 `no` 则仅检查更新而不会下载它们）。

`apply_updates = no`（默认不会应用更新。如果设置为 `yes`，则在下载后应用更新）。

`emit_via = stdio`（设置 `dnf-automatic` 发送消息的方式。默认设置为 `stdio`，这在设置发送消息的 `cron` 任务时非常有用。其他选项包括 `emit` 和 `motd`。如果留空，则不会发送任何消息）。

`email_from = root@example.com`（如果 `emit_via` 设置为 `email`，消息将从此处的电子邮件地址发送）。

`email_to = root`（您可以设置希望接收消息的地址）。

`email_host = localhost`（设置发送电子邮件消息的主机）。

`email_from = root@example.com`（这是从后台执行的 shell 命令，用于向来自 `[email]` 部分的接收者发送电子邮件）。

设置好 `automatic.conf` 文件的输入参数后，作为 `sudo` 用户启用 `systemctl` 以启用 DNF 自动更新：

1. `[js@relhel19-b~$] sudo systemctl enable --now dnf-automatic.timer`

启用后，检查计时器现在已设置：

1. `[js@relhel19-b~$] systemctl list-timers dnf-`
2. `NEXT LEFT LAST PASSED`
3. `2023-01-14 15:12:13 PST 15min left Sat 2023-01-14 13:41:51 PST 1h 14min ago`

![](img/d96b39fd89022f83082b77305c8fd6e9_123_0.png)

**图 7.2:** 在“运行命令”窗口中运行 `firefox` 浏览器

- 你也可以通过输入应用程序名称并按回车键从终端运行应用程序。请注意，在你运行应用程序时，终端将保持打开状态。如果你想将命令行用于其他用途，可以新的终端会话。

## 教程 #28：使用 GNOME Software 应用程序管理器管理和安装应用程序

你可以使用 GNOME Software 应用程序管理器（或 Software）安装新应用程序并管理现有的应用程序（前提是图形化应用程序）。可用应用程序按分类分组以便参考，你还可以使用关键词进行搜索，Software 将根据搜索结果提供建议。

现在让我们学习通过 GNOME Software 应用程序管理器安装新图形化应用程序的步骤：

- 1. **运行 GNOME Software 应用程序管理器工具：** 从 GNOME 桌面，点击桌面左角的“活动”（Activities）。从这里，你可以选择 3 种运行 Software 的方法：
    a. 从搜索栏中直接输入 `Software`，即可显示应用程序图标。
    b. 从 GNOME 桌面的底部面板，点击看起来像白色公包的图标。这将启动 GNOME Software 应用程序管理器。
    c. 从 GNOME，打开终端并使用 `gnome-software` 命令启动 Software。
- 2. **了解 GNOME Software 应用程序管理器工具：** 当 GNOME Software 应用程序管理器打开时，你将看到如下方**图 3.3** 所示的界面：

使用 GNOME 桌面管理 RHEL 9

![](img/d96b39fd89022f83082b77305c8fd6e9_124_0.png)

现在让我们查看应用程序界的一些细节：

- a. **搜索图标：** 要查找应用程序，可以点击界面左上角的放大镜图标。点击此图标将激活中间的搜索栏，你可以在其中搜索可以安装的新应用。
- b. **探索（Explore）：** 这是默认显示的内容，允许你浏览并列出分类分类的应用程序。
- c. **已安装（Installed）：** 此处将显示已安装应用程序的列表。你也可以点击“卸载”按钮来卸载不再使用的应用程序。
- d. **更新（Updates）：** 如果有系统和应用程序更新，你可以从此部分安装它们。
- e. **设置（Settings）：** 通过点击界面右上角的三条线图标，可以配置某些应用程序设置，例如激活额外的软件源或禁用当前的源、设置更新偏好（如自动更新和通知），以及在应用程序的“关于”部分阅读应用程序信息和致谢。
- 3. **安装应用程序：** 要安装应用程序，请通过 GNOME Software 应用程序中提供的选项进行选择。你可以使用上一节中提到的搜索或探索选项。在下方的示例*图 3.4* 中，正在安装 *GNU Emacs* 编辑器，并显示安装状态。安装 *GNU Emacs* 所需的所有依赖项也正在后台安装。

![](img/d96b39fd89022f83082b77305c8fd6e9_125_0.png)

**图 7.4:** 使用 GNOME Software 工具安装 GNU Emacs 编辑器

安装完成后，“取消”按钮将变为“打开”。当从 GNOME 桌面点击“显示应用程序”快捷方式时，也会出现 GNU Emacs 图标。

**管理已安装的应用程序：** 你可以通过在 GNOME Software 应用程序管理器中选择“已安装”来查看已安装应用程序列表并管理它们。将显示已安装的应用程序，你可以通过如图 3.5 所示的点击**卸载**按钮来移除应用程序。

使用 GNOME 桌面管理 RHEL 9

![](img/d96b39fd89022f83082b77305c8fd6e9_126_0.png)

图 7.5: 卸载 GNU Emacs 应用程序

- **更新应用程序：** 如果有应用程序或系统更新，你可以从此部分安装它们。你可以根据需要查看呈现的详细信息并应用更新。如果没有可用更新，“更新”将显示你的系统已是最新状态，如*图 3.6* 所示：

![](img/d96b39fd89022f83082b77305c8fd6e9_126_1.png)

图 7.6

## 教程 #29：在 GNOME 中管理存储
