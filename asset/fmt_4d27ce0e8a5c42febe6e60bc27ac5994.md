
在此示例中，`$1`引用`important\.docs`。可以使用多个引用，通过将`$1`更改为`$N`，其中`N`代表第`N`个引用。同样支持的通配符有`(.)` `(*)`和`(+)`。点仅匹配一个字符，星号匹配零或多个字符，加号匹配一个或多个字符。

附加到`RewriteRule`指令的某些标志见表 VIII.2。

## 表 VIII.2 RewriteRule 标志

| 标志 | 描述 |
| :--- | :--- |
| F | 返回 http 403 forbidden（禁止）错误 |
| G | 返回 http 410 gone（已失效）错误 |
| P | 通过`ProxyPass`指令对替换执行内部代理请求 |
| R | 执行外部重定向 |
| NC | 匹配时不区分大小写 |
| C | 将当前规则与下一条规则链联 |
| L | 不应用任何后续重写规则 |

`RewriteCond`也常用于在执行`RewriteRule`指令之前测试条件，类似于编程中的`if`语句。`RewriteCond`的语法如下：

```
RewriteCond testpattern condpattern [flags]
```

其中`testpattern`会与`condpattern`进行比对检查，`flags`是可选的修饰符。这可以通过语句“如果 test-pattern 匹配 condpattern，则执行后续代码”来记忆。`RewriteRule`的语法包括对服务器变量的使用（指定为`%{variable}`）以及对圆括号内分组文本的反向引用，用法与`RewriteRule`相同。

`RewriteCond`支持的一些服务器变量有：

| REMOTE_ADDR | DOCUMENT_HOST | DOCUMENT_ROOT |
| :--- | :--- | :--- |
| SERVER_NAME | SERVER_USER | SERVER_PORT | SERVER_PROTOCOL |
| TIME_YEAR | TIME_MON | TIME_DAY | TIME_HOUR | TIME_MIN | TIME_SEC |
| HTTP_USER_AGENT | HTTP_REFERER | HTTP_HOST | HTTP_ACCEPT |

完整列表可以在 Apache 网站上的`RewriteCond`文档中找到：`http://httpd.apache.org/docs/mod_rewrite.html`。

## RewriteCond 的基本示例如下：

```
RewriteCond %REMOTE_HOST ^theserver.com

RewriteRule /$ /server.html
```

只有当变量`REMOTE_HOST`匹配`theserver.com`时，才会会将所有内容重写到`DocumentRoot//server.html`。

此外，`RewriteCond`支持两个可选标志：`[OR]`和`[NC]`。`[OR]`用于测试多个条件，而`[NC]`用于禁用`testpattern`和`condpattern`的大小敏感性。例如：

```
RewriteCond %REMOTE_HOST 192.168.3.14 [OR]

RewriteCond %REMOTE_HOST ^thatserver.com [NC]

RewriteRule /$ /server.html
```

将匹配主机`192.168.3.14`、`thatserver.com`或`That-SERVER.com`。

关于构建正则表达式的额外帮助，请查阅`regex`手册页。

## 实验练习

在本实验中，假设用户已运行 Apache 并安装了`mod_rewrite`。将使用`mod_rewrite`为两种不同情况重写 URL：从一个服务器重定向到新服务器，以及根据访问服务器时使用的 Web 浏览器将用户重定向到特定的浏览器页面。

使用`RewriteRule`指令，在`httpd.conf`中添加一行，将用户从`http://oldserver/~theuser/somepath`重定向到`http://newserver/~theuser/somepath`。

使用`RewriteCond`条件语句，搜索用户的客户端类型，然后使用`RewriteRule`将用户重定向到特定客户端的页面。

1. 在文本编辑器中打开`httpd.conf`。
2. 使用`mod_rewrite`将主目录从一个位置重定向到另一个位置。
3. 使用`mod_rewrite`将所有到`/theuser/somepath/`的 URL 重定向到`http://newerver/~the/somepath/`，如下如下：

```
RewriteEngine On

RewriteRule ^/(.+)$ http://newerver/~$1 [R,L]
```
4. 基于客户端使用`RewriteCond`。

```
RewriteCond %{HTTP_USER_AGENT} "Mozilla/3.*"

RewriteRule ^foo.html$ foo.NS.html [L]

RewriteCond %{HTTP_USER_AGENT} "Lynx/" [OR]

RewriteCond %{HTTP_USER_AGENT} "Mozilla/[12]."

RewriteRule ^foo.html$ foo.20.html [L]

RewriteRule ^foo_html32.html [L]
```
