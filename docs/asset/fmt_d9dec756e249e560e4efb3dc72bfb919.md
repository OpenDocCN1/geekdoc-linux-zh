
![](img/9129877170834ca9d5fdac5319bf5f12_543_0.png)

图 13-35

- 4. 在密码短语字段中输入您的秘密密码短语，并在验证时重新输入相同的密码短语。
- 5. （可选）要在当前会话期间自动访问加密的 Novell iFolder 数据，请选择记住密码短语。

  如果您选择此选项，Novell iFolder 可以记住您的密码短语。下次您开始登录过程时，此密码短语交换将自动完成；不会出现对话框。
- 6. 从列表中选择所需的恢复代理，然后选择确定。

  将显示图 13-36 所示的对话框。

![](img/9129877170834ca9d5fdac5319bf5f12_543_1.png)

图 13-36

7. 验证您输入的信息是否正确；然后验证设置并通过选择 Connect 登录到 Novell iFolder 服务器。
8. （条件）如果系统提示您接受此服务器的证书，请选择 Details 查看证书信息；然后选择 Yes 接受它。如果您不接受证书，则无法连接到服务器。
9. 连接成功后，通过选择 Finish 关闭 Novell iFolder Account Assistant。

Novell iFolder 会同步指定账户的用户列表并识别可供下载的 Novell iFolders。此初始下载可能需要几秒钟到几分钟，具体取决于账户用户列表的大小。

10. 验证您设置的账户是否出现在账户列表中：

a. 右键单击通知区域中的 Novell iFolder Services 图标；然后从菜单中选择 Preferences 以打开 Novell iFolder Preferences 对话框的 Accounts 选项卡。

显示了图 13-37 中的 Novell iFolder Preferences 对话框。

![](img/9129877170834ca9d5fdac5319bf5f12_544_0.png)

Figure 13-37

当您连接到 Novell iFolder 服务器时，Online 复选框会被选中。

b. 关闭 Novell iFolder Preferences 对话框。

11. 使用以下任一方法为账户设置 Novell iFolders：

- 右键单击通知区域中的 Novell iFolder Services 图标 (?)；然后选择 iFolders 以打开 Novell iFolder 浏览器。参见图 13-38。
- 如果 Novell iFolders 可从服务器下载，则 Novell iFolder Notification 消息图标 (?) 会出现在任务栏通知区域旁边。单击该消息以打开 Novell iFolder 浏览器。

![](img/9129877170834ca9d5fdac5319bf5f12_545_0.png)

Figure 13-38

## Logging In to a Novell iFolder Account

您可以在任何时候在 Novell iFolder 目录中本地处理文件。您必须登录到 Novell iFolder 账户才能同步用户列表、同步 Novell iFolder 数据、上传新的 Novell iFolders、下载共享的 Novell iFolders、共享 Novell iFolders 以及管理 Novell iFolders。您可以分别登录并同时登录多个账户。

对每个账户使用以下其中一种登录方法：

- `Log In Automatically`—如果您希望在 Novell iFolder 客户端启动时自动登录，请为您的 Novell iFolder 账户启用 Remember My Password。您可以在配置账户时启用 Remember My Password，也可以在之后修改账户设置时启用。

每当您的密码更改时，下一次 Novell iFolder 尝试登录 Novell iFolder 账户时，自动身份验证会优雅地失败。Novell iFolder 会提示您登录；然后您可以输入新密码。之后，如果需要，您可以再次启用 Remember My Password。
- `Log In As Needed`—如果您只希望在需要时登录 Novell iFolder 账户，请禁用 Remember My Password。

要为现有 Novell iFolder 账户启用或禁用 Remember My Password，请执行以下操作：

1. 右键单击通知区域中的 Novell iFolder Services 图标 ( )；然后通过选择 Account Settings 从 Accounts 选项卡打开 Novell iFolder Preferences 对话框。
2. 选择 Novell iFolder 账户；然后通过选择 Properties 在 Novell iFolder Account Assistant 中查看其设置。
3. 按照屏幕上的说明指定 `password`。
4. 选择（启用）或取消选择（禁用）Remember My Password。
5. 验证您输入的设置；然后保存更改并通过选择 Connect 登录到服务器。

要登录 Novell iFolder 账户，请执行以下操作：

1. 右键单击通知区域中的 Novell iFolder Services 图标 ( )；然后选择 Account Settings。
2. 选择 Novell iFolder 账户；然后选择 Online 复选框。
3. 如果系统提示输入密码，请指定 `password`；然后选择 Connect。

如果为账户启用了 Remember My Password，则除非您的密码已过期，否则不会提示您输入密码。

如果登录失败，错误消息会报告原因，例如密码失败。

4. 连接成功后，关闭 Novell iFolders Properties 对话框。

## Logging Out of a Novell iFolder Account

每当您想离线工作时，请退出 Novell iFolder 账户。

1. 右键单击通知区域中的 Novell iFolder Services 图标 ( )；然后通过选择 Account Settings 从 Accounts 选项卡打开 Novell iFolder Preferences。
2. 找到您要管理的 `account`；然后通过取消选择 Online 复选框与 Novell iFolder 服务器断开连接。
3. 通过选择 Close 关闭 Novell iFolders Preferences 对话框。

## Viewing and Modifying Novell iFolder Account Settings

表 13-3 中列出的参数可以在 Account Settings 和 Account Properties 对话框中查看。

| Parameter | Description | Location | Modifiable by User (Yes/No) |
|---|---|---|---|
| Online | Indicates whether you are currently connected to the Novell iFolder server for an account. Select the Online check box next to the account to connect to the Novell iFolder server for this account. Deselect the Online check box next to the account to disconnect from the Novell iFolder server. | iFolder Preferences > Accounts tab | Yes |
| Name | Displays the descriptive name of the Novell iFolder server where your Novell iFolders are stored for the account. This name is supplied by the server and is controlled by the Novell iFolder administrator. | iFolder Preferences > Accounts tab Account Properties > Server tab | No |
