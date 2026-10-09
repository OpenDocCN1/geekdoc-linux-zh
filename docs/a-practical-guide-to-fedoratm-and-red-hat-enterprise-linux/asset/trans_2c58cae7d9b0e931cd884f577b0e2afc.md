
## 上下文与容器

为了提供灵活性和易于定制性，Apache 使用了配置指令、上下文和容器。上一节介绍了一些配置指令。本节讨论上下文和容器，它们在管理 Apache 服务器中至关重要。

### 上下文

有四个位置，称为*上下文*，定义了配置指令可以出现的位置。本章对每个配置指令进行了标记，以指示它可以出现在哪个上下文中。表 26-1 描述了这些上下文中的每一个。

**表 26-1 上下文**

| 上下文 | 指令可出现的位置 |
| :--- | :--- |
| **server config** | 仅在 **httpd.conf** 文件或包含的文件中，但不包括在 <VirtualHost> 或 <Directory> 容器中（下一节），除非另有标记 |
| **virtual host** | 仅在 **httpd.conf** 文件或包含的文件中的 <VirtualHost> 容器内 |
| **directory** | 仅在 **httpd.conf** 文件或包含的文件中的 <Directory>、<Location> 和 <Files> 容器内 |
| **.htaccess** | 仅在 .htaccess 文件（第 939 页）中 |

通过 Include 指令（第 957 页）引入的文件中的指令是其所包含上下文的一部分，并且必须在该上下文中被允许。

将指令放置在错误的上下文中会导致配置错误，可能导致 Apache 无法正确提供内容或无法启动。

### 容器

*容器*，或称*特殊指令*，是用于将其他指令分组的指令。容器由 XML 风格的标签界定。这里展示了三个示例：

```xml
<Directory> ... </Directory>
<Location> ... </Location>
<VirtualHost> ... </VirtualHost>
```

在 **httpd.conf** 中查找容器的示例。与其他指令一样，容器仅限于在指定的上下文中使用。本节描述了一些更常用的容器。

- **`<Directory>`**
  - **将指令应用于指定目录层次结构中的所有目录。**
  - 语法：`<Directory directory> ... </Directory>`
  - 其中 *directory* 是绝对路径名，指定容器内指令所应用的目录层次结构根目录所在的目录。*directory* 可以包含通配符；`\*` 不匹配 `/`。

`<Directory>` 容器提供与 `.htaccess` 文件（第 939 页）相同的功能。虽然管理员可以在 Apache 配置文件中 `<Directory>` 容器，但普通用户不能使用。普通用户必须使用 `.htaccess` 文件来控制对其自身目录的访问。

以下示例中 `<Directory>` 容器内的指令适用于 `/var/www/html/corp` 目录层次结构。Deny 指令拒绝所有客户端的访问，Allow 指令授予 192.168.10. 子网中的客户端访问权限，而 AllowOverride 指令（第 960 页）使 Apache 能够处理层次结构内 `.htaccess` 文件中的指令：

```apache
<Directory /var/www/html/corp>
    Deny From all
    Allow from 192.168.10.
    AllowOverride All
</Directory>
```

以下 `<Directory>` 容器出现在 `httpd.conf` 文件中，并为整个服务器文件系统（由 `/` 指定）设置了一个限制性环境：

```apache
<Directory />
    AllowOverride None
    Require all denied
</Directory>
```

AllowOverride 指令导致 Apache 不处理 `.htaccess` 文件中的指令。Require 指令（第 961 页）拒绝所有用户访问整个服务器文件系统目录。如果你希望启用较少的限制选项，必须明确启用它们，但这可能会暴露服务器文件系统并危及系统安全。这个限制性 `<Directory>` 容器在 `httpd.conf` 中紧随其后的是一个为 `/var/www` 设置较少限制选项的容器。

```apache
<Directory "/var/www">
    AllowOverride None
    Require all granted
</Directory>
```

前一个 `<Directory>` 容器之后是一个为 DocumentRoot（`/var/www/html`）设置选项的容器；这个容器影响所有内容。`httpd.conf` 中的代码夹杂着许多注释。去掉注释后，它看起来像这样：

```apache
<Directory "/var/www/html">
    Options Indexes FollowSymlinks
    AllowOverride None
    Require all granted
</Directory>
```

Options 指令中的 Indexes 选项允许 Apache 显示目录列表，而 FollowSymlinks 选项使 Apache 跟随符号链接。这个容器比前一个限制性较小，尽管它仍然不允许 Apache 处理 `.htaccess` 文件中的指令。

