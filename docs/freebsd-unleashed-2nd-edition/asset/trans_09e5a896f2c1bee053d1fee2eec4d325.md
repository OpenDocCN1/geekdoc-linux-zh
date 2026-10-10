
## 基于地址的访问控制

要将目录向除特定指定地址或主机名之外的所有人关闭，请在该目录中放置一个 .htaccess 文件，内容如下：

```
Order deny,allow
Deny from all
Allow from 64.41.131.102
Allow from stripes.somewhere.com
Allow from nowhere.com
Allow from 10.5.100
Allow from 10.67.22.211/255.255.255.0
```

如你所见，允许使用多种不同的地址格式；这些只是匹配规则，如果连接主机匹配其中任何主机名或网络模式，则允许其访问。同样，你也可以让目录向所有人开放，但*排除*某些主机：

```
Order allow,deny
Allow from all
Deny from 133t.hacker.com
Deny from 192.168
```

如果你是在 httpd.conf 中执行此操作，必须将这些命令放在 `<Directory>` 或 `<Location>` 块内；你还可以使用 `<Files>` 或 `<FilesMatch>` 来列出系统中任何位置某些应受访问控制约束的文件：

```
<Files "*.jpg">
    Order deny,allow
    Deny from all
    Allow from 64.41.131.102
</Files>
```

FilesMatch 可用于指定匹配正则表达式的文件名，如下例所示，这将匹配所有 .gif、.jpg、.jpeg 和 .png 文件：

```
<FilesMatch "\.(gif|jpe?g|png)$">
    Order deny,allow
    Deny from all
    Allow from 64.41.131.102
</FilesMatch>
```

但是请注意，`.htaccess` 文件中不可用 `<Directory>` 和 `<Location>`。尽管名为 `<Limit>` 块，但并非之前访问控制工作的必需条件。相反，其目的是列出应应用访问控制的特定访问方法。例如，你选择仅限制 GET 和 POST，但让所有其他方法不受限制。同样，你可以使用 `<LimitExcept>` 来指定不应应用访问控制的唯一方法。你之前看到一个这样的例子，即在控制 /home 内用户目录的注释掉的块中。

## 基于密码的访问控制

有时，按地址限制访问并不实用或可取。例如，你网站的特权部分可以向已付费的注册用户开放，而这些用户可能并非来自可预测的 IP 地址。此时，使用密码认证进行访问控制要合理得多。

Apache 存储自己的用户名和密码数据库，与 /etc/master.passwd 及其相关系统中的全局数据库不同。这是出于安全目的，试图将这两种认证方案合并在一起是非常糟糕的主意，所以连想都不要想。FreeBSD 密码数据库用于认证实际在系统上拥有账户的 shell 用户，而 Apache 认证数据库控制网络浏览者访问网站某些部分的权限。你可能遇到这两种功能领域重叠的情况（例如公司的互联网服务器），但不要受诱惑试图用同一个数据库同时服务两者。如果你成功了，那将成为不安全和不负责任系统管理技术的研究案例。这种做法被 Apache 小组明确反对，你会因此受到同行更多的蔑视而非尊重。不值得。

要为网站的一部分添加密码保护，你需要使用 .htaccess 文件（或 httpd.conf 中的等效配置）——包括适当使用 `<Directory>`、`<Location>` 和 `<Files>` 块——就像按地址访问控制一样。但是，此文件或配置块的内容差异较大，涉及使用 Apache 中完全不同的模块来进行访问控制。此类块的一个简单示例如下：

```
AuthType Basic
AuthName "Restricted Area"
AuthUserFile /usr/local/www/.htpasswd
Require valid-user
```

此示例包含使密码保护生效所需的最少指令数量；每条指令或其替代选项都是必需的。这些指令有些令人困惑，所以让我们逐个来看：

