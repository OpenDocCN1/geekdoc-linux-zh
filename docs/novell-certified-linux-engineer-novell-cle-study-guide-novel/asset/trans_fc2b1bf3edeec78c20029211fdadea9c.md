

也创建在树中。除了前面讨论的智能体对象外，还会添加以下对象：

- **Internet Services（互联网服务）**——Internet Services 对象是一个容器对象。它始终安装在 eDirectory 树的根目录中，且每棵树只能有一个实例。Internet Services 容器只能包含 NetMail 对象。Internet Services 容器如图 10.12 所示。

**图 10.12**  
Internet Services 容器。

![](img/c7771e8540507f2b00c088c7a411b57b_463_0.png)

- **Messaging Server（消息服务器）**——Messaging Server 对象代表你的 NetMail 服务器。Messaging Server 对象包含服务器配置使用的所有 NetMail 智能体对象，如图 10.13 所示。

**图 10.13**  
Messaging Server 对象。

![](img/c7771e8540507f2b00c088c7a411b57b_463_1.png)

除了容纳智能体对象外，Messaging Server 对象还包含在服务器上运行的 NetMail 服务的配置参数。这些参数如图 10.14 所示。

> **注意** 暂时不用担心如何所有这些配置参数。我们将在本章稍后讨论配置任务。

![](img/c7771e8540507f2b00c088c7a411b57b_464_0.png)

图 10.14  
Messaging Server 对象属性。

- **Parent Objects（父对象）**——虽然听起来像复数，但 eDirectory 中的 Parent Objects 对象实际上是一个单独的容器对象。当你想将 NetMail 系统拆分为较小的单元时使用它，这样你就可以配置多组具有不同设置的智能体。每个组表现得好像它是一个独立的电子邮件系统。Parent Objects 容器如图 10.15 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_464_1.png)

图 10.15  
Parent Objects 容器。

对于 CLE 考试，不必过于担心此功能。你只需要将 NetMail 管理为单个消息系统即可。

- **Templates（模板）**——eDirectory 树中的 Templates 对象是一个容器对象，包含 WebAccess 和 WebMail 模板（前面已讨论过），用于为用户提供基于浏览器的 NetMail 邮箱界面。Templates 容器如图 10.16 所示。

默认情况下，你的 Modular Web Agent 被配置为使用 WebAccess 模板，如图 10.7 中所示。在我看来，这是一个很好的选择。正如你将在本章的实验练习中看到的那样，WebAccess 模板提供了设计良好、直观的用户界面。

WebMail 模板运行良好，但坦白说，它非常朴素。我甚至听到有些学生称之为“丑陋”。我更喜欢温和的术语，如“极简主义”。

![](img/c7771e8540507f2b00c088c7a411b57b_465_0.png)

当 NetMail 启动时加载你的 Modular Web Agent 时，它将指定的模板加载到 RAM 中。

- **Mailing Lists（邮件列表）**——Mailing Lists 对象是位于 Internet Services 容器内的容器对象。如前所述，你的 NetMail 服务器使用 List Server Agent 可以充当列表服务器。当消息发送到列表服务器时，它会自动转发到服务器配置的邮件列表中包含的所有电子邮件地址。

在 Mailing Lists 容器中，你可以创建两种不同类型的邮件列表对象：Mailing List 和 NDS Mailing List。Mailing List 对象的功能类似于传统列表服务器。用户手动订阅列表。当他们这样做时，将在 Mailing List 对象内为该电子邮件地址创建一个 List User 对象。发送到列表的消息会发送给每个 List User 对象。

NDS Mailing List 对象的功能不同。NDS Mailing Lists 由 eDirectory 树中的容器、组、用户、组织角色或别名对象组成。当消息发送到列表时，它会传递给 NDS Mailing List 对象中配置的每个用户。

这可能非常强大，特别是如果你使用容器或组对象，因为这些对象是动态的。如果你从这些对象中添加或删除用户，它们会自动从列表中添加或删除。无需手动更新列表。

除了这些新的对象类之外，NetMail 还扩展了模式，为几个现有的对象类添加了新属性，包括 organization（组织）、organizational unit（组织单元）、user（用户）和 server（服务器）对象。

> **提示** 这些添加的属性在 iManager 中不可见。你只能在 WebAdmin 中查看和修改它们。WebAdmin 是一个基于 web 的管理工具，用于配置你的 NetMail 实现。我们将在本章稍后介绍 WebAdmin。

Organization 和 organizational unit 对象添加了 Domain 和 Message Store 属性，如图 10.17 所示。

Domain 属性允许你为该容器中的用户设置自定义电子邮件域。Message Store 属性允许你为该容器中的用户配置自定义消息存储目录。此参数不会更改 NMAP Agent 使用的消息队列或 scms 目录。消息队列和 scms 目录将在本章稍后讨论（见表 10.1）。

![](img/c7771e8540507f2b00c088c7a411b57b_466_0.png)

**图 10.17**  
容器对象 NetMail 属性。

User 对象添加了许多新属性。部分 NetMail 用户属性如图 10.18 所示。这些属性包括：

![](img/c7771e8540507f2b00c088c7a411b57b_466_1.png)

**图 10.18**  
User 对象 NetMail 属性。

- **User Status（用户状态）**——允许你启用或禁用指定用户作为 NetMail 用户。
- **Timeout（超时）**——指定在用户注销 NetMail web 界面之前的非活动时间（以分钟为单位）。
- **Privacy（隐私）**——指定通过 Address Book Agent 显示给终端用户的信息。当此属性设置为 **None（无）** 时，Address Book Agent 会显示用户的电子邮件地址和全名。当设置为 **Limited（有限）** 时，仅显示用户的电子邮件地址。当设置为 **Unlisted（未列出）** 时，不显示任何信息。
- **Reply To Address（回复地址）**——指定用户的回复地址。此地址显示在 outgoing（发件）消息的 From 字段中。
- **Quota（配额）**——启用时，此参数指定指定用户的邮箱可以消耗多少磁盘空间。
- **Forwarding（转发）**——启用时，此参数将接收的消息转发到指定的电子邮件地址。
- **Auto Reply（自动回复）**——启用时，此参数允许用户在接收到消息时向发件人发送自动回复。
- **Time Zone（时区）**——指定用户所在的时区。
- **Template（模板）**——允许用户指定他或她想使用的 NetMail web 界面。

Server 对象添加了 Novell NetMail Server 属性，如图 10.19 所示。此属性不可编辑。

![](img/c7771e8540507f2b00c088c7a411b57b_467_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_467_1.png)

至此，我们需要讨论安装 NetMail 时对服务器文件系统所做的更改。

## NetMail 在文件系统中的目录

在安装过程中，NetMail 被配置为使用服务器文件系统中表 10.1 所示的目录。

### NetMail 目录

**表 10.1**

| 目录 | 描述 |
| :--- | :--- |
| /opt/novell/netmail/bin | 此目录包含 NetMail 二进制文件。NetMail 二进制文件 `ims` 位于此目录中。前面讨论的每个 NetMail 智能体的二进制文件也驻留在此目录中。 |
| /var/opt/novell/netmail/users | 此目录是 NetMail 的默认消息存储。所有 NetMail 用户的邮箱和相关消息都存储在此目录结构中。 |
| /var/opt/novell/netmail/users/user/INBOX.box | 此文件包含指定 NetMail 用户的所有 incoming（收件）电子邮件消息。电子邮件附件包含在此文件中。 |
| /var/opt/novell/netmail/users/user/INBOX.idx | 此文件包含指定 NetMail 用户收件箱中所有消息的索引。 |

