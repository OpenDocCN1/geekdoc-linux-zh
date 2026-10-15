
WebAdmin 是用于配置 NetMail 系统的实用工具。它是一个基于浏览器的实用工具，集成到 iManager 中。

要直接访问 WebAdmin，请打开 Web 浏览器并输入 `http://your_server_IP:8018` 或 `https://your_server_IP:8020`

要从 iManager 内部访问 WebAdmin，请完成以下操作：
1. 在左侧，向下滚动并选择 Launch NetMail Management。
2. 在 WebAdminServer 名称字段中，浏览并选择您的 WebAdmin 服务器；然后选择 确定。

### 配置 NMAP 代理服务的上下文

NetMail 系统服务于在 NMAP 代理的 Context 属性中配置的所有容器中的所有用户，如下所示：

![](img/d63035f3fce0eaaf97203dde900affb7_213_0.png)

第一个上下文是在创建 NMAP 代理时定义的，与服务器所在的上下文相同。可以从 Context 页面添加额外的用户上下文。

由于 NMAP 上下文不是继承的，因此 NMAP 代理服务的每个容器或子容器都必须添加到该代理的上下文列表中。

消息服务自动提供给 NMAP 代理分配的上下文中的每个用户。用户邮箱在用户第一次收到消息时在本地消息存储目录中创建。

> 请勿将同一上下文添加到多个 NMAP 代理中。

NMAP 上下文由消息服务器跟踪。启动时，消息服务器生成 NMAP 上下文列表并将其保存在服务器内存中。此列表用于生成别名和地址簿。

对上下文列表所做的更改是动态更新的。无需重新启动 NetMail 服务。但是，如果在服务器运行时向上下文中添加用户，他们不会出现在地址簿中，直到服务器重启。

要配置由 NMAP 代理服务的 eDirectory 上下文，请执行以下操作：
1. 在 WebAdmin 中，展开 `Internet Services`。
2. 展开 `Messaging Server`。
3. 选择 `NMAP Agent`。
4. 选择 `Context`。
5. 选择 放大镜 图标。
6. 浏览并选择您希望 NMAP 代理服务的每个 容器；然后选择 保存。
7. 选择 保存。

### 选择 Web 界面模板

模板控制模块化 Web 代理的邮件客户端界面的外观。默认情况下，NetMail 附带 2 个模板：
- WebAccess (`Webacc.CTP`)
- WebMail (`WebMail.CTP`)

每个模板都包含展示其相应客户端界面所需的全部内容。当模块化 Web 代理在消息服务器上初始化时，它只需将模板文件加载到内存中。

要选择默认模板，请执行以下操作：
1. 在 `WebAdmin` 中，展开 `Internet Services`。
2. 展开 `Messaging Server`。
3. 选择 `Modular Web Agent`。
4. 向下滚动到 默认模板 字段，如下所示：

![](img/d63035f3fce0eaaf97203dde900affb7_215_0.png)

5. 选择 放大镜 图标。
6. 浏览并选择您要使用的 模板对象。
7. 默认情况下，模板位于 `Templates.Internet Services` 中。
8. 选择 保存。

> 如果使用 Mozilla 浏览器访问 WebAccess 或 WebMail 时输入了错误的登录信息，则不会显示登录对话框。
>
> 您必须刷新窗口或重新输入 URL。如果在注销 WebAccess 或 WebMail 后单击“重新登录”链接，您将到达注销页面。您必须启动一个新的浏览器才能到达登录提示。

![](img/d63035f3fce0eaaf97203dde900affb7_216_0.png)

即使您使用的是 IP 地址而不是 DNS 名称，消息服务器也依赖于 DNS 服务器作为名称解析器。

### 练习 8-1 配置并测试您的数字航空办公室的 NetMail

在本练习中，您将配置 NMAP 代理以服务您的整个容器并测试邮件服务器。

