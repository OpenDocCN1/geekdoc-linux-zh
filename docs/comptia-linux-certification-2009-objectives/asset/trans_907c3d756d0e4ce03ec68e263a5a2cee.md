

6. 使用 vi 编辑器，创建一个名为 `generic_map` 的文件。
7. 输入 `{用户名@DomainName1} {用户名@DomainName1}`
8. 保存并关闭该文件。
9. 输入 `postmap generic_map < generic_map` 以重新生成该文件的索引。
10. 输入 `service postfix restart` 以重启 postfix 服务。

## 流程参考：配置 Postfix 限制

要配置 postfix 限制：

1. 以 root 身份登录。
2. 使用 vi 编辑器打开 `/etc/postfix/main.cf` 文件。
3. 在文件末尾，输入 `smtpd_sender_restrictions = check_sender_access hash:/etc/postfix/sender_access, [由逗号分隔的零个或多个邮件发送方限制列表]` 以定义发送方限制。
4. 输入 `smtpd_client_restrictions = check_sender_access hash:/etc/postfix/client_access, [由逗号分隔的零个或多个邮件客户端限制列表]` 以定义客户端限制。
5. 输入 `smtpd_recipient_restrictions = check_sender_access hash:/etc/postfix/recipient_access, [由逗号分隔的零个或多个邮件客户端限制列表]` 以定义接收方限制。
6. 保存并关闭该文件。
7. 导航至 `/etc/postfix` 目录。
8. 打开发送方、接收方或客户端访问文件。
9. 定义限制。
   - 输入 `DomainName RELAY` 以允许中继。
   - 输入 `DomainName OK` 以接受来自指定域的邮件消息。
   - 输入 `DomainName REJECT` 以拒绝从指定域发送的邮件消息。
   - 输入 `DomainName ERROR: (### 消息)` 以拒绝来自发送方的邮件并显示任意消息。
   - 输入 `DomainName DISCARD` 以在接受消息后将其丢弃。
10. 保存并关闭该文件。
11. 输入 `postmap 发送方或接收方或客户端访问文件 < 发送方或接收方或客户端访问文件` 以构建相应的访问数据库。
12. 输入 `service postfix restart` 以重启 postfix 服务。

## 活动 13-4

### 配置 Postfix

**开始之前：**

1. 在 srvA 上，切换到 GUI。选择 **系统**→**管理**→**网络**。在 **网络配置** 对话框中，选择 **DNS** 选项卡。
2. 在 **主机名** 文本框中，输入 *srvA.ourglobalcompany.com* 并按 **Tab** 键。将 *192.168.0.2* 设置为主 DNS 和 DNS 搜索路径。
3. 选择 **主机** 选项卡。在 **地址** 文本框中，将 *192.168.0.2* 输入为 IP 地址。在 **主机名** 文本框中，将 *srvA.ourglobalcompany.com* 输入为主机名。在 **别名** 文本框中，将 *srvA ourglobalcompany.com* 输入为别名。
4. 在 **添加 / 编辑主机条目** 对话框中，点击 **确定**。保存配置并点击 **确定** 以重启网络服务。
5. 在 srvA 上，切换到 CLI。您已在 CLI 中以 root 身份登录。显示第一个终端。在命令提示符下，输入 `service sendmail stop` 以停止 sendmail 服务。输入 `chkconfig sendmail off` 以停止在系统启动时启用 sendmail 服务。清屏。
6. 在 srvB 上，切换到 GUI。选择 **系统**→**管理**→**网络**。在 **网络配置** 对话框中，选择 **DNS** 选项卡。在 **主机名** 文本框中，输入 *srvB.ourglobalcompany.com* 并按 **Tab** 键。将 *192.168.0.2* 设置为主 DNS 和 DNS 搜索路径。
7. 选择 **主机** 选项卡。在 **地址** 文本框中，将 *192.168.0.3* 输入为 IP 地址。在 **主机名** 文本框中，将 *srvB.ourglobalcompany.com* 输入为主机名。在 **别名** 文本框中，将 *srvB* 输入为别名。
8. 在 **添加 / 编辑主机条目** 对话框中，点击 **确定**。保存配置并点击 **确定** 以重启网络服务。切换到 srvA 的 CLI。

**场景：**
您的公司已使用 Sendmail 为 ourglobalcompany.com 域实现了邮件服务器。现在，由于组织规模扩大，访问邮件服务器的用户数量增加，从而导致服务器性能下降。作为系统管理员，您决定将邮件服务器从 Sendmail 迁移到 Postfix。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_676_0.png)

