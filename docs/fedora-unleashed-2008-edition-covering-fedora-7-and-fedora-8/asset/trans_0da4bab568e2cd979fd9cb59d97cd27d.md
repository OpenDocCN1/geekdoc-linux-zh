

![](img/34e72348d53ca54c2a1d9c871316691b_452_0.png)

图 19.5 配置 Samba，以允许来自您的局域网中特定主机或子网的访问。

![](img/34e72348d53ca54c2a1d9c871316691b_452_1.png)

图 19.6 在 SWAT 密码页面中输入 Samba 用户名和密码。

完成后，单击“添加新用户”按钮。然后，SWAT 会创建用户名和密码，并显示“已添加用户 *username*”（其中 *username* 是您输入的名称）。如果 Samba (smb) 服务器正在运行，新的 Samba 用户现在应该能够从任何允许的主机访问主目录。

例如，如果你在名为 *rawhide* 的主机上设置了 Samba，并且该主机的用户名是 andrew，那么该用户可以从任何远程主机（如果 GLOBALS 设置允许的话）访问 rawhide 上的主目录，也许可以像这样使用 `smbclient` 命令：

```
$ smbclient //rawhide/andrew -U andrew
Password:
Domain=[RAWHIDE] OS=[Unix] Server=[Samba 3.0.26a-6.fc8]
smb: \> pwd
Current directory is \\rawhide\andrew\
smb: \> quit
```

单击 SWAT 屏幕顶部工具栏中的“状态”图标，以查看 Samba 的状态，或者启动、停止或重新启动服务器。您可以使用生成的网页上的各种按钮来控制服务器并查看定期或连续的状态更新。

您也可以使用 SWAT 来共享 Linux 目录。首先，单击主 Samba 页面顶部工具栏中的“共享”图标（参见图 19.4）。在“创建共享”字段中输入共享名称，然后单击“创建共享”按钮。SWAT 共享页面会在对话框中显示详细的配置信息，如图 19.7 所示，从而提供对新 Samba 共享的详细配置访问。

![](img/34e72348d53ca54c2a1d9c871316691b_453_0.png)

图 19.7 使用 SWAT 共享页面来设置共享 Linux 文件系统的一部分。

在“基本选项”下的“路径”字段中输入您想要共享的目录名称（例如 /opt/share）。在“安全选项”下的“只读”字段中选择“否”或“是”，以允许或拒绝读写访问。选择“是”在“允许来宾”选项中，以允许其他用户访问，并在“允许主机”字段中指定主机名、IP 地址或子网以允许访问。完成后，单击“提交更改”按钮。然后，远程用户可以访问共享卷。这就是运行 Samba 的 Linux 服务器如何在混合计算环境中轻松模拟共享卷的方式！

或者，使用 `system-config-samba` 客户端（从命令行或系统设置菜单中的“服务器设置 > Samba 服务器”菜单项）。图 19.8 显示了名为 `/opt/share` 的共享目录的属性。使用“添加”按钮创建新的共享，并使用“属性”按钮（均位于主屏幕上）编辑共享的访问选项。使用“首选项”菜单编辑您的 Samba 服务器的一般设置，或创建和管理 Samba 用户。

![](img/34e72348d53ca54c2a1d9c871316691b_454_0.png)

图 19.8 通过编辑共享默认设置来配置 Samba 共享。

## 通过 `/etc/samba/smb.conf` 手动配置 Samba

`/etc/samba/smb.conf` 文件被分为几个部分。每个部分都是对共享资源（share）的描述，并且应该适当地命名。三个特殊部分如下：

- **[global]**—建立全局配置设置（在 `smb.conf` man 页面和 Samba 文档中有详细说明，这些文档位于 `/usr/share/doc/samba/docs` 目录下）
- **[homes]**—共享用户的主目录，并指定目录路径和权限
- **[printers]**—通过定义共享打印机和打印机访问来处理打印

