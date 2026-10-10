
`AllowOverride`可以设置为`All`，或者`Options`、`FileInfo`、`AuthConfig`和`Limit`的任意组合。这些选项的解释如下。

- **`Options`**：`.htaccess`文件可以添加此目录`Options`指令中未列出的选项。

- **`FileInfo`**：`.htaccess`文件可以包含用于修改文档类型信息的指令。

- **`AuthConfig`**：`.htaccess`文件可以包含授权指令。

- **`Limit`**：`.htaccess`文件可以包含`allow`、`deny`和`order`指令。

## 虚拟主机

使用Web服务器提供的更受欢迎的一项服务是托管虚拟域名，也称为虚拟主机。这是一个拥有自己域名的完整网站，就像是一台独立的机器一样，但它与其他网站托管在同一台机器上。`Apache`通过`httpd.conf`配置文件中的指令以简单的方式实现了这种能力。在`Apache`服务器上托管虚拟主机有两种方式。你可以拥有一个IP地址和多个`CNAMES`，或者拥有多个IP地址，每个地址一个名称。`Apache`有不同类型的指令集来处理这两种选项。

### 基于地址的虚拟主机

在配置好Linux机器具有多个IP地址之后，设置`Apache`将它们作为不同的网站提供服务非常简单。你只需要为每个想要作为独立网站的地址在`httpd.conf`文件中放入一个`VirtualHost`指令：

```apache
<VirtualHost www.virtual.com>
 ServerName www.virtual.com
 DocumentRoot /home/virtual/public_html
 TransferLog /home/virtual/logs/access_log
 ErrorLog /home/virtual/logs/error_log
</VirtualHost>
```

你应该在`VirtualHost`标签中使用IP地址，而不是主机名。

你可以指定`<VirtualHost>`标签内的任何配置指令。例如，你可能希望为虚拟主机设置与主服务器不同的`AllowOverride`指令。未指定的任何指令都将默认为主服务器的设置。

不能设置为在`VirtualHost`部分中设置的指令包括`ServerType`、`StartServers`、`MaxSpareServers`、`MinSpareServers`、`MaxRequestsPerChild`、`BindAddress`、`Listen`、`PidFile`、`TypesConfig`、`ServerRoot`和`NameVirtualHost`。

### 基于名称的虚拟主机

基于名称的虚拟主机允许你在同一个IP地址上运行多个主机。你需要将这些附加名称作为`CNAME`添加到你的DNS中，指向相应机器。当HTTP客户端（浏览器）向你的服务器请求文档时，它会在请求中发送一个变量，指示其请求文档的服务器名称。基于此变量，服务器确定应该从哪个虚拟主机提供内容。

**注意：**

一些旧版浏览器无法看到基于名称的虚拟主机，因为这是`HTTP 1.1`的一个特性，而这些旧版浏览器严格遵循`HTTP 1.0`标准。然而，许多其他旧版浏览器部分支持`HTTP 1.1`，而这是大多数浏览器已支持一段时间的`HTTP 1.1`功能之一。

基于名称的虚拟主机比基于IP地址的虚拟主机只需要多一步额外操作。你首先需要指示哪个IP地址拥有多个DNS名称。这通过`NameVirtualHost`指令完成。

```
NameVirtualHost 192.168.204.24
```

然后你需要为该地址上的每个名称设置一个章节，配置该名称的设置。与基于IP的虚拟主机一样，你只需要设置那些需要不同配置的主机。你必须设置`ServerName`指令，因为这是区分不同主机的唯一依据：

```
<VirtualHost 192.168.204.24>
ServerName bugserver.database.com
ServerAlias bugserver
DocumentRoot /home/bugserver/htdocs
ScriptAlias /home/bugserver/cgi-bin
TransferLog /home/bugserver/logs/access_log
</VirtualHost>
```

