

# 默认：关闭
# 描述：SWAT 是 Samba Web 管理工具。请使用 swat \
# 来配置您的 Samba 服务器。要使用 SWAT，\
# 请使用您喜欢的 web 浏览器连接到端口 901。
service swat
{
        port               = 901
        socket_type        = stream
        wait               = no
        only_from          = 127.0.0.1
        user               = root
        server             = /usr/sbin/swat
        log_on_failure += USERID
        disable            = yes
}

修改 disable 的值，如下所示：

        disable            = no

保存该文件，并关闭您的文本编辑器。

> *顺便提一下，请注意此默认配置确保 SWAT 服务只能通过 IP 地址 127.0.0.1 和端口 901 访问。IP 地址 127.0.0.1 是一个特殊的地址，被称为环回地址，因为发送到 http://127.0.0.1 的请求会被路由到发起该请求的浏览器所在的同一台机器上的 web 服务器。因此，默认情况下，SWAT 仅可通过文件服务器本机访问 – 通过 http://127.0.0.1:901 或 http://localhost:901（正如我们在本章前面提到的）。*

-   重启 xinetd 服务。（我们必须这样做，因为 SWAT 作为 xinetd 服务运行。xinetd 服务不在本书的讨论范围内，但只需知道其目的是支持 Internet 服务，例如 SWAT 即可）。为此，首先通过选择主菜单 | 系统设置 | 服务器设置 | 服务，启动服务配置 GUI 工具：

![](img/b852150740856958b10aff9e8c9d2adc_380_0.png)

然后找到并选择名为 **xinetd** 的服务，并单击 **Restart**。您将看到一个确认重启成功的对话框；然后您可以通过单击 **Quit** 退出该工具。

## 首次使用 SWAT

现在我们可以测试 SWAT 了。在 Linux 服务器上打开浏览器并输入 URL http://localhost:901。系统将提示您输入用户名和密码 – 请使用系统的 root 用户名和密码。然后您应该能看到 SWAT 主页：

![](img/b852150740856958b10aff9e8c9d2adc_381_0.png)

请注意，此页面包含 Samba 非常全面的在线文档索引（如上图所示），您可以从中了解有关 Samba 和 SWAT 的更多信息。此页面顶部还列出了八个按钮，用于访问 SWAT 的各种实用工具：

-   HOME – SWAT 的主页，也是您启动 SWAT 接口时看到的第一个页面。
-   GLOBALS – 用于设置 /etc/samba/smb.conf 配置文件中全局变量的值
-   SHARES – 用于创建和删除 Samba 共享，并设置 Samba 参数
-   PRINTERS – 用于创建和删除 Samba 打印机共享并设置打印机参数
-   WIZARD – 与 GLOBALS 类似，这也用于设置 /etc/samba/smb.conf 中的各种值
-   STATUS – 用于查看 Samba 服务器的状态，以及启动和停止与 Samba 相关的服务
-   VIEW – 用于查看 /etc/samba/smb.conf 配置文件的内容
-   PASSWORD – 用于添加、删除、启用和禁用 Samba 用户，以及设置 Samba 用户的密码

我们的 SWAT 已启动并运行，随时可以使用；我们的下一个任务是使用它来将 Linux 机器配置为文件服务器。为此，我们将使用上面列出的一些功能。然后，当我们设置好文件服务器后，我们将以客户机的视角对其进行检查，查看不同的客户机如何使用 Samba 访问我们创建的文件服务器。

## 添加 Samba 用户

要授权系统账户访问 Samba 服务，您可以使用 SWAT 的 PASSWORD 功能。一旦使用 root 用户名和密码登录到 SWAT，点击 PASSWORD 按钮，您将看到以下屏幕：

![](img/b852150740856958b10aff9e8c9d2adc_382_0.png)

在 Server Password Management 部分中，输入系统中现有账户的名称，并提供一个密码（我们已经在上面的截图中完成了这一步，我们正在为用户 kapils 创建 Samba 访问权限）。然后点击 Add New User 按钮。这将向 Samba 的 smbpasswd 配置文件添加一个条目，以指示该用户有权访问 Samba 的服务。

> *请注意，有权访问 Samba 服务的普通账户也有权访问 SWAT。然而，只有 root 用户才能访问 SWAT 的全套实用工具；普通用户仅允许使用 HOME、STATUS、VIEW 和 PASSWORD 屏幕中包含的有限功能。*

## 创建和配置 Samba 共享

现在我们可以开始将我们的 Linux 服务器配置为文件服务器，方法是创建一个 **share**（服务器上的专用目录，可被其他用户访问）。我们可以使用 SWAT 完成所有这些操作：

1.  创建一个目录，我们将其命名为 `/share`，用于文件服务器。具有 root 权限，您可以在命令行使用以下命令完成此操作：

    ```
    # mkdir /share
    ```

