
## 实验 10.1：实施 NetMail

在这个实验中，你将配置服务器上的 NetMail。然后，你将在 eDirectory 树中的两个用户之间来回发送电子邮件消息。

为了完成这个实验，你必须确保在第 5 章中配置的 DNS 服务器（由 named 守护进程提供）正在你的服务器上运行，并且已配置为服务 CLE.com 区域。如果你尚未配置它，请在开始此练习之前回到第 5 章并完成那些步骤。
此外，如果你决定使用另一台工作站来测试你的 NetMail 系统，你需要配置其 TCP/IP 栈以使用你的 Linux 服务器作为 DNS 服务器。

完成以下步骤：

1. 通过执行以下操作来验证你的 DNS 服务器是否正确解析：
   a. 在你的 Linux 服务器上，打开一个终端会话。
   b. 以 eDirectory 树中的用户（例如 CGrayson）登录，密码为 **novell**。
   c. 通过输入 `su` 切换到你 root 用户账户 —— 密码为 **novell**。
   d. 在 shell 提示符下，输入 `nslookup`。
   e. 在提示符下，输入 `cle1.cle.com`。
   f. 你的 named 服务应将该名称解析为你服务器的 IP 地址。

如果解析不正确，请通过输入 `chkconfig -list named` 验证服务是否正在运行。该服务应配置为在运行级别 3、4 和 5 时启动。还要检查你的 `/etc/named.conf` 文件，确保存在指向 `/var/named/named.hosts` 文件的 `cle.com` 区域条目。检查你的 `/var/named/named.hosts` 文件，确保存在你 CLE1 服务器的记录。

   g. 输入 `exit`。

2. 使用 `chkconfig` 命令，确保 postfix 和 sendmail 在运行级别 3、4 和 5 时设置为 **off**（关闭）。

3. 通过完成以下操作来配置由 NetMail 服务器服务的 eDirectory 树中的上下文：
   a. 打开浏览器窗口并导航至 http://your_server_IP_address:8018。
   b. 在 **用户名** 字段中，输入 **admin.if.cle**。
   c. 在 **密码** 字段中，输入 **novell**。
   d. 展开你的 **Internet Services** 容器。
   e. 展开你的 **CLE1 Messaging Server** 对象。
   f. 选择你的 **NMAP Agent** 对象。
   g. 选择 **Context** 选项卡。这样做后，将显示图 10.28 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_482_0.png)

> **图 10.28**
> 为 NMAP Agent 设置用户上下文。

   h. 管理的上下文字段应自动填充 CLE1 服务器对象所在的树的上下文（在这种情况下，为 **IF.CLE**）。
   i. 点击 **浏览** 图标。
   j. 浏览到并选择 **SLC.CLE** 容器。
   k. 点击 **保存**。
   l. 在 **Contexts** 选项卡中，点击 **保存**。

4. 通过完成以下操作将 outgoing 消息的大小限制为 2MB：
   a. 在左侧框架中，选择你的 **SMTP Agent** 对象。
   b. 向下滚动到 **消息大小限制** 下拉列表。
   c. 在消息大小限制下拉列表中，选择 2。
   d. 点击保存。

5. 选择你的 POP Agent，并验证其 Agent 状态是否设置为启用。

6. 选择你的 IMAP Agent，并验证其 Agent 状态是否设置为启用。

7. 通过完成以下操作配置你的 AntiSpam Agent 以阻止来自 SpamsIsUs.com 域名的消息：
   a. 在左侧框架中，选择你的 AntiSpam Agent 对象。
   b. 通过在“Send Back”下标记“是”来配置 AntiSpam Agent 将垃圾邮件消息返回给发件人。
   c. 通过在“CC Postmaster”下标记“是”来配置 AntiSpam Agent 将垃圾邮件消息的副本发送回发件人的 postmaster。
   d. 在“Blocked Sites”字段中，输入 SpamsIsUs.com。
   e. 点击保存。

8. 通过完成以下操作配置你的 NetMail 服务器的 Modular Web Agent：
   a. 在左侧框架中，选择你的 Modular Web Agent 对象。
   b. 在默认语言下拉列表中，选择你的语言。
   c. 在默认时区下拉列表中，选择你的时区。
   d. 向下滚动到默认模板字段。验证它是否设置为使用 WebAccess 模板。
   e. 点击保存。
   f. 展开你的 Modular Web Agent 对象。
   g. 选择 IMS Mail Module。
   h. 在消息大小限制下拉列表中，选择 2。
   i. 在地址簿下的个人部分中，选择启用。
   j. 在全系统下，选择启用。
   k. 在全系统下的字段中，输入你的服务器 IP 地址。
   l. 在默认 LDAP 服务器下，选择启用。
   m. 在默认 LDAP 服务器下的字段中，输入你的服务器 IP 地址。
   n. 点击保存。

