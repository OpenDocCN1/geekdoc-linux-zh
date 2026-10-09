
AuthName "Apache Server Bible Readers Only"
AuthType Basic
AuthUserDBFile /www/secrets/myuserdbm
require valid-user

此时，Apache 使用 `mod_auth_dbm` 模块在此配置适用的目录中进行身份验证。

> **注意** 请确保只有 Apache 和文件所有者可以读取 DBM 文件。除 DBM 文件的所有者外，任何人都不应能够写入该文件。

### mod_auth_db

如果你的系统不支持使用 DBM，但可以使用 Berkeley DB 文件支持，你可以使用 `mod_auth_db` 来代替 DBM 模块使用 DB 文件进行 Apache 的身份验证。该模块在标准的 Apache 发行版中并未被编译包含。

在配置基于 DB 文件的身份验证模块之前，请确保你知道系统中 DB 库文件存储的位置。例如，在 Linux 系统中，这些文件位于标准的 `/usr/lib` 目录中。如果你的系统没有 DB 库，你将需要获取源代码并首先编译 DB 支持。你可以在 www.sleepycat.com 找到 DB 库的信息。

确认你的系统具有 DB 库后，你可以继续重新配置并重编译 Apache。使用 `configure` 脚本中的 `--enable-db` 选项为 Apache 源代码配置 Berkeley DB 支持，然后像平常一样编译和安装 Apache。

此时，你已准备好使用 `mod_auth_db` 模块。该 `mod_auth_db` 模块提供了 `AuthDBUserFile`、`AuthDBGroupFile` 和 `AuthDBAuthorize` 指令。

#### AuthDBUserFile

`AuthDBUserFile` 指令设置包含用户列表和加密密码的用户 DB 文件的完全限定路径名。

- **语法**：AuthDBUserFile *filename*
- **上下文**：Directory, per-directory access control file (`.htaccess`)
- **覆盖权限**：AuthConfig

与其 DBM 对应项类似，DB 用户文件也使用用户名作为键，而值则是经过 `crypt()` 加密的密码。

> **注意** 务必确保用户文件位于 Web 文档树之外，并且只有 Apache 可以读取。除所有者（即 Apache）外，任何人都不应拥有这些文件的写入权限。

#### AuthDBGroupFile

AuthDBGroupFile 指令设置组 DB 文件的完全限定路径名，该文件包含用于用户身份验证的用户组列表。与其 DBM 对应项类似，组文件使用用户名作为键，逗号分隔的组列表被视为值。值内部不能包含任何空白字符，且绝不应包含冒号。

- **语法**：AuthDBGroupFile *filename*
- **上下文**：Directory, per-directory access control file (.htaccess)
- **覆盖权限**：AuthConfig

如果你不希望使用单独的组文件，可以使用单个 DB 文件同时提供密码和组信息。该文件的格式为：

DB_File_Key(username) - encrypted_password; comma_separated_group_list

其中用户名是键，而密码和组列表是值的两个字段。在另一个冒号之后可以在 DB 文件中保留其他数据；身份验证模块会忽略这些数据。如果你使用单个 DB 文件同时提供组和密码信息，你必须将 AuthDBGroup 和 AuthDBUserFile 指令都指向同一个文件。

#### AuthDBAuthoritative

当在同一目录中使用多种身份验证方案（如 mod_db、mod_dbm 和标准 mod_auth）时，你可以使用 AuthDBAuthoritative 指令来定义 mod_auth_db 是否为权威身份验证方案。该指令的默认值使 mod_auth_db 成为该目录的权威身份验证方案。因此，如果基于 DB 的身份验证对特定用户失败，该用户的凭证不会传递给较低层级的身份验证方案。当设置为 Off 值时，身份验证失败的凭证会传递给下一个身份验证层级。

- **语法**：AuthDBAuthoritative On | Off
- **默认设置**：AuthDBAuthoritative On
- **上下文**：Directory, per-directory access control file (.htaccess)
- **覆盖权限**：AuthConfig

## 动态内容生成模块

此处讨论的模块使 Apache 能够运行 CGI 脚本、SSI、过滤器等。表 5-4 列出了这些模块。

**表 5-4**
**动态内容生成模块**

