

# 480 第四部分 ♦ 在 SUSE Linux 中实现网络服务

sendmail 免费提供。其开发在开源社区（www.sendmail.org）和一家名为 Sendmail 的公司（www.sendmail.com）持续进行，Eric Allman 是该公司的首席技术官，下一代版本的 sendmail 正在积极开发中。

本节将解释如何在 SUSE 系统上安装、配置和启动 sendmail。

## 安装 sendmail

如前所述，SUSE 系统默认不会安装 sendmail。要安装 sendmail，您需要移除 Postfix（SUSE Linux 系统上的默认 MTA，即邮件传输代理）或您之前可能安装的任何其他 MTA。SUSE 使用 RPM 作为跟踪已安装软件包及其关联文件的核心数据库，简化了添加和删除整个软件包的操作，而 YaST 使这一过程变得更加简单。

要在您的 SUSE 系统上安装 sendmail：

- 1. 安装 YaST，选择“软件”（Software），最后选择“安装和删除软件”（Install and Remove Software）。点击“管理员模式”（Administrator Mode）并输入系统 root 密码进入实际安装界面。
- 2. 要找到 sendmail 包，在搜索框中输入 sendmail 并点击“搜索”（Search）。sendmail 包会在对话框的右上角显示列表。勾选复选框表示要安装该包，并点击安装和删除软件界面右下角的“接受”（Accept）按钮。
- 3. 如果您将 SUSE 系统配置为服务器系统，YaST 会作为基础服务器安装的一部分自动为您安装 Postfix。如果是这种情况，YaST 会显示如图 17-2 所示的“依赖冲突”（Dependency Conflict）对话框。从图中可以看出，YaST 自动检测到 sendmail 与当前安装的 Postfix MTA 存在冲突。
- 4. 如果包含 sendmail 包的介质不在 CD 或 DVD 驱动器中，YaST 将提示您插入相应的 CD 或 DVD 并继续安装。
- 5. 安装完成后，YaST 会显示一个对话框询问您是否要安装其他软件包。点击“否”（No），然后点击“确定”（OK）关闭 YaST 的“安装和删除软件”面板。

要解决此问题，请点击图 17-2 显示的“移除冲突”（Remove the Conflicting）按钮。点击“确定 - 重试”（OK - Try Again）继续。

# 第 17 章 + 邮件服务 — Postfix, Sendmail, Qpopper 和 Cyrus 481

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_525_0.png)

图 17-2：YaST 的依赖冲突对话框

## 配置 sendmail

sendmail 的主要配置信息存储在文件 /etc/sendmail.cf 中。额外信息存储在目录 /etc/mail 中。/etc/sendmail.cf 是一个文本文件，包含由文件不同行上的键/值对组成的配置信息。

大多数运行 sendmail 的系统都会从另一个文件 sendmail.mc 创建 /etc/sendmail.cf 文件，该文件通常存储在 /etc/mail（如 Red Hat 等 Linux 系统）或 /usr/lib/mail/cf（Solaris 系统）目录中。sendmail.cf 文件是使用 `m` 命令从 sendmail.mc 生成的，`m` 是一个宏处理器，可将 sendmail.mc 中的压缩信息扩展为更完整的 sendmail.cf。

幸运的是，SUSE 通过在 YaST 中提供图形化配置机制简化了 sendmail 配置。sendmail 的 YaST 配置模块及其使用的 脚本和配置文件都作为 SUSE 软件包的一部分自动安装。在 YaST 中配置任何 MTA 都在同一个位置完成，即“网络服务 邮件传输代理”（Network Services Mail Transfer Agent）。底层脚本实现了 SUSE Linux 上不同支持的 MTA（如 Postfix、sendmail 和 Exim）提供的任何更改或额外选项。本节描述了您可能需要在 YaST 的 sendmail 配置模块中设置或更改的最常见配置选项。

启动 YaST 的 MTA 配置模块（网络服务 -> 邮件传输代理）后，将出现图 17-3 所示的屏幕。

# 482 第四部分 ♦ 在 SUSE Linux 中实现网络服务

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_526_0.png)

图 17-3：指定您的网络连接

在此屏幕上，您可以识别运行 sendmail 的主机所使用的网络连接类型。如果您希望在接收传入邮件时自动包含病毒扫描，请勾选“启用病毒扫描 (AMViS)”复选框。（如果该包尚未安装，YaST 将 sendmail 配置过程结束时提示您插入相应的 CD 或 DVD 介质）。在此屏幕上选择适当选项后，点击“下一步”（Next）。显示图 17-4 所示的下一个屏幕。

如果您在希望能够接收和投递邮件的主机上配置 sendmail，但您的站点使用中心服务器来为互联网或其他本地网络中继邮件，请在此屏幕上输入该中心服务器的名称。如果 sendmail 需要验证此服务器以通过其发送邮件，请点击“身份验证”（Authentication）并输入 sendmail 应该使用的用户名和密码（这通常是一个名为 "sendmail" 的用户，已为其创建特定账户）。点击“确定”（OK）记录您所做的更改并返回“发出邮件”（Outgoing mail）面板，或点击“返回”（Back）在不进行任何更改的情况下返回“发出邮件”面板。

# 第 17 章 + 邮件服务器 – Postfix, Sendmail, Qpopper 和 Cyrus 483

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_527_0.png)

如果您希望来自您正在配置的主机的邮件看起来来自不同的域名，请点击“伪装”（Masquerade）并输入您希望出现在 sendmail 发送的邮件标头中的信息。此面板还允许您配置 sendmail，使来自特定本地用户的邮件看起来来自选定的位置，这对于不希望反映发送其特定主机名的系统账户非常有用。点击“确定”（OK）记录您所做的更改并返回“发出邮件”面板，或点击“返回”（Back）在不进行任何更改的情况下返回“发出邮件”面板。

点击“下一步”（Next）继续配置过程，并显示图 17-5 所示的屏幕。

此面板上最重要的设置是“接受远程 SMTP 连接”（Accept remote SMTP connections）设置。默认情况下，sendmail 监听在系统的回环接口上，并利用它在本地投递同样在本地发送的邮件。如果您希望您的系统能够接纳并投递从其他系统发送的邮件，您将需要启用“接受远程 SMTP 连接”设置。

# 484 第四部分 ♦ 在 SUSE Linux 中实现网络服务

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_528_0.png)

图 17-5：指定传入邮件参数

此面板上的其他设置允许您为 sendmail 指定检索和发送邮件的端口，并包含一个 sendmail 应该检索邮件以进行本地投递的远程邮件服务器。

此面板还允许您指定一个您希望投递邮件的中心地址。这是邮件别名（mail aliasing）最常见的示例，即指定发送给本地用户的邮件应该转发或投递到的目的地。点击“别名”（Alias）按钮将显示一个屏幕，允许您添加其他电子邮件别名，这些别名将存储在 /etc/mail/aliases 文件中。同样，点击“虚拟域名”（Virtual domains）按钮允许您指定发送给非本地用户的邮件应该转发或投递到的目的地。

点击“完成”（Finish）完成 sendmail 的配置。如果您启用了防病毒扫描且 AmAV 包尚未安装，YaST 将在此时提示您插入相应的 CD 或 DVD 介质。如果是这种情况，请插入相应的介质并等待安装完成。

YaST 通过运行 SUSEConfig for 来完成 sendmail 配置，该程序为您生成并更新 /etc/sendmail.cfg，以及 /etc/mail 中受您配置更改影响的所有文件。

