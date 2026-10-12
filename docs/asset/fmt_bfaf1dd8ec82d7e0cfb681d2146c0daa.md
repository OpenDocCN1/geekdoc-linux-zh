
- c. 输入已启用使用 iFolder 的 Digital Airlines 员工的 `用户 ID` 和 `密码`；然后输入服务器的 DNS 名称（`DAx.your container.digita l airlines.com`）。

- d. 选择 `Login`。

将出现 Novell iFolder 位置窗口对话框。在此对话框中，您输入工作站上要存储用于与 iFolder 服务器同步的文件的文件夹。

默认位置是 `\\Documents and Settings\Student\My Documents\iFolder\username\Home`。

- 13. 选择 `OK` 接受默认位置。

将出现一个 Internet Folder 设置对话框。

- 14. 选择 `Enable automatic login at startup`；然后确保选中了 `Encrypt files`。

- 15. 选择 `OK` 继续。

将出现一个获取密码短语对话框。

- 16. 输入并重新输入 `novell` 作为密码短语。

- 17. 输入 `oneNet` 作为提示。

- 18. 选择 `OK` 继续。

将出现一个密码短语恢复对话框。

- 19. 确保选中了 `Enable pass phrase recovery`；然后选择 `OK`。

您已登录到 iFolder。

请注意系统托盘中的 iFolder 客户端图标。

- 20. 右键单击该图标；然后选择 `Account Information`。

将出现一个对话框，其中包含选项卡，可用于查看和设置 iFolder 客户端信息。

- 21. 选择 `View Activity` 选项卡。

向上滚动窗口，请注意 iFolder 客户端已成功连接到您的 iFolder 服务器，并且在 iFolder 服务器上创建了一个 iFolder 数据库。

还请注意，同步会频繁发生。

6-64

*此文档仅供 Novell 认证讲师使用。*

*严禁复制此文档。如需报告涉嫌复制行为，请致电 1-800-PIRATES。*

Version 1

- 22. 选择 `Preferences` 选项卡。

同步设置为每 5 秒自动同步一次本地文件的更改，每 20 秒自动同步一次应同步到工作站的文件。

- 23. 取消选中 `Automatic sync`；然后选择 `Apply`。

- 24. 在 iFolder 对话框保持打开的状态下，将多个文件复制到您登录用户的家目录（在 `Account Information` 选项卡中查看位置）。

您可能希望复制 My Pictures 文件夹中的图片。

- 25. 返回 iFolder 对话框，选择 `View Activity` 选项卡；然后选择 `Sync` 按钮（选项卡页面的顶部）。

- 26. 观察 iFolder 将文件同步到 iFolder 服务器时显示的消息。

片刻之后，将显示同步完成的消息。

文件现在已加密并存储在 iFolder 服务器上。

- 27. 重新打开 `Automatic sync`；然后选择 `Apply`。

## 第三部分：配置 iFolder 以记录调试信息

现在用户正在登录和登出 iFolder 并同步文件，您应该配置 iFolder 将调试信息写入日志文件。

请执行以下操作：

- 1. 打开终端窗口，输入 `su` 并输入密码 `novell` 切换为 root 用户。

- 2. 输入 `cd /var/opt/novell/ifolder/DocumentRoot`。

- 3. 输入 `mkdir logs`。

如果未创建 index.html，请让学生创建它，并在 index.html 文件上重新执行 chmod 命令；然后重新启动 iFolder 服务。

- 4. 输入 `ls -al` 并验证 logs 文件夹是否存在。

- 5. 编辑 `httpd_ifolder_unix.conf` 文件以开始记录 iFolder 信息：

  - a. 选择 `应用程序 > KDE 菜单 > 系统 > 文件管理器 - 超级用户模式`。

  - b. 输入密码 `novell`；然后选择 `OK`。

  - c. 浏览到 `/etc/opt/novell/ifolder`。

  - d. 右键单击 `httpd_ifolder_unix.conf` 文件；然后选择 `Open With > KWrite`。

  - e. 在文件末尾添加以下内容：

