
<IfDefine HAVE_PERL>

LoadModule perl_module modules/libperl.so

</IfDefine>

```
在第一个条目中，检查 `HAVE_PERL` 参数是否设置。如果是，`LoadModule` 命令将加载 `modules/libperl.so` 模块，这对解释 Perl 脚本是必要的。

下一个指令块添加模块：
```
<IfDefine HAVE_PERL>

AddModule mod_perl.c

</IfDefine>
```
默认情况下，加载所有安装的模块或发行版包含的模块。但这不是高效的安排，因为发行版开发者无法知道特定用户需要哪些模块。可以加载以下主要的脚本支持模块：

- `perl_module` — Perl
- `php_module` — PHP
- `php3_module` — PHP 版本 3
- `php4_module` — PHP 版本 4
- `python_module` — Python

这些模块对 Web 服务器构成了最大的危险，因为它们允许执行脚本，而脚本可以被用来执行入侵攻击。例如，黑客可以利用 PHP 脚本中的漏洞在服务器上执行命令。设计良好的网站仅使用支持相应语言所需的单个 Web 模块。

我建议使用 PHP 编写网页；这种语言在配置上非常灵活，并提供理想的安全性。我的经验让我相信黑客更倾向于使用 Perl 创建 rootkit（rootkit 是一种允许执行命令并覆盖黑客在受损机器上踪迹的工具集）。但这仅是我的观点。一个胜任的 Perl 程序员可以轻松编写出既安全又难以破解的程序。检查已加载的模块，删除或注释掉那些不需要的模块。这将服务器的安全性提高 50%。

## 7.3. Access Rights

在本节中，我将向你介绍 `/etc/httpd/conf/httpd` 配置文件的主要参数。这些参数指定了目录的访问权限，格式如下：

```
<Directory /var/www/html>

Order allow

Allow all

</Directory>
```

它们也可能类似于：
```
<Location /server-status>

SetHandler server-status

Order deny, allow

Deny from all

Allow from .domain

</Location>
```

第一个代码块设置磁盘上特定目录的权限（在此例中为 `/var/www/html` 目录）；第二个代码块限制虚拟目录权限（在本例中为 `/server-status` ）。如果你熟悉 HTML，应该已经理解了前面的声明。对于没有这些知识的人，我将为目录提供一些解释。
声明代码从以下行开始：
```
<Directory Path>
```
在角括号中，指定关键字 `Directory`，随后是要设置权限的目录路径。随后是定义权限的命令。块结束于：
```
</Directory>
```
