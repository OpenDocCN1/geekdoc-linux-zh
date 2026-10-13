
# 身份认证

用户认证可以通过 PAM 或 SQL 实现。对于 PAM，默认检查用户是否在 `/etc/shells` 中列出了有效 shell。如果用户没有有效 shell，则连接将被拒绝。你可以使用 `RequireValid` 指令和 `off` 选项关闭此检查。远程用户随后可以使用任何类型的 shell 登录。

匿名配置中一个重要的指令是 `RequireValidShell`。默认情况下，FTP 守护进程首先检查远程用户是否尝试使用有效 shell（例如 BASH shell 或 C shell）登录。FTP 守护进程从 `/etc/shells` 获取有效 shell 列表。如果远程用户没有有效 shell，连接将被拒绝。你可以使用 `RequireValid` 指令和 `off` 选项关闭此检查。远程用户随后可以使用任何类型的 shell 登录。

# 匿名访问

下面的示例显示了一个标准的匿名配置。`Anonymous` 指令指定 `/var/ftp` 为匿名主目录。`User` 指令指定 FTP 守护进程运行的用户，`Group` 指明其所属组。在两种情况下，它们在大多数系统中都会被使用。`*` 匹配字符随后定义了一个适用于 `/var/ftp` 中所有目录和文件的 `Directory` 块。

`Directory` 指令内部有一个 `Limit` 指令，你用它对目录进行控制。该指令接受多个参数，包括 `READ` 用于读取访问和 `WRITE` 用于写入访问。在本示例中，`Limit` 指令对用户的写入能力实施限制。在 `Limit` 指令内部，`DenyAll` 指令拒绝权限，防止用户创建或删除文件，并实际上只赋予他们读取权限。第二个 `Directory` 指令为 `incoming` 目录创建了此规则的例外，该目录通常在 FTP 站点上设置以允许用户上传文件。为此，第一个 `Limit` 指令阻止了用户的 `READ` 和 `WRITE` 访问。`AllowAll` 指令阻止了用户删除或读取文件，而第二个 `Limit` 指令通过 `STOR` 允许用户上传文件。

然而，你也可以创建其他用户及其主目录，这些目录也可以具有相同限制的匿名 FTP 账户。此类账户被称为访客账户。远程用户需要知道用户名，通常还需要知道密码。一旦连接，他们仅对账户文件具有读取权限；文件系统的其余部分对他们是隐藏的。实际上，你是在相同位置创建了一个访问限制更严格的匿名 FTP 站点。

要创建一个访客账户，首先要为其创建一个用户和主目录。然后，你在 `proftpd.conf` 文件中为该账户创建一个 `Anonymous` 块。`Anonymous` 指令包含了你创建的访客用户的主目录。你可以使用 `-` 指定该路径和目录名（目录名通常与用户名相同）。在 `Anonymous` 块中，你使用 `User` 和 `Group` 指令来指定账户的用户名和组名。如果你希望用户提供密码，请将 `AnonRequirePassword` 指令设置为 `on`。`UserAlias` 指令用于为用户名定义别名。远程用户可以使用别名或原始用户名登录。然后，你输入剩余用于控制账户主目录中文件和目录访问的指令。这里列出了显示初始指令的示例。`User` 指令指定用户为 `myproject`。主目录为 `-myproject`，它通常解析为 `/var/myproject`。`UserAlias` 让用户可以使用 `myproject` 或 `mysydert` 的名称登录。

你也可以同样容易创建一个不需要密码的账户，让用户输入他们的电子邮件地址。下面的示例配置了一个名为 `mypics` 的匿名用户。不需要密码，也不需要有效的 shell。远程用户仍然需要知道用户名；在这种情况下为 `mypics`。

```
<Anonymous /var/mypics>

AnonRequirePassword off

User mypics

Group nobody

RequireValidShell off

<Directory *>
```

