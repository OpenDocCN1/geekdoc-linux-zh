
## 图 8.33

为用户对象启用 LUM 和 Samba。

9. 在**为此用户输入主组**字段中，浏览并选择您的 LUM 组。

10. 确保**同时将此用户对象转换为 Samba 用户对象**复选框已选中。

11. 在**输入所需的 Samba 密码**字段中，为该用户输入一个 Samba 密码。您需要理解 NNLS Samba 服务不使用用户对象的 eDirectory 密码。当用户对象启用 Samba 时，将添加一个属性来存储其 Samba 密码。默认情况下，此字段会自动填充 eDirectory 密码。Novell 建议 Samba 密码与 eDirectory 密码相同，以避免混淆。

12. 点击**确定**。

13. 当提示该用户已启用 LUM 时，点击**确定**。

对象创建后，用户将有两个额外的属性页：Linux 属性页和 Samba 属性页。如图 8.34 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_383_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_383_1.png)

Samba 属性页允许您更改用户的 Samba 密码，如图 8.35 所示。

在用户可以使用 Samba 之前，他或她需要在 Linux 服务器的文件系统中创建一个主目录。最简单的方法是让用户登录。回想一下第 6 章的内容，当 LUM 用户向系统进行身份验证时，会创建一个主目录并将其与 eDirectory 树中的用户对象关联。

在图 8.36 中，Jjackson eDirectory 用户使用 `ssh` 工具登录到 Linux 服务器。在身份验证期间，请注意 Jjackson 用户对象的主目录已自动在 `/home` 目录中创建。

![](img/c7771e8540507f2b00c088c7a411b57b_384_0.png)

**图 8.35** Samba 属性属性页。

![](img/c7771e8540507f2b00c088c7a411b57b_384_1.png)

**图 8.36** 自动创建主目录。

如果用户在登录后，您查看 iManager 中用户对象的 Linux 属性页，您将看到主目录属性已填充。如图 8.37 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_384_2.png)

**图 8.37** Linux 属性页中的主目录属性。

您可能在问：“如果我在 eDirectory 树中已经有想将其设为 Samba 用户的用户，我是否必须手动重新创建每个用户以启用它们的 Samba？” 请放心！与 LUM 一样，NNLS 包含 iManager 任务，位于 Linux 管理角色下，允许您将现有用户转换为 Samba 用户。这些角色如图 8.38 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_385_0.png)

**图 8.38**

将现有用户转换为 Samba 用户的任务。

如果您有当前不是 LUM 用户的用户，您可以使用 iManager 中的**将 eDirectory 用户转换为 LUM 用户**任务，同时将一个用户对象转换为 LUM 用户和 Samba 用户。

如果您有当前是 LUM 用户但不是 Samba 用户的用户，您可以使用**将 LUM 用户转换为 Samba 用户**任务。就本书而言，我们将重点介绍前一种选项，即将用户同时转换为 LUM 和 Samba 用户。

要将现有的 eDirectory 用户转换为 LUM 和 Samba 用户，请完成以下步骤：

1. 打开 web 浏览器并导航至 `https://*your_server_IP_address*/nps/iManager.html`。

2. 使用第 6 章中讨论的步骤，在您的树中配置一个或多个包含 LUM/Samba 用户的组。

3. 使用第 5 章和第 6 章中介绍的步骤，将将要转换为 LUM/Samba 用户的用户添加到组中。

4. 在**Linux 用户管理**下，选择**将 eDirectory 用户转换为 LUM 用户**。

5. 在**选择用户**字段中，浏览并选择要转换的用户。

6. 单击**确定**。将显示图 8.39 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_386_0.png)

#### 图 8.39

将现有用户转换为 Samba 用户。

7. 在**输入此用户的主组**字段中，浏览并选择该用户所属的启用了 LUM 的组。

8. 确保**同时将此用户对象转换为 Samba 用户对象**复选框已被选中。

9. 在**输入所需的 Samba 密码**字段中，输入该用户的 Samba 密码。如前所述，建议您使用用户的 eDirectory 密码作为 Samba 密码。否则，用户将需要记住两个密码——一个用于身份验证以访问树，另一个用于访问 Samba 资源。

10. 单击**确定**。

11. 当提示该过程已成功时，单击**确定**。如果还有更多用户需要转换，您可以选择**重复任务**以对其余用户对象重复此过程。

NNLS 还包含 `smbpsswd` 工具的一个版本，如果您实施过非 NNLS 版本的 Samba，可能会熟悉该工具。您可以使用此工具来设置用户对象的 Samba 密码。但是，它不会将用户转换为 LUM/Samba 用户，也不会配置 LUM 属性。Novell 建议您使用 iManager 来配置 Samba 用户。

既然您的用户对象已转换为 Samba 用户，接下来我们需要做的是配置您的 Samba 服务器。

### 配置 Samba 配置文件

与大多数组件一样，NNLS Samba 服务器通过文本文件进行配置。在这种情况下，该文件是位于 `/etc/opt/novell11/samba` 目录中的 `smb.conf` 文件。该文件如图 8.40 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_387_0.png)

```
================ Global Settings ================
[global]
##
## Basic Server Settings
##

        # workgroup = workgroup
        workgroup = workgroup

        # server string is the equivalent of the NT Description field
        server string = Samba Server

        # This option is important for security. It allows you to restrict
        # connections to machines which are on your local network. The
        # following example restricts access to two C class networks and
        # the "loopback" interface. For more examples of the syntax see
        # the smb.conf man page.
        ; hosts allow = 192.168.1, 192.168.2,0/24 192.168.3,0/255.255.255.0 127.0.0.1

        # Uncomment this if you want a guest account, you must add this to /etc/passwd
```

如果您熟悉非 NNLS 版本的 Samba，您会知道它是一个非常强大的产品，拥有许多高级配置选项。整本书都专门介绍过此产品。然而，就 CLE 而言，您只需要知道如何进行基本配置。从本质上说，您只需将其启动并运行起来。

因此，我们将在本书中实施基本配置。表 8.1 列出了 `smb.conf` 文件中您应该熟悉的必需元素。

### 表 8.1

`smb.conf` 指令

| 指令 | 描述 | 示例值 |
| :--- | :--- | :--- |
| `ldaps admin dn =` | 此指令指定 Samba 应使用哪个 eDirectory 用户通过服务器上的 LDAP 服务进行身份验证。此 eDirectory 用户的密码存储在 `/etc/opt/novell/samba/` 目录中的 `secrets.tdb` 文件中。如果您更改此用户的 eDirectory 密码，您必须使用前面提到的 `smbpasswd` 工具来使用新密码更新 `secrets.tdb` 文件。 | `cn=admin,ou=IF,o=CLE` |
| `ldap ssl =` | 指定是否加密与 LDAP 服务器的通信。 | **on**（默认）<br>**off** |