```
iFolderServerLogging “/var/opt/novell/ifolder/DocumentRoot/logs/index.html”
```

  - f. 保存 `httpd_ifolder_unix.conf` 文件。

- 6. 在 shell 提示符下输入以下内容，授予 Apache 创建和写入日志文件的权限：

```
chmod 757 /var/opt/novell/ifolder/DocumentRoot/logs
```

- 7. 在 shell 提示符下输入以下内容以重新启动 iFolder 服务：

```
/etc/init.d/novell-httpd stop
/etc/init.d/novell-httpd start
```

- 8. 输入 `cd /var/opt/novell/ifolder/DocumentRoot/logs`。

- 9. 输入 `ls -al` 验证 index.html 文件已创建。

- 10. 输入 `tail index.html`。

注意捕获到的 iFolder 服务器日志信息。

- 11. 保持此 `终端会话` 打开。

## 第四部分：修改和测试 iFolder 配置

现在您已安装 iFolder 客户端，激活 iFolder 用户，并同步了文件，您可以使用 iFolder 管理控制台来监控和配置 iFolder。

请执行以下操作：

- 1. 从您的 NNLS 服务器的 Mozilla 浏览器中，输入以下内容访问 iFolder 管理控制台：

`https://DAx.your*container*.digitalairlines.com`

`/iFolderServer/Admin`

将显示 Novell iFolder 欢迎页面。

- 2. 选择 `Reporting`。

- 3. 使用 `admin` 登录，密码为 `novell`。

在右侧“常规信息”下方，注意用户总数。

- 4. 在左侧 `Reporting` 下方，选择 `User Accounts`；然后在右侧选择 `Display`。

注意显示的已激活 iFolder 用户的数据。

- 5. 在页面顶部，选择 `User Management` 图标。

- 6. 输入 iFolder 用户的 `用户 ID`；然后选择 `Search`。

- 7. 选择 `用户 ID` 显示该用户的属性。

将显示属性页面。

查看显示的信息，例如磁盘配额、最后同步时间和已用空间。

- 8. 将磁盘配额更改为 `250 MB`；然后选择 `Update`。

- 9. 向下滚动到页面底部，通过选择 `Edit` 编辑该用户的客户端策略。

将显示该用户的策略页面，其中包含可从 iFolder 客户端获得的几种设置的配置。

## 目标 2 配置 iFolder（续）

1. 对于自动同步，选择`强制`。

2. 对于保存口令，选择`隐藏`。

3. 对于同步到服务器延迟，输入`30`；然后选择`强制`。

4. 对于 iFolder 位置，选择`隐藏`。

5. 选择`更新`。

6. 返回到`终端会话`；然后输入 `tail index.html`。

注意捕获到的调试输出。随时返回并刷新此窗口，以查看当发生 iFolder 事件时（即，注销和重新登录，同步文件等）记录了哪些类型的信息。

7. （可选）在文件管理器 - 超级用户会话中，你可以浏览到 index.html 文件并双击它以查看其完整内容，并在需要时刷新它。

8. 测试 iFolder 用户的新配置：

  - a. 从你的 Windows 工作站，通过执行以下操作之一注销 iFolder 客户端：

    - 如果你的 iFolder 客户端对话框是打开的，选择`文件` > `注销`。

    - 如果你的 iFolder 客户端对话框是关闭的，右键单击系统托盘中的 iFolder 客户端图标；然后选择`注销`。

  - b. 通过右键单击系统托盘中的 `iFolder 图标` 来登录你的 iFolder 用户；然后选择`登录`。

  - c. 对于你更改了设置的 iFolder 用户，输入`用户 ID` 和密码 `novell`；然后从下拉列表中选择你的服务器 DNS 名称。