上下文：server config, virtual host

- **`<Files>`**
  - **将指令应用于指定的普通文件。**
  - 语法：`<Files directory> ... </Files>`
  - 其中 *directory* 是绝对路径名，指定容器内指令所应用的普通文件所在的目录层次结构根目录。*directory* 可以包含通配符；`*` 不匹配 `/`。此容器类似于 `<Directory>`，但适用于普通文件而非目录。

以下指令来自 Fedora/RHEL *httpd.conf* 文件，拒绝访问所有文件名以 `.ht` 开头的文件，这意味着 Apache 将不提供 `.htaccess` 和 `.htpasswd` 文件。

```apache
<Files ".ht*">
    Require all denied
</Files>
```

上下文：server config, virtual host, directory, .htaccess

- **`<IfModule>`**
  - **如果加载了指定模块，则应用指令。**
  - 语法：`<IfModule [!module-name] ... </IfModule>`
  - 其中 *module-name* 是 Apache 测试的模块名称（第 968 页）。如果 *module-name* 已加载，或者如果 *module-name* 未加载且前面有 *!*，则 Apache 执行此容器中的指令。

如果你指定了一个属于未加载模块的配置指令，Apache 将无法启动。

以下 `<IfModule>` 容器位于 Fedora/RHEL *httpd.conf* 文件中，依赖于加载 *mime_magic_module* 模块。如果加载了此模块，Apache 将运行 *MIMEMagicFile* 指令，该指令告诉 *mime_magic_module* 其提示文件的位置。

```apache
<IfModule mime_magic_module>
    MIMEMagicFile conf/magic
</IfModule>
```

上下文：server config, virtual host, directory, .htaccess

- **`<Limit>`**
  - **将访问控制指令限制为指定的 HTTP 方法。**
  - 语法：`<Limit method [method] ... > ... </Limit>`
  - 其中 *method* 是 HTTP 方法。HTTP 方法指定要在 URL 上执行的操作。最常用的方法是 GET、PUT、POST 和 OPTIONS；方法名称区分大小写。GET（默认方法）发送 URL 指示的任何数据。PUT 将通信正文部分的数据存储在指定的 URL。POST 在指定的 URL 创建包含请求正文的新文档。OPTIONS 请求有关服务器功能的信息。

`<Limit>` 容器将一组访问控制指令绑定到指定的 HTTP 方法：只有此容器命名的方法才受这组指令的影响。

以下示例禁用了非 example.com 子域中系统的 HTTP 上传（PUT）：

```apache
<Limit PUT>
    Order deny,allow
    Deny from all
    Allow from .example.com
</Limit>
```

上下文：*server config, virtual host, directory, .htaccess*

> **注意：** 使用 `<LimitExcept>` 容器比使用 `<Limit>` 容器更安全，因为前者可以防止任意方法。当你使用 `<Limit>` 时，你必须小心地明确列出这组指令可能影响的所有可能方法。

- **`<LimitExcept>`**
  - **将访问控制指令限制为除指定 HTTP 方法以外的所有方法。**
  - 语法：`<LimitExcept method [method] ... ... </LimitExcept>`
  - 其中 *method* 是 HTTP 方法。有关方法的讨论请参见 `<Limit>`。

此容器导致一组访问控制指令*不*绑定到指定的 HTTP 方法。因此，*未*在 `<LimitExcept>` 中命名的方法会受到这组指令的影响。

以下 `<LimitExcept>` 容器内的访问控制指令影响除 GET、POST 和 OPTIONS 以外的 HTTP 方法。你可以将此容器放在 `<Directory>` 容器中，以限制其作用范围：

```apache
<LimitExcept GET POST OPTIONS>
    Order deny,allow
    Deny from all
</LimitExcept>
```

上下文：*server config, virtual host, directory, .htaccess*

- **`<Location>`**
  - **将指令应用于指定的 URI。**
  - 语法：`<Location URI> ... </Location>`
  - 其中 *URI* 指向内容；它指定了文件或容器内指令所应用的目录层次结构的根目录。虽然 `<Directory>` 容器指向本地文件系统内部，但 `<Location>` 指向本地文件系统外部。*URI* 可以包含通配符；`*` 不匹配 `/`。

以下 `<Location>` 容器限制来自 example.net 域的客户端访问 `http://server/pop`，其中 *server* 是服务器的 FQDN：

```apache
<Location /pop>
    Order deny,allow
    Deny from all
    Allow from .example.net
</Location>
```

上下文：*server config, virtual host*