| 操作 | 执行方法 |
| :--- | :--- |
| 1. 安装 Postfix。 | a. 在标记为 srvA 的系统上，安装 **postfix-2.3-2.1.el5_2.1386.rpm** 软件包。 <br> b. 输入 <br> `alternatives --set mta /usr/sbin/sendmail.postfix` 以将 Postfix 设置为默认 MTA。 |
| 2. 配置标记为 srvA 的服务器上的 incoming 邮件。 | a. 导航到 /etc/postfix 文件夹。 <br> b. 使用 vi 编辑器打开 main.cf 文件。 <br> c. 找到 “inet_interfaces = all” 一行并取消注释。 <br> d. 找到 “inet_interfaces = localhost” 一行并将其注释。 <br> e. 按 Esc 切换到命令模式。 <br> f. 找到 “#mydestination = $myhostname” 代码。 <br> g. 取消注释以下行 <br> #mydestination = $myhostname, <br> localhost.$mydomain, localhost, <br> $mydomain, 和 #mail.$mydomain, <br> www.$mydomain, ftp.$mydomain。 |
| 3. 配置标记为 srvA 的服务器上的邮件别名。 | a. 找到 “alias_maps = hash:/etc/aliases” 指令。 <br> b. 光标位于 `alias_maps = hash:` 之后。要将别名文件位置更改为 `/postfix/aliases`，将光标移动到 `/etc/` 末尾。输入 **postfix/** <br> c. 按 **Esc** 切换到命令模式。 <br> d. 找到 “alias_database = hash:/etc/aliases” 指令。 <br> e. 光标位于 `alias_database = hash:` 之后。要将别名文件位置更改为 `/postfix/aliases`，将光标移动到 `/etc/` 末尾。输入 **postfix/** <br> f. 按 **Esc** 切换到命令模式。 <br> g. 保存并关闭文件。 <br> h. 使用 **vi** 编辑器打开 aliases 文件。 <br> i. 输入 **hr: chris, pat,** <br> j. 输入 **root: jsmith** <br> k. 按 **Esc** 切换到命令模式。 <br> l. 保存并关闭文件。 <br> m. 输入 **postalias /etc/postfix/aliases** 以更新别名数据库文件。 <br> n. 启动 postfix 服务。 <br> o. 设置 postfix 服务在系统启动时运行。 |
| 4. 检查邮件配置。 | a. 从标记为 srvA 的系统切换到标记为 srvB 的系统。切换到 CLI。 <br> b. 在标记为 srvB 的系统上，输入 `mail hr@ourglobalcompany.com` <br> c. 在 Subject 提示处，输入 `Test mail - Postfix` <br> d. 输入 `This is a test mail for postfix`。 <br> e. 输入句号（ . ）并按 **Enter**。 <br> f. 在 cc 提示处，按 **Enter**。 <br> g. 从标记为 srvB 的系统切换到标记为 srvA 的系统。 <br> h. 在标记为 srvA 的系统上，输入 `mail -u chris` <br> i. 观察显示主题为 “Test mail - Postfix” 的邮件。 <br> j. 退出邮箱。 <br> k. 查看 pat 邮箱中的邮件消息并退出邮箱。 <br> l. 输入 `clear` 以清除终端屏幕。 |
| 5. 配置标记为 srvA 的服务器上的邮件限制。 | a. 使用 vi 编辑器打开 main.cf 文件。 <br> b. 在文件末尾，输入 <br> `smtpd_sender_restrictions = check_sender_access hash:/etc/postfix/sender_access` 以定义发送方限制。 <br> c. 在文件末尾，输入 <br> `smtpd_recipient_restrictions = check_recipient_access hash:/etc/postfix/recipient_access, reject_unauth_destination` 以定义接收方限制。 <br> d. 按 **Esc** 切换到命令模式。 <br> e. 保存并关闭文件。 <br> f. 使用 vi 编辑器打开 sender_access 文件。 <br> g. 输入 **junk@junkmail.com ERROR: 550 MAIL DISCARDED** 以在接受消息后将其丢弃。 <br> h. 按 **Esc** 切换到命令模式。 <br> i. 保存并关闭文件。 <br> j. 输入 **postmap sender_access < sender_access** 以构建相对于发送方的访问数据库。 <br> k. 使用 vi 编辑器打开 recipient_access 文件。 <br> l. 要拒绝 eric 的邮件，输入 <br> **eric@ourglobalcompany.com REJECT** <br> m. 按 **Esc** 切换到命令模式。 <br> n. 保存并关闭文件。 <br> o. 输入 **postmap recipient_access < recipient_access** 以构建相对于接收方的访问数据库。 <br> p. 重启 postfix 服务。 <br> q. 清屏。 |

