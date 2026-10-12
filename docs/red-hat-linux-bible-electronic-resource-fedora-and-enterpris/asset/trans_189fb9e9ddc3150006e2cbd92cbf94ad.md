
updates. 与 `rhn_register` 一样，你需要对计算机拥有 root 权限才能运行 `up2date`。这是因为 `up2date` 需要权限来更改配置文件并安装软件包。

`up2date` 配置文件 (`/etc/sysconfig/rhn/up2date`) 决定了 `up2date` 的行为。以下是 `up2date` 配置文件中的一些关键设置，帮助你了解启动它时 `up2date` 会做什么：

- 默认情况下调试是禁用的。如果 `up2date` 出现问题，将 `debug=0` 改为 `debug=1` 以启用调试。
- 下载的软件包存储在 `/var/spool/up2date` 目录中。安装后，软件包会被删除（默认情况下）。
- `up2date` 日志文件是 `/var/log/up2date`。你可以在任何文本编辑器中打开该文件，以查看 `up2date` 所做的一切的描述。
- 以单词 `kernel` 开头的任何软件包都会被跳过。将你想要跳过的其他软件包名称添加到 `pkgSkipList=kernel*` 条目中。你可以使用 shell 通配符，例如示例中显示的星号，来匹配所有内核软件包。

`up2date` 配置文件包含其他设置，可用于进一步优化你的 `up2date` 会话。例如，你可以指定 HTTP 代理服务器，更改退出前必须发生的失败网络连接尝试次数，或指示你希望连同二进制软件包一起检索源软件包。

`up2date` 源文件 (`/etc/sysconfig/rhn/sources`) 是另一个你可能考虑增强的配置文件。特别是，如果你想从 yum 或 apt 仓库获取已安装在系统上的软件包的更新，可以将这些仓库的位置添加到此文件中。以下两行分别包含可添加到 sources 文件中的 yum 和 apt 仓库条目的示例：

```
yum fedora-9-i386-stable http://download.fedora.us/fedora/redhat/9.0.93/i386/yum/stable
apt freshrpms-9-i386 http://ayo.freshrpms.net redhat/9/i386/ updates freshrpms
```

yum 示例将服务显示为 `yum`，频道名称为 `fedora-9-i386-stable`，后面跟着 yum 仓库的位置。在 apt 示例中，仓库分为三部分：主机名、路径和最终目录。请注意，在此示例中，`updates` 和 `freshrpms` 目录都是可用的仓库。一旦你添加了与刚才显示类似的行，它们在运行 `up2date` 时会在 Channel 窗口中作为频道出现。

要使用来自 Red Hat Inc. 的软件包的官方位置，你只需使用默认的 `up2date` 设置。以下是 `up2date` 会话的示例：

- 1. 输入 **up2date** 或单击通知图标并选择启动 `up2date`。如果你的系统尚未拥有 Red Hat 公钥，系统会询问你是否希望 `up2date` 安装它。（该密钥用于验证你收到的软件包是否由 Red Hat 签名。）
- 2. 单击“是”以安装密钥。Red Hat Update Agent 窗口出现。
- 3. 单击“前进”。Channels 窗口出现。
- 4. Channel 表示你正在运行的 Red Hat Linux 版本。选择适合你的 Red Hat 安装的 Channel 并单击“前进”。Update Agent 开始检查你的可用软件包。
- 5. Available Package Updates 窗口出现，显示可供更新的软件包。单击你想要更新的每个软件包，或单击“Select All Packages”以更新所有适用的软件包。你可以单击某个软件包，然后单击“View Advisory”以查看该软件包更新所解决的公告。
- 6. 单击“前进”继续。Update Agent 开始测试软件包以检查你正在更新的软件包之间的依赖关系。如果所选软件包产生任何依赖关系，则会出现“Packages Required to Solve Dependencies”窗口，列出你需要的额外软件包。
- 7. 单击“前进”将显示的软件包包含在更新中（或单击后退按钮更改软件包列表）。Retrieving Packages 窗口出现，并在软件包从 Red Hat Network 下载时记录进度。
- 8. 单击“前进”开始将软件包下载到你的计算机。（这可能需要一段时间，具体取决于你的 Internet 连接速度和正在下载的软件包数量。）
- 9. 当所有软件包下载完成后，单击“前进”。Installing Packages 窗口出现。
- 10. 单击“前进”开始安装你已下载的软件包。
- 11. 当所有软件包安装完成后，单击“Next”。All Finished 窗口出现，显示每个已安装软件包的名称和版本。
- 12. 单击“Finish”结束会话。

