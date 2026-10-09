

## 允许来自环境变量=变量指令

```
<Directory /Mysite/myboss/rants>
order deny, allow
deny from myboss.mycompany.com
allow from all
</Directory>
```

通常，影响所有主机的指令优先级最低。在上面的示例中，由于`allow`指令影响所有主机，因此它的优先级较低。

尽管`allow`、`deny`和`deny, allow`是`order`指令最常用的值，但你也可以使用另一个值`mutual-failure`，以表明只有那些出现在`allow`列表中但未出现在`deny`列表中的主机才能访问。在所有情况下，每一个`allow`和`deny`指令都会被评估。

### 拒绝来自环境变量=变量

此指令是`deny`指令的一种变体，它拒绝所有设置了指定环境的主机的访问权限。

**语法**: `deny from env=variable`

**上下文**: 目录、位置、目录级访问控制文件（.htaccess）

**覆盖**: 限制

例如，如果你想拒绝所有使用微软Internet Explorer的主机访问，你可以使用`BrowserMatch`指令，每当浏览器向服务器标识自己并包含字符串"MSIE"时，设置一个名为`ms_browser`的变量。

```
BrowserMatch "MSIE" ms_browser
```

现在你可以使用`<Directory>`容器来指定`deny`指令，如下所示：

```
<Directory /path/to/vbscript_directory>
    order deny,allow
    allow from all
    deny from env=ms_browser
</Directory>
```

如果你有兴趣阻止对特定HTTP请求方法（如GET、POST或PUT）的访问，你可以使用`<Limit>`容器来实现。例如：

```
<Location /cgi-bin>
    <Limit POST>
        order deny,allow
        deny from all
        allow from yourdomain.com
    </Limit>
</Location>
```

此示例允许对`cgi-bin`目录的POST请求，仅当请求来自`yourdomain.com`域中的主机时。换句话说，如果该网站有一些HTML表单通过HTTP POST方法发送用户输入数据，那么只有yourdomain.com的用户才能有效使用这些表单。通常，CGI应用程序存储在`cgi-bin`目录中，许多网站都提供使用POST方法向CGI应用程序提交数据的HTML表单。使用上述基于主机的访问控制配置，网站可以允许任何人运行CGI脚本，但只允许特定网站（在此情况下为yourdomain.com）实际向一个或多个CGI脚本发布数据。这使得该网站的CGI访问具有一定的只读特性。每个人都可以运行生成输出的应用程序而不接受任何用户输入，但只有特定域的用户才能提供输入。

### 组合身份验证与授权

mod_auth中的基本HTTP用户身份验证支持和mod_access中的访问授权支持可以结合起来实现实际的身份验证问题。例如，假设你希望允许一组用户仅在他们通过AOL连接浏览网站时才能访问你网站的/aolbuddies/部分。以下是你可以在httpd.conf中添加的配置，在适当替换路径和文件名之后：

```
Alias /aolbuddies/    "/path/to/web/directory/for/aolbuddies/"

<Location /aolbuddies/>
    Deny from all
    Allow from .aol.com

    AuthName "AOL Buddies Only"
    AuthType Basic
    AuthUserFile /path/to/.myusers.pwd
    AuthGroupFile /path/to/.mygroups
    Require group aolbuddies

    Satisfy all
</Location>
```

Satisfy all指令告知Apache仅允许通过身份验证和授权测试的用户访问。当AOL用户通过AOL连接到http://your_server/aolbuddies/时，系统会提示用户输入用户名和密码。如果用户输入属于aolbuddies组的用户名且用户密码正确，则允许用户访问。

> **注意** 你必须将所有你的AOL好友添加为/path/to/.myusers.pwd中的用户，并在/path/to/.mygroups中创建一个名为aolbuddies的组，该组中列出所有AOL好友（你之前添加的/path/to/.aol中的用户）。

### 使用关系数据库进行身份验证

如果你在网络（甚至Web服务器）上运行关系数据库服务器，并且有大量的用户（即超过1,000名用户）需要通过Web进行身份验证，你可以使用数据库服务器替代前文讨论的基于文本文件的（mod_auth）身份验证。使用数据库服务器处理大量用户有几个优点；主要优点如下：

- 当大量用户存储在文本文件中时，mod_auth身份验证会变得非常缓慢。
- 如果你允许用户通过Web使用自定义应用程序更改密码，文本文件是不安全的，因为你必须确保对文件的写访问正确地加锁和解锁。将数据存储在数据库服务器中消除了脚本中的这种额外负担，并提供了更好的整体数据完整性。

在关系数据库中，你可以存储大量关于用户的信息，这些信息可以被你的Web应用程序使用。因此，使用MySQL等数据库服务器集中用户数据库对长期来看是有意义的。

### 注意事项

你可以使用大多数现代关系数据库服务器（如MySQL、Postgres、DB2、Oracle和Microsoft SQL）作为用户数据库。安装这些数据库服务器中的任何一个超出了本书的范围。我假设你已经在你的网络或Web服务器上安装了这些数据库服务器之一。

### 提示

对于拥有许多用户的网站，你可能希望创建一个专用的数据库服务器，使其在你的Web网络上可访问。理想情况下，数据库服务器应通过后端网络而不是互联网进行访问。大多数情况下，最好在每台服务器系统上有一个额外的以太网接口，并创建一个仅局域网内的服务器可访问的LAN。（有关如何创建此类网络的详细信息，请参阅第23章。）

### 使用MySQL数据库服务器进行身份验证

MySQL是开源社区中最广泛使用的免费数据库服务器；它在GNU公共许可下可用。安装和设置你的服务器作为用户身份验证数据库服务器非常容易。使用Linux平台，你可以简单地下载并安装服务器、客户端和开发RPM包，几分钟内即可就绪！MySQL服务器可在www.mysql.com下载。

### 在MySQL服务器中创建用户身份验证数据库

要将MySQL服务器用作身份验证数据库，你需要在数据库中的表中至少包含用户名和密码信息。如果你已经有了包含此类信息的现有数据库表，则无需遵循此处给出的步骤。

1. 使用`mysql -u root -p`命令登录到MySQL服务器。你将需要输入数据库的root密码。

### 警告

MySQL服务器的root密码应始终与你的Unix系统上的root密码不同。它们服务于不同的目的，因此应保持分开。

2. 登录到MySQL后，运行`create database auth;`命令，这将创建一个名为`auth`的数据库。

