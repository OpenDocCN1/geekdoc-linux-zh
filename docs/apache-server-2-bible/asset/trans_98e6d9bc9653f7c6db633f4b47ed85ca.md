
## 适当的文件和目录权限

```
├---cgi-bin (ScriptAlias)
└---logs (CustomLog 和 ErrorLog)
```

上述目录结构在许多方面都是安全的。为了理解其原因，首先查看 **httpd.conf** 中针对上述目录结构的以下 Apache 配置。

```
ServerRoot     "/home/httpd"
DocumentRoot     "/www/htdocs"
ScriptAlias     /cgi-bin/ "/www/cgi-bin/"
CustomLog     /www/logs/access.log common
ErrorLog     /www/logs/error.log
```

由于这些主要目录中的每一个都是独立的（即没有一个目录是另一个目录的子目录），因此它们彼此之间是安全的。在一个目录中的权限错误不会影响另一个目录。如果你不认为这是件大事，请数一下你参与用户和 Linux 工作的年限，然后通读所有的墨菲定律。

需要为上述目录结构设置适当的权限。

由 **ServerRoot** 指定的目录应仅对 root 用户可访问，因为除了 root 之外，没有人需要配置或运行 Apache。**DocumentRoot** 应该对管理你网站内容的一个或多个用户以及 Apache 用户（通过使用 **User** 指令指定）或 Apache 组（通过使用 **Group** 指令指定）可访问。例如，如果你想让一个名为 **htmlguru** 的用户在你的网站上发布内容，并且你以 **httpd** 用户身份运行 Apache，你可以通过以下步骤让 Apache 和指定用户都能访问 **DocumentRoot** 目录：

- 1. 创建一个新的名为 webteam 的组：
  `groupadd webteam`
- 2. 将 **htmlguru 用户** 添加到 webteam 组：
  `usermod -G webteam htmlguru`
- 3. 更改 **DocumentRoot** 目录（及其下面所有子目录）的所有者：
  `chown -R httpd.webteam /www/htdocs`

此命令将目录所有者设置为 Apache（即 `httpd` 用户），将组所有者设置为 `webteam`，其中包含 `htmlguru` 用户。换句话说，Apache 和 `htmlguru` 都将拥有访问文档树的权限。

- 4. 更改 `DocumentRoot` 目录（及其下面所有子目录）的权限，如下所示：

```bash
chmod -R 2570 /www/htdocs
```

此命令确保 `DocumentRoot` 下的文件和子目录可被 Apache 用户读取和执行，并且 `webteam` 组可以读取、写入和执行所有内容。它还确保每当在文档树中创建新文件或目录时，`webteam` 组都将拥有访问权限。

这种方法的一个巨大优点是，将新用户添加到 webteam 就像运行以下命令一样简单：

```bash
usermod -G webteam new_username
```

同样，如果你希望将现有用户从 `webteam` 组中移除，只需运行：

```bash
usermod -G username [group1,group2,group3,...]
```

其中 `group1`、`group2`、`group3` 等是该用户所属的组（不包括 `webteam` 组）。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_535_0.png)

> 你可以通过运行 `groups username` 命令来了解用户属于哪些组。

由 `ScriptAlias` 指定的目录应仅对 CGI 开发人员和在 `httpd.conf` 中使用 `User` 指令指定的 Apache 用户可访问。我建议你为开发人员创建一个新的名为 `webdev` 的组。尽管开发组（如 `webdev`）需要对该目录具有读取、写入和执行权限，但 Apache 用户只需要读取和执行权限。不要允许 Apache 用户在此目录中写入文件。例如，假设你的 `httpd.conf` 中有以下 `ScriptAlias`：

```bash
ScriptAlias /cgi-bin/ "/www/cgi-bin/"
```

如果 `httpd` 是你的 Apache 用户，`webdev` 是你的开发组，你应该按如下方式为 `/www/cgi-bin` 设置权限：

```bash
chown -R httpd.webdev /www/cgi-bin
chmod -R 2570 /www/cgi-bin
```

或者，如果你只想允许单个用户（例如 `cgiguru`）开发 CGI 脚本，你可以按如下方式设置文件和目录权限：

```bash
chown -R cgiguru.httpd /www/cgi-bin
chmod -R 750 /www/cgi-bin
```

这里，用户 `cgiguru` 拥有该目录，而用于 Apache 服务器的组（由 `Group` 指令指定）是该目录及其文件的组所有者。

最后，`CustomLog` 和 `ErrorLog` 指令中使用的日志目录应仅允许 `root` 用户写入。对此类目录（例如 `/www/logs`）推荐的权限设置如下：

