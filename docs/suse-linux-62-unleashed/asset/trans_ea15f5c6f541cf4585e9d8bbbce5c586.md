
# SMTP 与协议
第 9 章

假设你有一份纸质备忘录想要发送给 Gonzo 公司的同事 Mary 和 Bill，以及 Whizer 公司的 Ted 和 Ben。你将备忘录的副本交给了你信赖的邮差 Alphonse，他记录了多个收件者。由于他是一个想为你的公司节省 66 分钱的聪明人，Alphonse 制作了两份备忘录的副本，并将它们分别放入写有相应公司地址的信封中，而不是给每个收件者发送一个副本。在 Gonzo 信封的封面上，他写着“Mary and Bill”，在 Whizer 信封的封面上，写着“Ted and Ben”。当 Alphonse 在 Gonzo 和 Whizer 的同事收到信封时，他们复制了备忘录，并将其发送给 Mary、Bill、Ted 和 Ben，而没有检查备忘录本身的地址。对于 Gonzo 和 Whizer 的邮差来说，备忘录本身的地址可能是写给教皇的。他们只关心信封上的地址。

SMTP 客户端和服务器的工作方式与 joe@gon.gov 向其同事 betty@zippy.gov 和 fred@whizer.com 发送邮件相同。邮件头中的收件者列表如下：

To: betty@zippy.gov, fred@whizer.com

gonzo.gov 的 SMTP 客户端连接到 whizer.com 邮件服务器来交付 Fred 的副本。当它准备列出收件者（信封地址）时，它应该做什么？如果它获取了前面的 To: 行列出的两个收件者（头地址），Betty 将收到两封信，因为 whizer.com 邮件服务器会将一个副本转发到 zippy.gov。如果 gonzo.gov 的 SMTP 客户端连接到 zippy.gov 并将 Betty 和 Fred 列为收件者，也会发生同样的问题。zippy.gov 邮件服务器将转发第二封 Fred 的信。

解决方案与 Alphonse 和其他邮差使用的相同。Gonzo.gov 的 SMTP 客户端将邮件放入一个仅包含每个主机收件者名称的信封中。收件者列表仍然在邮件头中，但它们在信封内部，gonzo.gov 和 whizer.com 的 SMTP 服务器不会查看它们。在这个示例中，给 whizer.com 邮件服务器的信封仅列出 fred，而给 zippy.gov 的信封仅列出 Betty。

别名（Aliases）说明了信封地址不同的另一个原因。假设你向别名 homeboys 发送邮件，它包含了 phonse、joe、betty 和 george 的名字。在你的邮件中，你写道 To: homeboys。然而，sendmail 会展开别名并构建一个包含所有收件者的信封。取决于这些名称在其他主机上是否也是别名，原始消息可能被放入多达四个不同的信封并递送到四个不同的主机。在每种情况下，信封仅包含收件者的名称，但原始消息包含了别名（扩展为 homeboys@your.host，这样回复才能正常工作）。

![](img/cbac72550c712a2216e94d1a310_0.png)

# 网络与互联网服务
第二部分

第一个示例显示了信封地址与头地址不同的另一种方式。使用 sendmail，你可以在命令行指定收件者。假设你有一个名为 letter 的文件，如下：

```
$ cat letter
To: null recipient <>
Subject: header and envelope addresses
```

你使用以下命令发送此邮件，将你的登录名替换为 loginuser：

```
$ /usr/bin/sendmail loginuser <
```

由于你的地址在信封上，即使你的登录名没有出现在邮件头，你会收到邮件。除非另有说明（使用 -t 标志），否则 sendmail 将构建你在命令行指定的地址。

# sendmail 的功能

为了更好地理解 sendmail，你需要了解它的功能以及它们如何适应 MUA、 MTA、路由器和客户端的体系。sendmail 可以作为路由器、客户端或服务器工作。然而，它的主要工作是路由。

# sendmail 作为路由器

sendmail 上是一个路由器，这意味着它接收邮件、检查地址并决定发送的最佳方式。sendmail 是如何完成此任务的？它从自己的文件中确定它所需的某些信息，例如配置文件。配置文件通常很晦涩，但用户可以对其进行修改。

# 别名文件

别名可以用于创建邮件列表。在上一节的示例中，别名 postmaster 实际上是本地邮差的邮件列表。对于大型或频繁更改的列表，可以使用 :include: 别名形式，引导 sendmail 从文件中读取列表成员。如果别名文件包含以下行

```
homeboys: :include:/home/alphonse/homeboys.aliases
```
