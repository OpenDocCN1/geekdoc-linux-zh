
`ServerType`指令设置`httpd`守护进程是以独立模式运行还是由`inetd`管理。

```
ServerType standalone
```

`MinSpareServers`和`MaxSpareServers`指令管理常驻的`httpd`进程数量。Apache 试图维持处理当前负载所需的进程数量，外加少量额外进程。如果备用服务器数量低于最小值，则会启动更多进程。如果备用服务器数量超过最大值，则部分进程会被终止。针对预期负载调整这些设置。

```
MinSpareServers 5
MaxSpareServers 15
```

`StartServers`指令规定初始启动的进程数量。

```
StartServers 5
```

`MaxClients`指令定义启动进程数量的上限。如果尝试连接的客户端数量超过设定的数量，他们将被拒绝访问。这主要是为了防止服务器失控，因为大多数站点不希望意外地将用户锁定在外。将此值设置得远高于你预期的用户数量。

```
MaxClients 150
```

`Listen`指令将`httpd`守护进程绑定到特定的 IP 地址或端口，除了使用`BindAddress`配置的默认 IP 和端口外：

```
Listen 192.168.10.2:80
```

`AccessFileName`指令设置覆盖文件的名称，通常是`.htaccess`。

```
AccessFileName .htaccess
```

# 目录块指令

Apache 允许你定义一些指令块，使其仅适用于特定的目录树。这样，站点的某些部分可以与其他部分不同地进行配置。该块以`<Directory path>`指令开始，以`</Directory>`指令结束。以下是一个示例。

```
<Directory /Games>
Options SymLinksIfOwnerMatch
AllowOverride None
</Directory>
```

包含在此块中的任何指令仅适用于所定义的目录。`Options`指令允许启用或配置特殊功能。此示例中的指令允许 Web 服务器仅在所有者匹配时跟踪符号目录链接，以确保安全性。`AllowOverride`指令定义`.htaccess`文件是否可以覆盖在此块中指定的选项。

# 访问控制

通过使用`allow`和`deny`访问控制指令，你可以调整哪些用户可以访问你站点上的目录。此示例以`<Location /doc>`指令开始，并以`</Location>`指令结束。`Location`指令指定某个目录，并允许你分配特定的指令。以下是这些指令的示例：

```
<Location /doc>
order deny,allow
deny from all
allow from 127.0.0.0/255.0.0.0
Options Indexes FollowSymLinks
</Location>
```

`order`语句表示先拒绝后允许。这导致服务器拒绝所有人，除了明确允许的人。`deny`和`allow`指令表明，只有坐在该系统的用户可以访问`/doc`目录，因为它只允许回环网络。`Options`指令启用了`Indexes`，这导致服务器在找不到默认 Web 页面时发送一个格式良好的目录列表。在`Options`中启用的还有`FollowSymLinks`，它允许服务器跟踪目录中的符号链接。

这些指令也可以用于其他类型的块，例如`Directory`和`Files`。

# 别名和重定向

`Alias`指令可以将用户指向另一个目录，即使它在另一个文件系统上。

```
Alias /icons/ /usr/share/apache/icons/
```

这样，`icons`目录看起来像是`DocumentRoot`目录的子目录，但实际上位于`/usr/share/apache/icons`。

`Redirect`指令允许你将用户指向文档的新位置。语法如下：

```
Redirect Old_URL New_URL
```

# 默认页面

大多数用户不会输入完整的 URL，例如`http://www.debian.org/index.html`，而是只输入`http://www.debian.org`。那么，站点如何知道应该提供哪个页面？这是通过`DirectoryIndex`指令设置的。

```
DirectoryIndex index.html index.htm index.shtml index.cgi
```

默认情况下，服务器会按照列出的顺序查找页面，并显示找到的第一个页面。

# 用户 Web 目录

许多站点允许用户创建 Web 站点。这是通过`UserDir`指令配置的。

```
UserDir public_html
```

这告诉服务器在`~/public_html`目录中查找。如果有人尝试打开`http://www.homepages.com/~jnash`，服务器实际上会访问`http://www.homepages.com/~jnash/public_html`。这是一种让用户设置自己页面的好方法，无需担心存储这些页面的中心位置。

# MIME 类型

`TypesConfig`指令告诉服务器`mime.types`配置文件存储在哪里。该文件告诉服务器哪些 MIME 类型对应哪些文件扩展名。

```
TypesConfig /etc/mime.types
```

`DefaultType`指令告诉服务器如何处理未知 MIME 类型的文件。

```
DefaultType text/plain
```

# CGI 文件

CGI（通用网关接口）文件是用于提供站点动态内容的程序或脚本。`ScriptAlias`指令定义了这些文件所在的目录。

```
ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
```

必须特别注意 CGI 文件，因为错误的权限或不良代码可能导致严重的安全漏洞。

```
IndexOptions FancyIndexing
```

还有其他一些有用的`IndexOptions`可用，例如`ScanHTMLTitles`、`IconsAreLinks`和`FoldersFirst`。`ScanHTMLTitles`读取 HTML 文件并使用标题而不是文件名。`IconsAreLinks`允许用户点击图标，而不仅仅是点击文件名。`FoldersFirst`将文件夹列在顶部，文件列在下方。

```
IndexOptions ScanHTMLTitles IconsAreLinks FoldersFirst
```

以下指令允许你微调用于列表的图标。

```
DefaultIcon /icons/unknown.gif
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
```

`AddDescription`指令允许你为匹配某个模式的文件或一组文件添加描述。

```
AddDescription "GZIP compressed tar archive" .tgz
```

`HeaderName`和`ReadmeName`指令指定某些文本文件的显示方式。由`HeaderName`定义的文件附加在目录列表的顶部，而`ReadmeName`附加在底部。

```
ReadmeName README
HeaderName HEADER
```

# 认证

Apache 提供了认证机制，允许你保护目录或整个站点。最基本的形式使用包含用户账户和加密密码的文件。下面是一个示例块，显示了所需的指令。

```
<Directory /home/httpd/html/private>
AuthType Basic
AuthName Private
AuthUserFile /etc/web.users
AuthGroupFile /etc/web.groups
Require valid-user
</Directory>
```
