
![](img/a6a91935f07f13d62210d3016f91c5fc_41_1.png)

安装后，配置 `SuExec` 的关键是设置虚拟主机允许 Apache 在与运行原始用户的 Web 服务器上运行 CGI 和 SSL 文件的系统。通常，这些程序与 Web 服务器相同的用户运行（例如某些发行版中的 `www-data`）。`SuExec` 可以减少多户环境下用户运行自己的 CGI 脚本时发生的安全风险。请记住脚本必须是可执行的——很多人经常忽略这一点，并会导致错误。

## 01 设置 LAMP 栈

为了配置 `SuExec`，请确保你已安装 LAMP 栈。你可以通过在 `/var/www` 中创建一个 `php` 文件来验证 Apache 和 `PHP` 的运行。如果渲染正确，则在浏览器中加载该文件。如果你看到文件的内容，可能是 `libapache2-mod-php` 软件包有问题。这是一个常见的疏忽：Apache 实现了本文引用的站点。

| 特性 | 值 |
| :--- | :--- |
| 系统 | Linux x86_64 4.6.0-ubuntu |
| 构建日期 | 2017年2月16 11:52 |
| 服务器 API | Core |
| 虚拟目录 | enabled |
| 加载配置 | `/etc/php/7.1/cli.ini` |
| 额外文件扫描目录 | `/etc/php/7.1/conf.d` |
| 额外文件 | 7.1.3-deb |

## 02 启用 cgi 模块

要在 Apache 中使用 CGI，首先需要启用相应的模块。浏览 `modules-enabled` 目录（通常为 `/etc/apache2/mods-enabled`）下的 Apache 配置，并使用 `LoadModule cgi_module /usr/apache2/modules/mod_cgi.so` 指令启用它。如果没有该文件，说明我们使用一个允许配置运行目录的修改模块。我们看到所需的目录是 `/usr/lib/cgi-bin`，因此创建一个内容的测试文件：

```bash
#!/usr/bin/perl
print "Content-type: text/html\n";
print "Hello, World!\n";
```

这里的 `header` 特别重要，因为它告诉浏览器如何解释我们发送的数据。Web 服务器应该无任何警告地重启，你现在应该能够在启用的模式中看到该文件。使用 `a2enmod suexec` 命令显示单个模块，然后通过 `service apache restart` 重启 Apache。

```bash
sudo service apache restart
```

![](img/a6a91935f07f13d62210d3016f91c5fc_42_0.png)

Hello, World.

```apache
## Module mod_cgi_conf
LoadModule cgi_module modules/libapache2_mod_cgi.so
## ...
```

## 03 检查默认虚拟主机

假设你使用的是 Apache 的基础安装，“默认虚拟主机”将通过 `/etc/apache2/sites-available/000-default.conf` 文件进行配置。如果你打开它，将发现没有启用 CGI 选项。这是因为系统没有提供 CGI 内容——它是通过这种方式被专门启用的。关键行是配置 `ScriptAlias`，你的网站上设置 `ScriptAlias /cgi-bin/` 将映射到 `/usr/lib/cgi-bin/`。由于 `+Execgi`，执行被启用。

```apache
ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
+Execgi
```

![](img/a6a91935f07f13d62210d3016f91c5fc_42_1.png)

## Apache SuExec

> `SuExec` 通过擦除服务器配置中标记为安全以外的所有环境变量来清理环境

![](img/a6a91935f07f13d62210d3016f91c5fc_43_0.png)

如果模块已安装，当你尝试重新加载 CGI 脚本时会遇到 500 错误——这是由于 `SuExec` 实施的安全措施。别担心，这很容易解决。

使用命令 `sudo mkdir /home/scripter/scripts` 创建一个合适的地方——`SuExec` 对谁有权在目录中写入和执行非常严格，因此我们可以通过 `sudo chown scripter:scripter /home/scripter/scripts` 传输所有权和正确的权限，以及 `sudo chmod 700 /home/scripter/scripts`——我们的用户 `scripter` 将能够写入该目录。

## 08 创建新用户

流程的下一步是创建一个新用户，该用户将执行我们的 CGI 脚本。如果你有多个站点，每个用户都可以有自己的家目录，

```bash
$ useradd -m -d /home/scripter scripter
Adding new user: 'scripter' with group 'scripter'
Creating home directory: '/home/scripter'
Copying files from '/etc/skel' to '/home/scripter'
passed password ownership successfully
$ chown scripter:scripter /home/scripter
$ chmod 755 /home/scripter
```

## 10 创建并复制新脚本

我们将创建一个新脚本，但首先我们需要确保它在我们新用户下可以正常工作，因此我们使用 `sudo touch /home/scripter/scripts/test.pl`。

将以下内容粘贴到我们用于定义解释器的文件中 `"Content-type: text/html\n<html><head></head>\n<body>print(\"Hello World!\");</</body></body></html>"` 中，以输出内容。当我们在接下来的步骤中测试脚本时，它的运行方式将与完全一样。

```bash
$ touch /home/scripter/scripts/test.pl
$ chmod 700 /home/scripter/scripts/test.pl
$ chown scripter:scripter /home/scripter/scripts/test.pl
```

并使用。在每个提示信息处按回车键——我没有显式地以用户身份登录，所以没关系。设置用户将自动创建相应的家目录，我们将在下一步中使用它。

```bash
$ su -s scripter -d /home/scripter /home/scripter/scripts/test.pl
```

## 11 变为可执行

现在我们已经测试了脚本，我们需要它是可执行的。我们还需要确保我们的新 `scripter` 是拥有该文件权限的人。为了做到，我们需要使用命令 `chmod 700 /home/scripter/scripts/test.pl`。我们现在将在 `web-data` 用户家目录中设置一切，这样此脚本才能通过 `SuExec` 正确运行。

## 09 创建新的脚本目录

我们将从新用户的家目录存储并运行脚本，

## 12 使用脚本目录更新虚拟主机

由于我们更改了脚本目录的位置，我们需要更新虚拟主机文件——例如，编辑默认虚拟主机文件 `/etc/apache2/sites-enabled/000-default`，并将 `ScriptAlias` 更改为 `/home/user/scripts/`。`ScriptAlias` 命令实际上需要 `Options +ExecCGI` 选项，这只有在重启 `apache` 时才严格需要。

```apache
<Module module_cgi.so>
  LoadModule cgi_module /usr/lib/apache2/modules/mod_cgi.so
</Module>
<Module module_env.so>
  LoadModule env_module /usr/lib/apache2/modules/mod_env.so
</Module>
<Module module_rewrite.so>
  LoadModule rewrite_module /usr/lib/apache2/modules/mod_rewrite.so
</Module>
<Module module_proxy.so>
  LoadModule proxy_module /usr/lib/apache2/modules/mod_proxy.so
</Module>
```

## 13 在虚拟主机中设置用户
