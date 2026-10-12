
如果可以，最好基于 IP 地址而非主机名来配置访问控制。这样做会提升性能，因为无需进行名称解析——客户端的 IP 地址会随每个请求一起发送。

此外，你还可以使用 `allow` 和 `deny` 根据特定环境变量的存在或缺失来允许或拒绝访问网站内容。例如，以下语句拒绝访问包含名为 `NOACCESS` 的环境变量上下文的请求：

```
deny from env=NOACCESS
```

Apache 的默认行为是先应用所有 `deny` 指令，然后再检查 `allow` 指令。如果你希望更改此顺序，可以使用 `order` 语句。Apache 可能会以三种不同的方式解释此语句：

-   **order deny,allow** — 在评估 `allow` 指令之前先评估 `deny` 指令。如果主机未被明确拒绝访问，则允许其访问资源。这是未指定其他内容时的默认排序。
-   **order allow,deny** — 在评估 `deny` 指令之前先评估所有 `allow` 指令。如果主机未被明确允许访问，则拒绝其访问资源。
-   **order mutual failure** — 只有在 `allow` 指令中指定且同时未出现在 `deny` 指令中的主机才被允许访问。如果主机未出现在任一指令中，则不授予访问权限。

来看一个例子。假设你希望仅允许你自己域名内的人员访问你网站上的 `server-status` 资源。如果你的域名是 `gnulix.org`，你可以在配置文件中添加这些行：

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from gnulix.org
</Location>
```

## 认证

认证是确保访问者确实是其声称身份的过程。你可以配置 Apache，仅允许能够验证其身份的客户访问网页内容的特定区域。Apache 中有几种认证方法；基本认证（Basic Authentication）是最常见的（也是本章讨论的方法）。

在基本认证下，Apache 要求用户为访问受保护资源提供用户名和密码。然后，Apache 验证该用户是否被允许访问相关资源。如果用户名可接受，Apache 将验证密码。如果密码也通过验证，用户即获得授权，Apache 将处理该请求。

HTTP 是一种无状态协议；发送到服务器的每个请求和每个响应都是单独处理的，而不是以智能方式处理。因此，认证信息必须包含在每个请求中。这意味着每个针对密码保护区域的请求都更大，因此速度稍慢。为了避免不必要的系统使用和延迟，仅保护你的网站中确实需要保护的区域。

要使用基本认证，你需要一个列出哪些用户被允许访问资源的文件。该文件由包含名称和密码对的纯文本列表组成。它看起来非常像 Linux 系统中的 `/etc/passwd` 用户文件。

**注意**

不要使用 `/etc/passwd` 作为认证的用户列表。当你使用基本认证时，密码和用户名以 base 64 编码的文本形式从客户端发送到服务器——这与纯文本的可读性无异。用户名和密码包含在每个发送到服务器的请求中。因此，任何可能在监视网络流量的人都能获取这些信息！

要为 Apache 创建用户文件，请使用 `htpasswd` 命令。该命令包含在 Apache 软件包中。如果你使用 RPM 安装，它位于 `/usr/bin`。不带任何选项运行 `htpasswd` 将产生以下输出：

```
Usage:
htpasswd [-c|mdps] passwordfile username
htpasswd -b[-cmdps] passwordfile username password