如果你有兴趣查看升级情况，可以执行以下操作：

- 检查日志文件 (/var/log/up2date)。
- 查看是否有任何软件包遗留在 spool 目录 (/var/spool/up2date) 中。

虽然此时你不一定需要重新启动 Linux，但如果随任何已更新的软件包安装了新的守护进程，你可能希望重新启动它们。例如，要重新启动你的 Web 服务器 (httpd 守护进程)，你可以作为 root 用户输入以下内容：

```
# /etc/init.d/httpd restart
```

## 使用 Red Hat Network

一旦你拥有 Red Hat Network 账户，你就可以登录到 RHN 网站并利用它提供的服务。如前所述，每个注册用户有权注册一台计算机以接收自动更新。仅通过在 Red Hat Network 网站注册即可获得的其他服务包括：

- 可以查看完整的可用勘误表列表，包括安全、错误修复和增强警报。勘误表按 Red Hat Linux 版本组织，以便于确定兼容性问题。
- 勘误表的电子邮件警报以及修复问题的新可用软件包的通知。
- 一个授权管理器，显示你有权通过 RHN 管理的系统，并允许你添加更多系统。
- 一个用于安排操作的功能，例如在指定时间自动更新软件包。

转到 Red Hat Network 网站 (rhn.redhat.com) 并使用你在前面描述的 rhn_register 会话期间创建的用户名和账户登录。使用此页面上的链接浏览 RHN 网站。可用的部分包括：

- **Your RHN** — 包含可能包含过时软件包的系统的通知。Your RHN 中的部分包括：Your Account（包含个人信息，如姓名、地址、电子邮件等）和 Your Preferences（你可以在其中指定是否希望接收电子邮件勘误表）。
- **Systems** — 让你查看 System List，其中包含你已在 RHN 注册的所有系统，或使用搜索工具搜索你的系统列表。
- **Errata** — 从 Errata 页面你可以显示所有勘误表，仅显示适用于你的系统的勘误表，或对可用勘误表进行关键词搜索。
- **Software** — 一个频道指定了与其关联的软件包更新的 Red Hat Linux 版本。通过在此部分中选择 Channel List，你可以看到你正在使用的 Red Hat Linux 版本可用的软件包版本。
- **Schedule** — 你可以安排软件包安装在稍后时间进行。从此页面你还可以查看待处理、已完成和已归档的操作。
- **Help** — 如需更多关于 Red Hat Network 的帮助，Help Desk 提供 RHN FAQ、客户服务支持链接、支持论坛和 RHN 参考指南。

如果你想购买额外的授权，我建议你查看 Red Hat Network 网站以获取最新价格。在撰写本文时，Fedora Core 可用 $60 每年的 Basic Service Entitlement。该授权让你获取更新的软件包，但不提供来自 Red Hat, Inc. 的任何技术支持。（以前，使用 Red Hat Linux 时，你还可以获得有限的安装支持，但 Fedora 不提供。）为了获得官方支持，Red Hat 鼓励客户升级到 Red Hat Enterprise Linux 并购买 $96 每年的 Enterprise Service Entitlement。

在不购买额外授权的情况下，你可以向 RHN 注册额外的系统。但是，你不能使用更新机制来更新这些额外的系统。要注册额外的系统，只需从每个系统运行 rhn_register 命令即可