接下来的示例提供了一种更通用的访客登录方式。用户名为 `guest`，主目录位于 `-guest`。远程用户需要知道访客账户的密码。第一个 `Limit` 指令允许所有用户登录。第二个 `Limit` 指令允许来自特定网络（由网络 IP 地址所示）的用户具有写入权限，并拒绝其他人的写入权限。

# 436 Red Hat Linux 8: 完整参考

```
<Anonymous ~guest>

User                guest

Group              nobody

AnonRequirePassword  on

<Limit LOGIN>

AllowAll

</Limit>

# 拒绝来自信任主机外的所有用户的写入权限。

<Limit WRITE>

Order               allow, deny

Allow               from 10.0.0.

Deny                from all

</Limit>

</Anonymous>
```

# 虚拟 FTP 服务器

ProFTPD 守护进程可以同时管理多个 FTP 站点。通过使用 `proftpd.conf` 文件中的 `VirtualHost` 功能，你可以创建一组独立的指令来配置单独的 FTP 服务器。`VirtualHost` 指令通常用于配置作为 FTP 站点的虚拟服务器。如果你配置系统以支持多个 IP 地址，你可以使用额外的 IP 地址来设置虚拟 FTP 服务器，从而在同一系统上提供另一个 FTP 站点。此新增的服务器将使用额外的 IP 地址作为自己的地址。远程用户可以通过该 IP 地址而不是系统的主 IP 地址进行访问。由于此类 FTP 服务器不是在独立的机器上独立运行，而是在同一台机器上，因此它被称为虚拟 FTP 服务器或虚拟主机。此功能允许你在单台机器上运行看似多个不同的 FTP 服务器。当远程用户使用虚拟 FTP 服务器的 IP 地址来访问它时，ProFTPD 守护进程会检测到并作为该站点的 FTP 服务运行。ProFTPD 单台机器上同时处理大量的虚拟 FTP 站点。

鉴于其配置能力，你还可以根据特定规则定制虚拟 FTP 站点，例如访客站点、针对特定组的匿名站点或针对特定用户的匿名站点。

你通过在 `proftpd.conf` 文件中输入 `<VirtualHost>` 指令来配置虚拟 FTP 服务器。此类条目以 `VirtualHost` 指令和 IP 地址开始，并以终止的 VirtualHost 指令 `</VirtualHost>` 结束。放置在其中的任何指令都应用于虚拟主机。对于匿名或访客站点，添加 `Anonymous` 和 `Guest` 指令。你甚至可以特定目录添加 `Directory` 指令。在独立配置中，通过将 `Port` 指令设置为 `on`，你可以创建一个运行在同一系统上但在不同端口连接的虚拟主机。

```
<VirtualHost 10.0.0.1>

  ServerName "My virtual FTP server"

</VirtualHost>
```

Xinetd 和独立配置处理虚拟主机的方式不同。Xinetd 检测到虚拟主机后，然后将其交给 FTP 守护进程。FTP 守护进程随后检查请求中指定的地址和端口，并为相应的虚拟主机处理请求。在独立配置中，FTP 守护进程持续监听所有指定端口上的请求，并生成子进程来为不断进的不同虚拟主机处理每个请求。在独立配置中，ProFTPD 可以同时支持许多主机。接下来的示例显示了虚拟 FTP 主机的一个示例配置。`VirtualHost` 指令使用域名地址作为参数。当使用域名名时，它必须与网络域名服务器中的 IP 地址关联。而该 IP 地址反过来引用了运行 ProFTPD 守护进程的机器。

```
<VirtualHost 10.0.0.1>

  ServerName "My virtual FTP server"

</VirtualHost>
```

# 第 19 章：Web 服务器：Apache 441

这是用户空间 Web 服务器 Tux 协调使用的端口，类似于 Apache。
`documentroot` 指定了 Web 文档的根目录（Red Hat 上为 `/var/www/html`）。

理想情况下，Tux 作为主 Web 服务器运行，而 Apache 作为次 Web 服务器运行。要配置 Apache 与 Tux 配合运行，需要将 Apache `httpd.conf` 文件中的端口项从 80 更改为 8080：

```
8080
```