2.  如果您尚未这样做，请使用 Mozilla 浏览器（或您喜欢的 web 浏览器）浏览到位于 `http://localhost:901` 的 SWAT 主页，并使用 root 用户账户登录。

3.  点击 **GLOBALS** 工具栏图标。在 **Base Options** 部分，使用 **Workgroup** 字段输入您希望服务器在客户机使用它时出现在其中的工作组名称。（如果您没有设置工作组，那么这很可能是默认值，**WORKGROUP**）。您还应该通过向 **server string** 字段输入值来命名该服务 – 它可以是任何您希望您的 Samba 客户机看到的字符串。我们将保留默认值，**Samba Server**：

    ![](img/b852150740856958b10aff9e8c9d2adc_383_0.png)

4.  点击 **Commit Changes** 将您的更改保存到配置文件。

5.  现在点击屏幕顶部的 **SHARES** 工具栏按钮。我们将通过赋予 `/share` 目录一个 **share name** 来共享它；让我们把它命名为 `linuxbox-share`。您应该首先检查此页面上的下拉列表中的条目，以确保您选择的共享名称尚未用于其他共享；然后，将共享名称输入 **Create Share** 字段：

    ![](img/b852150740856958b10aff9e8c9d2adc_384_0.png)

    现在点击 **Create Share** 按钮来创建共享。这将向您展示另一个屏幕，您可以在其中指定共享的属性。您肯定需要将 `path` 字段设置为您的共享目录的路径（在此示例中，它是 `/share`）。在下面的截图中，我们还特别设置了一些其他字段：

6.  ![](img/b852150740856958b10aff9e8c9d2adc_385_0.png)

    在这里，我们将 **read only** 字段设置为 No，使其成为可写共享；将 **browseable** 字段设置为 Yes，以允许 `/share` 目录的内容可见；并将 **available** 字段设置为 Yes，以“启用”该共享（即，使其对用户可用）。我们还添加了一个注释，以提醒我们该共享的用途。

    完成后，点击 **Commit Changes** 按钮，将这些设置提交到 Samba 配置文件。

    > 如果您愿意，您可以点击 *SHARES* 屏幕中的 **Advanced View** 按钮来设置更多设置（例如，您可以向 *valid users* 或 *invalid users* 文本框中插入一个以空格分隔的用户列表，以控制哪些用户被允许或被拒绝访问 Samba 共享）。您还可以点击 **VIEW** 按钮来查看 `/etc/samba/smb.conf` 配置文件的完整内容。

7.  重启 Samba 服务，以便配置更改可以生效。为此，点击 **STATUS** 按钮，然后点击 **Restart smbd** 按钮以重启该服务。等待页面重新加载，然后点击 **Restart nmbd** 按钮以重启该服务。

## 从 Windows NT/2000/XP 机器访问共享

现在我们在 Linux 服务器上配置了一个 Samba 共享，我们可以从网络上的其他许多机器访问它。要从 Windows 系统访问该共享，您可以使用 Windows 的网络邻居易（Network Neighborhood）浏览到它，甚至可以使用工具 | 映射网络驱动器（Tools | Map Network Drive）将其映射为网络驱动器。

## 从另一台 Linux 机器访问共享

您也可以从任何配备 SMB 功能的客户机访问您的 Linux 文件系统共享 – 例如，从另一台 Linux 机器。为此，客户机可以使用包含在 Samba 客户机软件包中的功能。实际上，您可以使用两种不同的应用程序来从配备 SMB 功能的客户机通过网络访问您的 Linux 文件共享：

-   您可以使用 smcclient 命令，它提供了一个类似 FTP 的接口，执行类似 FTP 的功能
-   如果您的客户机是 Linux 机器，您可以使用 smbmount 命令将远程 smb 共享挂载为本地目录

要通过远程机器访问 smb 共享，您需要知道远程 samba 服务器机器上 samba 用户账户的用户名和密码（如我们之前创建的 kapils 账户）。让我们看看如何使用此账户，通过 smcclient 或 smbmount 来访问远程 Samba 共享。

## smcclient 实用工具

如果您使用客户机 Linux 机器访问您的 Samba 共享，您可以使用 smcclient 实用工具。为了这里创建的共享，我们在命令行运行以下命令：

```
$ smcclient //linuxserver/linuxbox-share -U kapils
added interface ip=192.168.0.114 bcast=192.168.0.255 nmask=255.255.255.0
Password:
Domain[WORKGROUP] OS=[Unix] Server=[Samba2.2.7a]
smb: / >
```

在 smcclient 命令中，我们需要指定两件事：

-   文件服务器的名称和共享的名称
-   我们用来访问共享的用户名称（即，我们之前使用 SWAT 设施的 PASSWORD 屏幕创建的用户）

请注意，系统会提示您输入密码。当与 samba 服务器的密码认证成功时，您将获得一个 smcclient 会话，其外观与 FTP 会话非常相似。如上所示，会话的提示符为 smb: />。现在您可以使用所有可用的命令来操作远程文件系统文件：

