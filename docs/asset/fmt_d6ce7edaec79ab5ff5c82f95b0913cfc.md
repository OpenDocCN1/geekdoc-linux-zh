
| Address | Displays the DNS name or IP address of the Novell iFolder enterprise server where you have an account. Get this information from your Novell iFolder administrator. For example: srv21.example.com or 192.168.1.1. You can modify the address but you must be disconnected from the Novell iFolder server when you make the change. | Account Properties > Server tab | Yes |
| Server description | Displays information about the Novell iFolder server, such as its service location and Novell iFolder administrator contact information. The description is supplied by the server and is controlled by the Novell iFolder administrator. | Account Properties > Server tab | No |

### Table 13-3

要查看或修改账户设置：

1. 右键单击通知区域中的 Novell iFolder Services 图标；然后通过选择 Account Settings 从 Accounts 选项卡打开 Novell iFolder Preferences。
2. 在 Accounts 报告中，您可以为每个账户管理以下参数：
   - Online（选择以连接；取消选择以断开连接）
   - Name（仅查看）
   - User Name（仅查看）
3. 选择您要管理的 Novell iFolder 账户；然后通过选择 Properties 在 Server 选项卡上打开 Account Properties 对话框。
4. 在 Server 选项卡上，您可以为所选账户管理以下参数：
   - Name（仅查看）
   - Address（连接时仅查看；断开连接时可修改）
   - Server description（仅查看；滚动以查看所有信息）
   - Automatically connect（选择以启用；取消选择以禁用）
   - Account is default（选择以启用；仅在存在多个账户时可用）
5. 选择 Identity 选项卡以管理所选账户的以下参数：
   - User Name（仅查看）
   - Password（指定密码）
   - Remember password（选择以启用；取消选择以启用）
   - Automatically connect（选择以启用；取消选择以禁用）
   - Account is default（选择以启用；仅在存在多个账户时可用）
6. 选择 Disk Space 选项卡以管理所选账户的以下参数：
   - Quota（仅查看）
   - Used（仅查看）
   - Available（仅查看）
   - Automatically connect（选择以启用；取消选择以禁用）
   - Account is default（选择以启用；仅在存在多个账户时可用）
7. 完成后，关闭 Account Properties 对话框；然后关闭 Novell iFolder Preferences 对话框。

## Deleting a Novell iFolder Account

您可以指定是否仅从当前计算机中删除账户，或是否同时从服务器中删除您拥有的 Novell iFolders。

如果您仅从计算机中删除 Novell iFolder 账户：
- 该账户的本地 Novell iFolders 将恢复为普通文件夹。使用文件管理器查找并删除本地数据副本（如果不需要）。
- 您仍可从安装了 Novell iFolder 客户端的其他计算机访问 Novell iFolders。
- 当 Novell iFolder 客户端与 Novell iFolder 3.x 企业服务器一起使用时，您也可以通过 Novell iFolder 3.x Web 访问从任何地方访问文件。

如果您从服务器中删除 Novell iFolder 帐户：
- 您拥有的所有 Novell iFolders 均变为未共享状态。
- 成员计算机上 Novell iFolders 的本地副本将被还原为普通文件夹。如不需要数据，请使用文件管理器查找并删除本地副本。
- Novell iFolder 及其内容将从服务器中删除。
- 您将被移除为他人与您共享的 Novell iFolders 的成员。
- 帐户将从本地计算机中删除。

如果您决定在此或其他计算机上再次使用此帐户，则必须像刚创建时一样设置帐户及其 Novell iFolders。

要删除 Novell iFolder 帐户：
1. 右键单击通知区域中的 Novell iFolder Services 图标（ ）；然后从“帐户”选项卡打开 Novell iFolder 首选项，选择“帐户设置”。
2. 选择要删除的 Novell iFolder 帐户；然后选择“删除”。
3. 会弹出一条消息提示您确定删除操作的范围。执行以下任一操作：
   - 仅从当前计算机中删除 iFolder 帐户——确保取消选择“从服务器中删除我的 iFolder 和文件”；然后选择“是”。
   - 删除 iFolder 帐户以及服务器上的 iFolders 和文件——选择“从服务器中删除我的 iFolder 和文件”；然后选择“是”。
   - 取消删除——选择“否”以退出删除操作。您的帐户及其 Novell iFolders 保持不变。

## 为客户端配置 Novell iFolder 首选项

1. 右键单击通知区域中的 Novell iFolder Services 图标（ ）；然后从“常规”选项卡打开 Novell iFolder 首选项，选择“首选项”。
2. 为表 13-4 中列出的项目指定您的首选项。
3. 完成后，关闭 Novell iFolder 首选项对话框。

![](img/9129877170834ca9d5fdac5319bf5f12_549_0.png)

## 练习 13-6：在 SLED 10 工作站上设置并使用 Novell iFolder 客户端

在本练习中，您将在 DAxx SUSE Linux Enterprise Desktop 10 工作站上设置并使用 Novell iFolder 客户端。

您使用学生 DVD 2 上提供的 RPM 文件在工作站上安装 Novell iFolder 客户端。使用客户端，您可以同步 da-oes 上可用的文件，与另一用户共享 iFolder，将文件上传到 iFolder 服务器，并从服务器下载文件。

| 参数 | 描述 |
|---|---|
| 登录桌面时启动 iFolder | 配置系统在您使用设置了 Novell iFolder 帐户的本地用户名登录时启动 Novell iFolder。（一种方法是确保在退出桌面时 Novell iFolder 正在运行，以便它成为默认桌面会话的一部分。）对于启用了“记住我的密码”的帐户，同步将在指定的同步间隔在后台进行。否则，您必须手动启动 Novell iFolder。 |
| 创建 iFolders 时显示确认对话框 | 选择此选项可在每次创建 Novell iFolder 时收到确认消息，除正常的视觉提示（如 Novell iFolder 出现在 Novell iFolders 列表中）之外。取消选择此选项可停止接收确认消息。 |
| 通知共享 iFolders | 选择此选项可在您收到共享 Novell iFolder 的新邀请时在通知区域启用弹出消息。取消选择此选项可禁用弹出消息。您可以在 Novell iFolder 运行时选择“显示可用 iFolders”以在 Novell iFolder 浏览器中查看当前计算机上可供下载的 Novell iFolders 列表。 |
| 通知冲突 | 选择此选项可在同步文件时发生冲突时在通知区域启用弹出消息。取消选择此选项可禁用同步冲突的弹出消息。每当发生冲突时，Novell iFolder 错误图标会在 Novell iFolder 运行时显示在 Novell iFolder 上。 |
