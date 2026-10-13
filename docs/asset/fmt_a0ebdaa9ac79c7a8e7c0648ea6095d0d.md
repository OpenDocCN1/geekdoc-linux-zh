
## 第 15 章：Web 服务器安全

- `DocumentRoot` 存储如 HTML、JavaScript 和图像等 网站内容。
- `ScriptAlias` 存储 CGI 脚本。
- `CustomLog` 和 `ErrorLog` 存储访问和错误日志文件。你可以为这些指令分别指定两个不同的目录，但从长远来看，将所有日志文件放在一个日志目录通常是易于管理的。

我建议使用目录结构，使得所有主目录都是相互独立的——这意味着没有一个主目录是其他目录的子目录。

- `ServerRoot` 应该指向一个只有 root 用户才能访问的目录。
- `DocumentRoot` 目录需要权限：
    - 维护你 网站的用户
    - Apache 用户或组（使用 `httpd.conf` 文件中的 `User` 和 `Group` 指令指定）
- `ScriptAlias` 目录应该仅允许脚本开发者和 Apache 用户或组访问。
- `CustomLog` 或 `ErrorLog` 目录应该仅允许 root 用户访问。

即使是 Apache 用户或组也不应该拥有日志目录的权限。下面的示例了这样的目录结构：

```
/ 
+--home
  |--httpd (ServerRoot)
  |--www
    |--htdocs (DocumentRoot)
    |--cgi-bin (ScriptAlias)
    |--logs (CustomLog and ErrorLog)
```

这种目录结构在许多方面都是非常安全的。要理解为什么，请首先查看 `httpd.conf` 中的以下 Apache 配置。

```
ServerRoot /home/httpd
DocumentRoot /www/htdocs
ScriptAlias /cgi-bin/ "/www/cgi-bin"
CustomLog /www/logs/access.log common
ErrorLog /www/logs/error.log
```

## 第四部分：网络服务安全

因为所有这些主要目录都是独立的（没有一个是是另一个的子目录），所以它们是安全的。一个目录中的权限错误不会影响其他目录。

### 使用适当的文件和目录权限

`ServerRoot` 应该仅允许 root 用户访问，但除了 root 之外，没人应该配置或运行 Apache。`DocumentRoot` 应该允许管理你 网站内容的用户以及 Apache 用户（使用 `User` 指令指定）或 Apache 组（使用 `Group` 指令指定）。

例如，如果你有一个名为 `htmlguru` 的用户用于在你的 网站上发布内容，并且你以 `httpd` 身份运行 Apache，以下是让 Apache 和指定用户都能访问 `DocumentRoot` 目录的方法：

- 使用此命令创建一个新组 `webteam`：

```
groupadd webteam
```

- 使用此命令将 `htmlguru` 作为用户添加到 `webteam` 组：

```
usermod -G webteam htmlguru
```

- 使用此命令更改 `DocumentRoot` 目录（及其下方的所有子目录）的所有者：

```
chown -R httpd:webteam /www/htdocs
```

此命令将目录所有权设置为 Apache（即 `httpd` 用户），并将组所有权设置为 `webteam`，该组包含了 `htmlguru` 用户。这意味着 Apache 和 `htmlguru` 都可以访问文档树。

- 按照这种方式更改 `DocumentRoot` 目录（及其下方的所有子目录）的权限：

```
chmod -R 2770 /www/htdocs
```

此命令使得 `DocumentRoot` 下的文件和子目录对 Apache 用户来说是可读和可执行的，并让 `webteam` 组可以读取、写入和执行一切。它确保了每当在文档树中创建新文件或目录时，`webteam` 组都有访问权限。

这种方法的一个巨大优势是向 `webteam` 添加新用户只需运行以下命令：

```
usermod -G webteam <username>
```

- 从 `webteam` 组中移除现有用户，只需运行：

```
usermod -G <username> [group1,group2,group3,...]
```

在此配置中，`group1`、`group2`、`group3` 等是该用户所属的组（不包括 `webteam` 组）。

你可以通过运行 `group <username>` 命令来找到用户所属的（组）。

`ScriptAlias` 应该仅允许 CGI 开发者和 Apache 用户访问。我建议你为开发者（们）创建一个新组 `webdev`。虽然开发者组（`webdev`）需要该目录的读取、写入和执行权限，但 Apache 用户只需要读取和执行权限。不要允许 Apache 用户在此目录中写入文件。例如，你在 `httpd.conf` 中有以下 `ScriptAlias`：

```
ScriptAlias /cgi-bin/ "/www/cgi-bin/"
```

如果 `httpd` 是你的 Apache 用户，`webdev` 是你的开发者组，请如下设置 `/www/cgi-bin` 的权限：

```
chown -R httpd:webdev /www/cgi-bin
chmod -R 2770 /www/cgi-bin
```

或者，如果你只想让一个用户（例如 `cgiguru`）开发 CGI 脚本，你可以这样设置文件和目录权限：

```
chown -R cgiguru:httpd /www/cgi-bin
chmod -R 750 /www/cgi-bin
```

在此处，用户 `cgiguru` 拥有该目录，而用于 Apache 服务器的组（由 `Group` 指令指定）是该目录及其文件的所有者。

`CustomLog` 和 `ErrorLog` 指令使用的日志目录应该只允许 root 用户写入。对于此类目录（例如，`/www/logs`），推荐的权限设置为：

```
chown -R root:root /www/logs
chmod -R 700 /www/logs
```

许多 网站出现暴露目录的一个常见原因是有人创建了目录但忘记创建索引文件（`index.html` 或 `INDEX.HTM`）。如果这种情况频繁发生，可以使用 CGI 脚本将用户重定向到首页或内部搜索界面。只需修改 `DirectoryIndex` 如下：

```
DirectoryIndex index.html
```

### 列表 15-1：index.pl

```perl
#!/usr/bin/perl
# 目的：此脚本用于重定向指向
# 没有 index.html 页的用户
#
### 设置自动重定向 URL
my $AUTO_REDIRECT_URL = '/';
# 获取当前 URL 路径
my $curDir = $ENV{REQUEST_URI};
### 如果路径不是首页 (/)
### 重定向用户到首页
if ($curDir ne '/') {
    print redirect($AUTO_REDIRECT_URL);
    # 如果首页也缺少索引页，
    # 我们无法重定向回首页（以避免递归重定向）
    # 显示错误消息。
} else {
    print header;
    print "HOME PAGE NOT FOUND!";
}
exit 0;
```

当 Apache 运行运行时找不到目录索引文件（`index.html` 或 `index.htm`）时，此脚本会将指向没有索引文件的目录的用户重定向到 网站的首页。

![](img/177ab5b774eeb101e12de61f8616d71a_379_0.png)

如果你不想显示目录列表，可以通过设置以下配置禁用目录列表：

```
<Directory />
Options -Indexes
</Directory>
```