您 `/etc/samba/smb.conf` 配置文件中的每个部分都应该以被共享的资源命名。例如，如果资源 `/usr/local/programs` 正在被共享，您可以将该部分命名为 `[programs]`。当 Windows 看到该共享时，它会被称为您为该部分命名的名称（在本例中为 programs）。设置此共享最简单、最快的方法是来自 `smb.conf` 的以下示例：

```
[programs]
path = /usr/local/programs
writable = true
```

这段配置将 /usr/local/programs 目录与任何请求它的有效用户共享，并使该目录可写。这是最基本的共享，因为它对该目录没有限制。

以下是您可以在部分中设置的一些参数：

- 要求用户在访问共享目录之前输入密码
- 限制允许访问共享目录的主机
- 更改用户在该目录上允许的权限
- 限制该目录可访问的时间段

可能性几乎是无穷无尽的。在各个部分中设置的任何参数都会覆盖 [global] 部分中设置的参数。以下部分在 [programs] 部分中添加了一些限制：

```
[programs]
path = /usr/local/programs
writable = true
valid users = ahudson
browsable = yes
create mode = 0700
```

`valid users` 条目将 `userid` 限制为仅 `ahudson`。由于 `browsable = yes` 条目，所有其他用户都可以浏览目录，但只有 `ahudson` 可以写入该目录。`ahudson` 在该目录中创建的任何文件都赋予 `ahudson` 完全权限，但其他人将无法访问这些文件。这与使用 `chmod` 命令设置权限完全相同。同样，有很多选项，因此在开发部分时，您可以尽可能富有创造性。

## 使用 [global] 部分设置全局 Samba 行为

[global] 部分建立了 Samba 的所有配置设置。如果某个参数未在另一个部分中明确设置，Samba 将使用 [global] 部分中的默认设置。[global] 部分还设置了 Samba 的一般安全配置。[global] 部分是唯一不需要括号内名称的部分。

Samba 假设第一个未标记为 [global] 的括号部分之前的任何内容都是全局配置的一部分。（在 `/etc/samba/smb.conf` 中使用括号标题可以使您的配置文件更具可读性。）以下部分讨论了共享目录和打印机的常见 Samba 设置。然后您将会看到如何测试您的 Samba 配置。

## 使用 [homes] 部分共享主目录

[homes] 部分共享 Fedora 用户的主目录。当用户的 Windows 计算机连接到持有主目录的 Linux 服务器时，主目录会自动共享。使用默认配置的一个问题是，用户会看到所有配置文件（如 .profile 和其他文件名以点开头的文件），而他们在通过 Linux 登录时通常不会看到这些文件。避免这种情况的一个快速方法是在 [homes] 部分中包含一个路径选项。要使用此解决方案，每个需要共享其主目录的 Samba 共享的用户都需要一个单独的“主目录”作为其 Windows 主目录。

例如，这个伪主目录可以是您在 Fedora 系统上每个用户主目录中名为 share 的目录。在使用 SWAT 时，可以通过在指定默认 homes 共享的路径时使用 *\u* 选项来指定路径选项。完整的路径设置将如下所示：

```
/home/\u/share
```

此设置指定每个用户目录下名为 share 的目录是共享的 Samba 目录。提供单独“主目录”的手动 smb.conf 设置如下所示：

```
[homes]
comment = Home Directories
path = /home/\u/share
valid users = %S
read only = No
create mask = 0664
directory mask = 0775
browsable = No
```

如果您有一个默认的 [homes] 部分，该共享会以用户的名称显示在用户的“网上邻居”中。当用户连接时，Samba 会扫描 smb.conf 中的现有部分，查找用户主目录的具体实例。如果没有，Samba 会在 /etc/passwd 中查找用户名。如果提供了正确的用户名和密码，则 /etc/passwd 中列出的主目录会在用户的主目录下共享出来。通常 [homes] 部分看起来像这样（`browsable = no` 条目防止其他用户能够浏览您的主目录，使用它是良好的安全实践）：

```
[homes]
browsable = no
writable = yes
```