```
<VirtualHost 192.168.204.24>
ServerName pts.database.com
ServerAlias pts
DocumentRoot /home/pts/htdocs
ScriptAlias /home/pts/cgi-bin
TransferLog /home/pts/logs/access_log
ErrorLog /home/pts/logs/error_log
</VirtualHost>
```

#### 提示

如果你在内网或内部网络上托管网站，用户经常会使用机器的短名称而不是完全限定域名。例如，他们可能在浏览器位置栏中输入`http://bugserver/index.html`，而不是`http://bugserver.database.com/index.html`。在这种情况下，`Apache`不会识别这两个地址应该指向同一个虚拟主机。你可以通过为`bugserver`和`bugserver.database.com`都设置`VirtualHost`指令来解决这个问题，但简单的解决方法是使用`ServerAlias`指令，该指令列出了机器的所有有效别名：

```
ServerAlias bugserver
```

###### 警告

如果你计划在你的系统上运行大量虚拟主机，你应该考虑将所有记录的信息发送到标准的`Apache`日志文件，而不是发送到单独的文件。原因是你可能会达到系统的文件描述符限制，因为每个日志文件都会消耗一个文件描述符。Linux 2.2中每个进程的系统限制为1024，但由于`ulimit`限制，实际可能低得多。此问题的症状包括诸如“无法fork”、“日志文件未写入信息”或“HTTP请求响应缓慢”等错误消息。

###### 日志记录

`Apache`几乎可以提供你感兴趣的任何来自Web访问的信息。运行`Apache`服务器时会产生两个标准日志文件——`access_log`和`error_log`。除了`error_log`之外的所有日志（默认情况下，这就是`access_log`）都是按照`CustomLog`和`LogFormat`指令指定的格式生成的。这些指令出现在你的`httpd.conf`文件中。

可以使用`LogFormat`指令定义新的日志格式：

```
LogFormat " %h %l %u %t "%r" %>s %b" common
```

通用日志格式是创建自定义日志格式的良好起点。请注意，大多数可用的日志分析工具都假设你使用的是通用日志格式或组合日志格式，这两种格式都在默认配置文件中定义。

以下变量可用于`LogFormat`语句：

- `%b`发送的字节数，不包括HTTP头。

- `%f`文件名。

- `%(VARIABLE)e`环境变量*VARIABLE*的内容。

- `%h`远程主机。（*注意：*如果你有高流量，不要包含此变量，因为它会导致每次命中都进行反向DNS查找。）

- `%a`远程IP地址。

- `%(HEADER)i`发送到服务器的请求中*HEADER:*头行的内容。

- `%l`远程登录名（如果提供了*identd*）。

- `%(NOTE)n`来自其他模块的注释*NOTE*的内容。

- `%(HEADER)o`回复中*HEADER:*头行的内容。

- `%p`提供请求的服务器规范端口。

- `%P`处理请求的子进程ID。

- `%r`请求的第一行。

- `%s`内部重定向请求的原始请求状态。对于最后一个请求的状态，使用`%s`。

- `%t`时间，采用通用日志格式时间格式。

- `%(format)t`时间，形式由*format*给出，应采用*strftime(3)*格式。

- `%T`处理请求所花的时间，以秒为单位。

- `%u`来自*auth*的远程用户；如果返回状态（`%s`）为401，则可能是虚假的。

- `%U`请求的URL路径。

- `%v`提供请求的服务器的规范服务器名称。

在每个变量中，你可以在变量前面添加一个条件，以决定是否显示该变量。如果不显示，则会显示`·`。这些条件的形式是数值返回值的列表。例如，`%401u`将显示*REMOTE_USER*的值，除非返回代码是401。

然后可以使用*CustomLog*指令指定日志文件的位置和格式：

```
CustomLog /var/log/httpd/apache/access_log common
```

如果未指定为绝对路径，则假设日志文件的位置相对于*ServerRoot*。

## CGI 和 SSI