| 模块 | 用途 |
| :--- | :--- |
| *mod_cgi* | 运行 CGI 脚本。详细信息请参见第 12 章。 |
| *mod_include* | SSI 过滤器。详细信息请参见第 13 章。 |
| *mod_actions* | 基于媒体类型或请求方法执行 CGI 脚本。 |
| *mod_ext_filter* | 使用外部程序过滤输出。 |

### mod_actions

`mod_actions` 模块默认被编译。`mod_actions` 允许你基于 `MIME-type` 或 HTTP 请求方法运行 CGI 脚本。它提供以下指令。

#### Action

`Action` 指令允许你为特定的 MIME 类型关联一个操作。该操作通常是处理所请求文件的 CGI 脚本。这允许你为给定的 MIME 类型执行 CGI 脚本。

- **语法**：`Action` *MIME-type* *cgi_script*
- **上下文**：Server config, virtual host, directory, per-directory access control file (`.htaccess`)
- **覆盖权限**：`FileInfo`

例如，以下指令使 Apache 在请求 HTML 文件时始终运行指定的脚本：

```
Action text/html /cgi-bin/somescript.pl
```

该脚本通过标准环境变量 `CGI_PATH_INFO` 和 `PATH_TRANSLATED` 接收所请求文档的 URL 和文件路径。这在开发过滤脚本时很有用。本节讨论其中一个这样的过滤脚本。

当通过 Web 请求文本文件（`.txt`）时，它在 Web 浏览器上的显示格式并不理想，因为大多数 Web 浏览器不会以任何方式转换换行符。通常，大多数文本文件显示为一个大的段落。通过使用 `Action` 指令，你可以开发更好的解决方案。

举一个更有趣的例子，假设你现在想要开发一个解决方案，不仅要在 Web 浏览器上更好地显示文本文件，还要在每个文本文件的末尾插入版权声明。为了实现这一点，你需要做两件事。首先，在 httpd.conf 文件中添加以下指令：

```
Action plain/text /cgi-bin/textfilter.pl
```

然后，开发 Perl 脚本 textfilter，该脚本将以你希望的方式显示文本文件。列表 5-1 显示了这样一个脚本。你可以在随附 CD-ROM 的 Scripts/Chapter 5 目录中找到此脚本。

#### 列表 5-1：textfilter.pl

```perl
#!/usr/bin/perl
#
# Script: textfilter.pl
#
# Purpose: This filter script converts plain text files
#         into an HTML document but keeps the text layout
#         as is.
#
# Copyright (c) 2001 by Mohammed J. Kabir
#
# License: GPL
#
# The copyright message file is always stored in
# the server's document root
# directory and is called copyright.html.
my $copyright_file = $ENV{DOCUMENT_ROOT} . "/copyright.html";
# Get the requested document's path
my $path_translated = $ENV{PATH_TRANSLATED};

# Other variables needed for storing data
my $line;
my @text;
my @html;

# Store the path info and the file name of requested doc in an
array
@filename = split(/\/\/.{$path_translated};

# Because HTML tags are used to display the text file,
# lets print the text/html content header.
print "Content-type: text/html\n\n";

# Read the document requested and store the data
# in @text array variable
@text = &readFile($path_translated);
# Now print the following HTML document tags.
# These tags will be sent before the actual document content
#
print <<HEAD;
<HTML>
<HEAD><TITLE>$filename[-1] </TITLE> </HEAD>
<BODY BGCOLOR="white">
<BLOCKQUOTE>
<PRE>
HEAD
# Now print each line stored in the @text array
# (that is, the content of the document requested)
#
foreach $line (@text) { print $line; }
# Now read the copyright file and store the content
# in the @html array variable
#
@html = &readFile($copyright_file);
# Print each line stored in the @html array (that is,
# the content of the copyright message file)
#
foreach $line (@html){ print $line; }
# Exit the filter
exit 0;

sub readFile {
#
# Subroutine: readFile
# Purpose: Reads a file if it exists or else prints
# an error message and exits script
#
# Get the name of the passed file name and store
# it in variable $file
my $file = shift;
# Local buffer variable
my @buffer;
# If the file exists, open it and read all the
# lines into the @buffer array variable
if(-e $file) {
open(FP,$file) || die "Can not open $file:";
while(<FP>){
```