执行以下操作：
1. 验证 sendmail 未在运行：
   a. 在您的 NNLS 服务器上，打开一个终端会话。
   b. 通过输入 `su -` 和密码 `novell` 切换到 root 用户。
   c. 输入 `chkconfig --list sendmail`。
      `sendmail` 守护进程应设置为在运行级别 3（非图形引导）和 5（图形引导）下关闭。
2. 通过输入 `ping DAx.your container.digitalairlines.com` 来确保 DNS 正确解析您服务器的 IP 地址（按 `Ctrl+C` 停止 ping）。
   例如，如果您在 DA3 上工作，则输入 `ping DA3.atl.digitalairlines.com`。
3. 访问 WebAdmin 并验证 NetMail 已配置为服务您容器中的用户：
   a. 在您的 NNLS 服务器上，打开浏览器窗口并输入 `https://DAx.your container.digitalairlines.com:8020`。
      Novell WebAdmin 登录页面出现。
   b. 以 admin 身份登录，密码为 `novell`。
   c. 在左侧，展开 `Internet Services`。
   d. 展开 `DAx Messaging Server`。
   e. 选择 `NMAP Agent`。
   f. （条件）如果出现 About Popups 对话框，请选择 否。将出现带有多个选项卡的 NMAP Agent 页面。
   g. 选择 `Context` 选项卡。
   h. 验证您的容器是否已列出。
   i. （条件项）如果您的容器未被列出，请添加 您的容器（使用放大镜图标）；然后选择 保存。
4. 验证您的 POP 代理是否已启用：
   - a. 在 `DAx 消息服务器` 下，选择 `POP 代理`。
   - b. 验证代理是否已启用。
   - c. （条件项）如果代理未启用，请选择 已启用，然后选择 保存。
5. 设置服务器时区：
   - a. 在左侧，选择 模块化 Web 代理。
   - b. 在右侧的默认时区下拉列表中，选择 您的时区。您这样做是为了确保消息服务器的时区与 NNLS 服务器的时区相同。
   - c. 选择 保存。
6. 测试配置。
   - a. 在当前 Mozilla Web 浏览器窗口中，通过按 `Ctrl+N` 打开一个新的浏览器窗口。
   - b. 输入 `http://DAx.your container.digitalairlines.com:52080`。
   - c. 当提示登录时，输入用户名为 `JJackson`，密码为 `novell`；然后选择 确定。此时将显示 WebAccess 页面。
   - d. 在左侧，选择 撰写 图标。
   - e. 在收件人字段中，输入 `AGresko@your container.digitalairlines.com`。例如，如果您正在 DA3 上工作，则输入 `AGresko@atl.digitalairlines.com`。
   - f. 在主题和正文字段中，输入 文本。
如果正文字段留空，消息将不会发送。
   - g. 选择 发送。
   - h. 等待发送窗口关闭；然后，在 Web/Access 页面顶部，选择 退出 图标。
   - i. 选择 登录。
   - j. 当提示登录时，以用户名为 `AGresko`，密码为 `novell` 进行身份验证。
     您应该能看到刚从另一个账户发送的消息。
   - k. 选择该 消息。
   - l. 尝试向您树中的其他用户发送电子邮件。
   - m. 尝试向另一棵树中的用户发送电子邮件消息。
   - n. 完成后，关闭浏览器窗口。

*（练习结束）*

### 摘要

| 目标 | 摘要 |
| :--- | :--- |
| 1. 识别 NetMail 功能 | Novell NetMail 是一个基于互联网标准消息和安全协议的高性能电子邮件和日历系统。 |
| | NetMail 旨在适应多种网络环境。它已在单个 Linux 服务器上成功测试支持多达 30,000 名用户。 |
| | NetMail 高效的分层架构将运行电子邮件和日历系统所需的服务器数量降至最低。 |
| | NetMail 与 Novell eDirectory 紧密集成。 |
| | NetMail 还可以将电子邮件和日历服务分布在多个服务器上。这提高了性能，同时防止关键进程因系统故障而中断。 |
| 目标 | 摘要 |
| :--- | :--- |