- **AuthType**——可以是 Basic 或 Digest；我们主要关心的是 Basic。
- **AuthName**——这只是“realm”（域）或你保护区域的名称。此名称会显示在用户浏览器的认证窗口中（例如，“为 www.somewhere.com 上的 ‘Restricted Area’ 输入用户名”），帮助用户了解他们正在进入哪个区域，以及需要哪些用户名和密码。名称可以是任何内容，但如果名称中包含空格，必须用引号括起来。
- **AuthUserFile**、**AuthDBUserFile** 和 **AuthDBMUserFile**——必须使用其中一个指令来指定包含该域的用户/密码数据库文件的位置。（如果你愿意，每个域可以使用不同的用户数据库文件。）如果是纯文本文件，使用 AuthUserFile；如果是 db 或 dbm 格式以提高查找速度（如果其中有很多用户，这是一个好主意），则相应使用 AuthDBUserFile 或 AuthDBMUserFile。我们将稍后介绍如何创建纯文本或 db/dbm 用户数据库。
- **AuthGroupFile**、**AuthDBGroupFile** 和 **AuthDBMGroupFile**——这些指令的工作方式与 AuthUserFile 指令相同，只是它们指定 AuthUserFile 指示文件中的用户组，允许你限制对组的访问，而不仅仅是特定用户。此指令不是必需的，但如果使用它，必须存在 AuthUserFile 指令（及相关用户数据库文件），以便识别其用户为所列出组的成员。
- **Require**——告诉 Apache 如何认证用户。参数可以是 valid-user（在 AuthUserFile 文件中存在且输入正确密码的任何用户）、user <username> <username>...（用户列表）或 group <groupname> <groupname>...（组列表）。

### 添加用户

一旦设置好访问控制块并且 `apachectl configtest` 报告配置正常，就可以开始添加用户了。首先，让我们看看如何创建纯文本用户数据库，这是使用 AuthUserFile 指令的类型。要使用的命令是 `htpasswd`，在 FreeBSD 中它位于 /usr/local/bin，因此是你路径的一部分：

```
# htpasswd -c /usr/local/www/.htpasswd frank
```

-c 标志仅首次需要；这告诉 `htpasswd` 创建该文件，因为它尚不存在。然后系统会提示输入用户密码，你必须输入两次（惯例如此）。要在脚本中执行此操作，可以使用 -b 选项并将密码作为另一个参数指定：

```
# htpasswd -b /usr/local/www/.htpasswd joe Pr1d9Lndz
```

另一个有用的选项是 -m，它使 `htpasswd` 使用基于 MD5 的加密算法，而不是系统的 crypt() 例程；这可能提供更好的安全性。其他选项可在 `apachectl` 的手册页中找到。

### 注意

用户数据库文件可以放在系统中 Web 服务器用户（nobody）可读的任何位置，并且可以命名为任何名称，虽然传统上以 .htpasswd 开头并由默认服务器配置保护以防止查看。但是，将文件放在任何可以被拥有 Web 浏览器的用户访问的地方都是个非常糟糕的主意！简而言之，不要将其放在 /usr/local/www/data 内部或任何用户的 public_html 目录中；相反，请使用 Web 不可访问的位置，例如 /usr/local/www 或用户主目录内部。你不希望人们下载你的用户数据库并破解它！

纯文本用户数据库适用于小型用户列表；然而，一旦你开始处理数十或数百个用户，查找用户密码所需的时间会使认证过程变得繁琐甚至无法工作。解决方案是使用真正的数据库文件，无论是 db 还是 dbm 形式，并使用相应的 AuthDBUserFile 或 AuthDBMUserFile 指令。允许你操作数据库文件的支持程序是 /usr/local/bin/dbmanage：

```
# dbmanage /usr/local/www/.httpwwdb adduser frank
New password:
Re-type new password:
User frank added with password encrypted to NtmDxy6jvyW7A using crypt
```

此示例将创建一个名为 /usr/local/www/.httpwwdb 的 db 风格数据库文件，然后你可以使用 AuthDBUserFile 指令访问它。如有必要，也可以使用 dbm 等效项，但你不应该需要。有关可用于用户管理命令的更多详细信息，请参阅 `dbmanage` 手册页。

### 添加组

在纯文本文件（AuthGroupFile）中列出组非常简单。每行包含组名、冒号，然后是组内用户列表：

```
group: frank joe alice
```

组文件可能应与用户文件保存在同一位置，并使用相似的名称；然而，由于组文件不包含任何密码，安全考虑就不那么关键了。

组文件也可以通过 `dbmanage` 进行管理，但通常不需要这样做，因为（与 /etc/group 一样）组数量很少像用户数量那么多。如果你希望混合格式，可以将 AuthGroupFile 与 AuthDBUserFile 配合使用；这可能是维护大型用户列表和小型组列表的最简单方法。