9. 通过完成以下操作测试你的 NetMail 系统：
   a. 打开一个新的浏览器窗口并导航至 http://your_server_IP_address:52080。
   b. 当出现提示时，以 **CGrayson** 身份进行身份验证，密码为 **novell**。NetMail Web 用户界面使用 WebAccess 模板显示，如图 10.29 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_484_0.png)

**图 10.29**
NetMail WebAccess 模板。

   c. 选择 **添加文件夹**。
   d. 在 **文件夹名称** 字段中，输入 MyStuff。
   e. 标记 **邮箱** 然后点击 **确定**。
   f. 切换回你的终端会话。
   g. 在 shell 提示符下，输入 `cd /var/opt/novell/netmail/users/CGrayson`。
   h. 输入 `ls`。
   i. 你应该能在 CGrayson 的目录中看到 MyStuff.box 和 MyStuff.idx 文件，如图 10.30 所示。
   j. 切换回你的浏览器窗口。
   k. 在屏幕的最左侧，点击 **编写消息** 图标。**邮件消息** 屏幕出现，如图 10.31 所示。
   l. 在 **收件人** 字段中，输入 DNElson@CLE.com。
   m. 在 **主题** 字段中，输入测试消息。

![](img/c7771e8540507f2b00c088c7a411b57b_485_0.png)

**图 10.30**
用户邮箱文件夹文件。

![](img/c7771e8540507f2b00c088c7a411b57b_485_1.png)

**图 10.31**
创建新的邮件消息。

   n. 在 **消息** 字段中，输入 **测试消息**。
   o. 点击 **发送**。
   p. 在 **WebAccess** 屏幕中，点击 **退出** 图标。
   q. 选择 **登录**。
   r. 在 **用户名** 字段中，输入 **DNelson**。
   s. 在 **密码** 字段中，输入 **novell**。
   t. 应该显示来自 CGrayson 的 **测试消息** 电子邮件，如图 10.32 所示。
   u. 选择 **测试消息** 电子邮件。
   v. 点击 **关闭** 图标。

![](img/c7771e8540507f2b00c088c7a411b57b_486_0.png)

**图 10.32**
D'Nelson 收件箱中的新消息。

10. 通过完成以下操作测试你的地址簿 Agent 和你的 Modular Web Agent 的功能：
    a. 点击 **编写消息** 图标。
    b. 点击 **地址簿** 按钮。
    c. 在 **搜索** 字段中，输入 **Jackson**。
    d. 选择 **搜索**。
    e. 在 **全系统** 下，标记 **Jim Jackson** 用户。
    f. 选择 **收件人**：。
    g. 点击 **编写**。
    h. 在 **主题** 字段中，输入 **新消息**。
    i. 在 **消息** 字段中，输入 **新消息**。
    j. 点击 **发送**。
    k. 注销并重新以 **JJackson** 身份登录，密码为 **novell**。
    l. 你应该能在 Jim Jackson 的收件箱中看到 **新消息** 电子邮件。

11. 点击 **退出** 图标。

现在你拥有一个功能齐全的 NetMail 系统，并与你的 eDirectory 树完全集成。你不再需要为你的电子邮件系统维护单独的用户账户。如果你将用户添加到由你的 NMAP Agent 支持的上下文中，他或她会自动拥有电子邮件账户。除非是在最小的组织中，否则这可以带来巨大的时间（和成本）节约。

让我们回顾一下你在本章中所学的内容。

## 总结

在本章中，你学习了 NetMail 的功能和好处。你了解到 NetMail 与 eDirectory 完全集成，易于部署，具有模块性，并且具有高度可扩展性。你还了解到 NetMail 的模块性是使用模块化的 agent 创建的，包括以下：

- 地址簿 Agent
- 别名 Agent
- 反垃圾邮件 Agent
- 反病毒 Agent
- 自动回复 Agent
- 日历 Agent
- 连接管理器 Agent
- IMAP Agent
- 列表服务器 Agent
- 模块化 Web Agent
- NMAP Agent
- POP Agent
- 代理 Agent
- SMTP Agent

你还了解到，安装 NetMail 会扩展你的 eDirectory 树架构，为你的组织、组织单元、服务器和用户对象添加几个新的对象类以及新属性。

然后你学习了用于消息存储和消息队列的 Linux 服务器文件系统中的目录。你还了解到，NetMail 系统是使用 WebAdmin 实用程序配置的，这与你用于配置其他 NLM 产品的 iManager 实用程序是分开的。

你了解到，NetMail 在接收到电子邮件消息时会创建两个文件：一个控制文件和一个数据文件。然后你了解了这些文件在 NetMail 系统中处理时所经过的九个阶段。