```
chown -R root.root /www/logs
chmod -R 700 /www/logs
```

> 不要允许任何人（包括 Apache 用户或组）读取、写入或执行在 `CustomLog` 和 `ErrorLog` 指令中指定的日志目录中的文件。

始终确保你对通过 Web 可访问的新目录采用最小化方法授予访问权限。还要确保你不允许 Web 访客查看任何目录列表。你可以使用后面讨论的方法隐藏目录列表。

## 目录索引文件

每当用户请求通过 Web 访问某个目录时，Apache 会执行以下操作之一：

- 1. 检查该目录是否可访问。如果是，则继续；否则，显示错误消息。
- 2. 在确定目录可访问后，它查找通过使用 `DirectoryIndex` 指令指定的目录索引文件。默认情况下，该文件是 `index.html`。如果它能读取请求目录中的此文件，则显示文件内容。如果不存在此类文件，Apache 将检查是否可以为该目录创建动态列表。如果允许创建动态列表，它将创建该列表并向用户显示目录内容。

由于 Apache 创建的动态生成的目录列表会为潜在的不良分子提供关于你的目录结构的线索，因此你不应该允许此类列表。避免创建动态目录列表的最简单方法是创建一个文件名在 `DirectoryIndex` 指令中指定的文件。例如，如果你将 `DirectoryIndex` 设置如下：

```
DirectoryIndex index.html index.htm
```

Apache 将首先在 URL 请求的目录中查找 `index.html`，如果 `index.html` 缺失，则查找 `index.htm`。

然而，许多网站暴露目录的一个常见原因是，当创建新目录时，创建者忘记创建索引文件或上传了大小写错误的索引文件，例如 `INDEX.HTML` 或 `INDEX.HTM`。

如果这种情况经常发生，你可以使用 CGI 脚本自动将用户重定向到你的主页或内部搜索引擎界面。只需修改 *DirectoryIndex* 指令如下：

```
DirectoryIndex index.html index.htm /cgi-bin/index.pl
```

现在，在 *ScriptAlias* 指定的目录中添加一个 CGI 脚本，例如清单 18-1 中所示的那个。

### 清单 18-1: **index.pl**

```perl
#!/usr/bin/perl
# Purpose: this script is used to redirect
# users who enter a URL that points to
# directories without index.html page.
use CGI qw(:standard);

# Set the automatically redirect URL
my $AUTO_REDIRECT_URL = '/';

# Get the current URL path
my $curDir = $ENV{REQUEST_URI};

# If the current URL path is not home page (/)
# then redirect user to home page
if ($curDir ne '/') {
    print redirect($AUTO_REDIRECT_URL);
    # If the home page is also missing the index page,
    # we can't redirect back to home page (to avoid
    # recursive redirection), so display an error message.
} else {
    print header;
    print "HOME PAGE NOT FOUND!";
}
exit 0;
```

此脚本在 Apache 未能找到目录索引文件（*index.html* 或 *index.htm*）后运行。该脚本只是将 URL 指向没有索引文件的目录的用户重定向到网站的主页。

如果你使用不同的别名名称，请确保更改上述指令中的 /cgi-bin/ 路径。如果你根本不想显示任何目录列表，你可以简单地通过设置以下配置来禁用目录列表：

```
<Directory />
  Options -Indexes
</Directory>
```

*Options* 指令告诉 Apache 禁用所有目录索引处理。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_538_0.png)

> 告诉 Apache 不要跟随符号链接也是一个好主意，因为这些链接可能会意外地暴露你不希望公开的部分磁盘空间。要禁用 Apache 跟随符号链接，请将 *Options* 指令设置为 -FollowSymLinks。

## 禁用默认访问

一个好的安全模型规定不存在默认访问权限，因此要养成首先不允许任何访问权限的习惯。仅向特定目录允许特定访问。要实施无默认访问，请在 `httpd.conf` 中使用以下配置段：

```
<Directory />
  Order deny,allow
  Deny from all
</Directory>
```

这会首先禁用所有访问。现在，如果你需要启用对特定目录的访问，请再次使用 `<Directory ...>` 容器来打开该目录。例如，如果你想允许访问 /www/htdocs，请添加以下配置：

```
<Directory "/www/htdocs">
  Order deny,allow
  Allow from all
</Directory>
```

这种方法——只打开你需要的——是一种预防性安全措施，并高度推荐。此外，不要允许用户使用每目录配置文件（.htaccess）来更改开放访问的目录中的任何目录级配置选项。

## 禁用用户覆盖

要在任何目录中使用每目录配置文件（.htaccess）禁用覆盖配置设置，请执行以下操作：

```
<Directory />
  AllowOverride None
</Directory>
```