在网站上提供动态内容最常见的方法是使用CGI（通用网关接口）程序。CGI是服务器进程（如生成动态文档的程序）与服务器本身之间通信的规范。服务器端包含（SSI）允许将CGI程序或其他程序的输出插入到现有的HTML页面中。

### CGI

默认情况下，你可以将任何CGI程序放在服务器的*ScriptAlias*目录中。这些程序必须由运行服务器的用户可执行。这通常意味着你需要将文件的模式更改为755，这样除了用户以外没有人可以执行它们。

```
chmod 755 program.cgi
```

为了在*ScriptAlias*目录之外执行CGI程序，你需要为该目录启用*ExecCGI*选项。这可以在你的`access.conf`文件或该目录中的`.htaccess`文件中完成。

CGI程序可以用任何语言编写。最流行的CGI编程语言是Perl和C。由于本书不是关于CGI的书，你可能需要找一本好的CGI编程书，例如*《CGI Programming with Perl, Second Edition》*。

为了测试你是否正确配置了CGI，请尝试以下用Perl编写的CGI程序，它显示HTTP环境变量的值。

```
#!/usr/bin/perl
print "Content-type: text/html\n\n";
print "<html><head><title>Simple CGI program</title></head><body>\n";
for (keys %ENV) {
    print "$_ = $ENV{$_}<br>\n";
}
print "</body></html>\n";
```

如果你打算用Perl编写CGI程序，你可能需要查看随Perl捆绑的CGI模块。

### SSI

服务器端包含是直接写入HTML页面的指令，服务器在向Web客户端提供页面时解析这些指令。它们可用于包含其他文件、程序输出或环境变量。

启用SSI（Server-Side Includes，服务器端包含）最常见的方式是指示服务器在提供具有特定文件名扩展名（通常是`.shtml`）的文件时对其进行解析。这可以通过在`srvm.conf`文件中取消以下行的注释来实现：

```
#### To use server-parsed HTML files
#### AddType text/html .shtml
#### AddHandler server-parsed .shtml
```

通过取消注释`AddType`和`AddHandler`行，你可以告诉服务器解析所有`.shtml`文件中的SSI指令。

启用SSI较少使用的方式是通过`XBitHack`指令。`XBitHack`可以设置为`on`、`off`或`full`，并可以在服务器配置、每个`<Directory>`、每个`<VirtualHost>`或`.htaccess`文件中设置。如果`XBitHack`指令处于开启状态，则表示所有设置了用户执行位的文件都应被解析以查找SSI指令。这有两个主要优点。其一，你无需仅仅因为想添加少量动态内容就重命名文件并更改指向该文件的所有链接。另一个原因更偏向外观——查看你网页内容的用户无法通过文件名看出你正在动态生成页面——因此你的“魔术”显得略微令人印象深刻。如果`XBitHack`设置为`full`，`Apache`还会测试组执行位。如果该位开启，它将返回包含文件最后修改时间的`Last-Modified`标头；否则，它不会生成`Last-Modified`标头。允许生成`Last-Modified`标头使得数据可以被缓存。

除了这些指令外，对于你希望允许SSI的目录，还必须指定`Options Includes`指令。这可以在服务器的`access.conf`文件或`.htaccess`文件中设置。

#### 基本SSI指令

SSI指令看起来类似于HTML注释标签。语法如下：

```
<!--#element attribute=value attribute=value ... -->
```

`element`可以是以下其中之一：

- `config`: 此指令允许你设置关于如何处理文档解析的各种配置选项。由于页面是从上到下解析的，因此`config`指令应出现在HTML文档的顶部。可以通过此命令设置三种配置：

    - `errormsg`: 允许你设置在解析文档过程中发生错误时返回给客户端的错误消息。这通常是`[an error occurred while processing this directive]`，但你可以通过此指令将其设置为任何内容。

      示例：`<!--#config errormsg='[It's broken, dude]'-->`

    - `sizefmt`: 允许你设置用于显示文件大小的格式。你可以将值设置为`bytes`以显示确切的字节大小，或设置为`abbrev`以KB或MB显示大小。

      示例：`<!--#config sizefmt="bytes"-->`

    - `timefmt`: 允许你设置用于显示时间的格式。该值的格式与C（以及Perl）中用于显示日期的`strftime`函数使用的格式相同，如以下表格所示。

