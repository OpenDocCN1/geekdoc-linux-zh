
`http_access deny restricted_site`

## 主题 D

## 配置电子邮件服务

你已为用户设置了代理服务器，现在需要通过定义电子邮件进程来提供客户端和服务器电子邮件服务。在本主题中，你将配置电子邮件服务。

不久之前，组织仅使用内部邮件室和邮政服务进行业务通信。如今，我们通过电子邮件和即时消息进行电子通信。理解邮件客户端的运行机制对于实施电子邮件服务至关重要。

## 邮件协议

**定义：**

邮件协议是一组规则，用于启用邮件服务器分发电子邮件消息。使用邮件协议，电子邮件消息可以存储在服务器上，或在阅读时传输到客户端计算机。邮件协议允许用户在服务器上创建和管理文件夹，搜索消息，或删除消息。`POP`、`IMAP` 和 `SMTP` 是最常用的邮件协议。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_666_0.png)

图 13-21：电子邮件消息使用 `POP`、`IMAP` 和 `SMTP` 协议进行分发。

## 简单邮件传输协议

简单邮件传输协议（`SMTP`）是一种协议，定义了一组规则，以启用向服务器发送电子邮件消息的程序与从客户端接收电子邮件消息的程序之间的交互。邮件传输代理（`MTA`）或邮件用户代理（`MUA`）充当 `SMTP` 客户端。`SMTP` 服务器始终监听 `25` 端口以获取客户端响应。`SMTP` 使用 `TCP` 传输消息，使用 `IP` 进行路由。它包含一系列状态代码，用于设置服务器与客户端之间通信的特定条件。它还包含一组命令，用于服务器与客户端之间的通信。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_2.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_3.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_4.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_5.png)

图 13-22：使用 `SMTP` 的客户端之间通信。

除了文本消息，使用扩展 `SMTP`（`ESMTP`）还可以通过电子邮件传输图形和附件。扩展 `HELLO`（`EHLO`）命令用于 `ESMTP` 客户端与服务器通信，服务器会以三种状态代码之一进行响应：成功、失败或错误。

## 邮件队列化（Spooling）

队列化（Spooling）是处理电子邮件消息投递延迟的方法。如果存在电子邮件投递延迟，源计算机上的 `SMTP` 会对消息进行队列化处理。如果没有延迟，源计算机上的 `SMTP` 会通过 `TCP` 连接将电子邮件消息发送到目标计算机。目标计算机上的 `SMTP` 接收电子邮件消息并将其放入用户的邮箱中。当目标计算机上的用户向源计算机上的用户发送回复时，也会发生相反的过程。

## POP3

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_6.png)

`邮局协议版本 3（POP3）` 用于通过 `TCP` 连接在 `110` 端口上检索电子邮件消息。`POP` 客户端连接到服务器并检索所有消息。然后，它将它们作为新消息存储在客户端 `PC` 上，从服务器删除它们，并从服务器断开连接。它支持 `MIME` 格式的电子邮件消息。通常，`POP3` 支持以明文格式传输消息和密码。它还通过 `TCP` 在 `995` 端口上使用 `SSL` 协议对消息进行加密，从而提供消息身份验证。

## IMAP

![](img/477ccb2f05b6ba1b2d563ea74f18c197_667_7.png)

`互联网消息访问协议（IMAP）` 用于通过 `TCP` 连接在 `143` 端口上检索电子邮件消息。客户端从服务器检索所有消息，服务器保留这些消息，直到用户删除它们。虽然它以明文格式传输消息和密码，但它支持通过 `TCP` 在 `993` 端口上使用 `SSL` 对消息进行加密。它支持 `MIME` 格式的电子邮件消息。

## 邮件队列

**定义：**

`邮件队列` 是计算机需要处理的电子邮件消息的等待区域。邮件队列的组织方式是，第一个添加到队列的项目也是第一个从队列发出的项目。

**示例：**

```
root@localhost:~#

File Edit View Terminal Tabs Help

[root@localhost :~]# mailq

--- Queue ID---- ---Size--- ---Arrival Time--- - Sender/Recipient-----

DE67933057S 2633 Thu Jul 30 20:05:39 MAILER-DAEMON

 (connect to srvB.orgglobalcompany.com[192.168.0.2]: Connection refused)

 root@srvB.orgglobalcompany.com

C14AC330566 2584 Thu Jul 30 19:52:03 MAILER-DAEMON

 (connect to srvB.orgglobalcompany.com[192.168.0.2]: Connection refused)

 root@srvB.orgglobalcompany.com

B9F2033056B 2567 Thu Jul 30 19:52:03 MAILER-DAEMON

 (connect to srvB.orgglobalcompany.com[192.168.0.2]: Connection refused)

 root@srvB.orgglobalcompany.com

-- 8 Kbytes in 3 Requests.

[root@localhost :~]#
```