htpasswd -n[mdps] username
htpasswd -nb[mdps] username password
```

-   `-c` 创建一个新文件。
-   `-n` 不更新文件；在标准输出上显示结果。
-   `-m` 强制对密码进行 MD5 加密。
-   `-d` 强制对密码进行 CRYPT 加密（默认）。
-   `-p` 不对密码进行加密（明文）。
-   `-s` 强制对密码进行 SHA 加密。
-   `-b` 使用命令行提供的密码而不是提示输入。
-   `-D` 删除指定的用户。

在 Windows、TPF 和 NetWare 系统上，默认使用 `-m` 标志。在所有其他系统上，`-p` 标志可能无法工作。

如你所见，这是一个使用不太困难的命令。例如，要创建一个名为 `gnulixusers` 且包含用户 `wsb` 的新用户文件，你需要执行类似以下操作：

```
# htpasswd -c gnulixusers wsb
```

然后系统会提示你为该用户输入密码。若要添加更多用户，请重复相同的步骤，只是省略 `-c` 标志。

你还可以创建用户组文件。这些文件的格式类似于 `/etc/groups`。在每一行中，输入组名，后跟冒号，然后列出所有用户，每个用户之间用空格分隔。例如，用户组文件中的一个条目可能如下所示：

```
gnulixusers: vsw ggt jp ajde nadia rkr nak
```

现在你已经知道如何创建用户文件，是时候看看 Apache 如何使用它来保护网络资源了。

要将 Apache 指向用户文件，请使用 `AuthUserFile` 指令。`AuthUserFile` 将用户文件的文件路径作为其参数。如果文件路径不是绝对路径——即不以 `/` 开头——则假设该路径是相对于 `ServerRoot` 的。使用 `AuthGroupFile` 指令，你可以以相同方式指定组文件。

接下来，使用 `AuthType` 指令设置用于此资源的认证类型。在这里，类型设置为 `Basic`。

现在你需要决定资源属于哪个领域（realm）。领域用于将共享相同授权用户的不同资源分组。领域可以是几乎任何字符串。领域会显示在用户网络浏览器上的认证对话框中。因此，你应将领域字符串设置为具有信息量的内容。领域由 `AuthName` 指令定义。

最后，说明哪种类型的用户被授权使用该资源。你通过 `require` 指令来完成此操作。使用此指令的三种方式如下：

-   如果你指定 `valid-user` 作为选项，则用户文件中的任何用户都被允许访问资源（即，前提是他们也输入了正确的密码）。
-   你可以使用 `users` 选项指定允许访问的用户列表。
-   你可以使用 `group` 选项指定组列表。组列表中的条目，以及用户列表中的条目，均以空格分隔。

回到前面看到的 `server-status` 示例，与其根据主机名让用户访问 `server-status` 资源，你可以要求用户通过认证来访问该资源。你可以使用配置文件中的以下条目来实现：

```
<Location /server-status>
    SetHandler server-status
    AuthType Basic
    AuthName "Server status"
    AuthUserFile "gnulixusers"
    Require valid-user
</Location>
```

如果资源同时具有基于主机和基于用户的访问保护，Apache 的默认行为是要求请求者满足这两种控制。但假设你想混合基于主机和基于用户的保护，并允许通过任一方法成功即可访问资源。你可以使用 `satisfy` 指令来实现。你可以将 `satisfy` 指令设置为 `All`（这是默认值）或 `Any`。当设置为 `All` 时，在提供资源之前必须满足所有访问控制方法。如果将 `satisfy` 设置为 `Any`，则只要满足任一访问条件，就会提供资源。

这是另一个访问控制示例，再次使用前面的 `server-status` 示例。这次，你结合访问方法，允许所有来自 GnuIIx 域名的用户访问，而来自域外的人员必须先验证身份才能访问。你可以使用以下内容来实现：

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from gnuix.org
    AuthType Basic
    AuthName "Server status"
    AuthUserFile "gnulixusers"
    Require valid-user
    Satisfy Any
</Location>
```

保护 Web 服务器上的内容还有更多方法，但这里讨论的方法足以让你入门，并且对于大多数情况来说可能已经足够。请参阅 Apache 的在线文档，了解更多关于如何保护网站区域示例。

## Apache 模块

Apache 核心功能相对有限；Apache 的功能来源于模块。每个模块通过添加必要功能来解决明确定义的问题。通过添加或删除模块以提供你希望 Apache 具有的功能，你可以定制 Apache 服务器以满足你的具体需求。

基本 Apache 服务器包含近 50 个核心模块。还有许多其他开发者提供的模块。Apache 模块注册表是 Apache 附加模块的仓库，可在 `http://modules.apache.org/` 找到。模块列在 `/etc/httpd/` 下的 `modules` 目录中，但该目录是链接到模块所在的 `/usr/lib/httpd/modules` 目录的（你的列表可能看起来不同）：