| 格式 | 描述 |

| :--- | :--- |

| `%%` | 百分号 |

| `%a` | 星期缩写 |

| `%A` | 星期 |

| `%b` | 月份缩写 |

| `%B` | 月份 |

| `%c` | ctime格式：Sat Nov 19 21:05:57 1994 |

| `%d` | 月份中的数字日期 |

| `%e` | DD |

| `%D` | MM/DD/YY |

| `%h` | 月份缩写 |

| `%H` | 小时，24小时制，前导0 |

| `%I` | 小时，12小时制，前导0 |

| `%j` | 一年中的第几天 |

| `%k` | 小时 |

| `%l` | 小时，12小时制 |

| `%m` | 月份编号，从1开始 |

| `%M` | 分钟，前导0 |

| `%n` | 换行符 |

| `%o` | 华丽的日期，如 1st, 2nd, 或 25th |

| `%p` | a.m. 或 p.m. |

| `%r` | 时间格式：09:05:57 p.m. |

| `%R` | 时间格式：21:05 |

| `%s` | 秒，前导0 |

| `%t` | Tab |

| `%T` | 时间格式：21:05:57 |

| `%U` | 周数；周日作为每周第一天 |

| `%u` | 星期数字：周日 = 0 |

| `%V` | 周数；周一作为每周第一天 |

| `%x` | 日期格式：11/19/94 |

| `%X` | 时间格式：21:05:57 |

| `%y` | 年份（两位数字） |

| `%Y` | 年份（四位数字） |

| `%z` | 时区ASCII表示，例如 PST |

- `echo`: 显示下列包含变量中的任意一个。时间将按照`timefmt`指定的时间格式显示。要显示的变量通过`var`属性指示。

    - `DATE_GMT`: 格林威治标准时间的当前日期。

    - `DATE_LOCAL`: 本地时区的当前日期。

    - `DOCUMENT_NAME`: 用户请求文档的文件名（不包括目录）。

    - `DOCUMENT_URL`: 用户请求文档的（%-解码）URL路径。注意，在嵌套包含文件的情况下，这不是当前文档的URL。

    - `LAST_MODIFIED`: 用户请求文档的最后修改日期。

- `exec`: 根据提供的参数执行shell命令或CGI程序。有效属性为`cgi`和`cmd`。

    - `cgi`: 要执行的CGI程序的URL。该URL必须是本地CGI，而不是位于另一台机器上的。CGI程序会接收最初传递给请求文档的`QUERY_STRING`和`PATH_INFO`，因此指定的URL不能包含这些信息。你最好使用`include virtual`而不是此指令。

    - `cmd`: 要执行的shell命令。结果将显示在HTML页面上。

- `fsize`: 显示由`file`或`virtual`属性指定的文件的大小。大小将按照`sizefmt`指令指定的方式显示。

    - `file`: 文件的路径（文件系统路径），如果值以`/`开头，则相对于根目录；否则相对于当前目录。

    - `virtual`: 文件的相对URL路径。

- `flastmod`: 显示文件的最后修改日期。所需文件的指定方式与`fsize`指令相同。

- `include`: 包含文件的内容。文件通过`file`和`virtual`属性指定，方式与`fsize`和`flastmod`相同。如果指定的是CGI程序且未设置`IncludesNoExec`，则该程序将被执行并显示结果。应优先使用此指令而非`exec`指令。你可以使用此指令传递`QUERY_STRING`，而这是`exec`指令无法做到的。

- `printenv`: 显示所有现有变量。没有属性。

    - 示例：`<!--#printenv -->`
