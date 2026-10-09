
# Apache 配置文件

Apache 的配置文件信息包含在一组特定的配置文件中：

- `/etc/httpd/httpd.conf` 文件是 Apache 的主配置文件。
- `/etc/httpd/conf.d` 目录包含所有已安装模块（如 PHP、SSL 等）的配置文件。
- `/etc/httpd/logs` 目录是一个指向 `/var/log/httpd` 目录的符号链接，其中包含所有的 Apache 日志文件。
- `/etc/httpd/modules` 目录是一个指向 `/usr/lib/httpd/modules` 目录的符号链接，其中包含所有配置为动态共享对象的 Apache 模块。

动态共享对象（或称 DSO）是独立于 Apache `httpd` 二进制文件编译的模块。之所以这样称呼它们，是因为它们可以按需加载。关于 DSO 的更多信息请访问 [http://httpd.apache.org/docs-2.0/mod](http://httpd.apache.org/docs-2.0/mod)。

- `/etc/httpd/run` 目录是一个指向 `/var/run` 的符号链接，其中包含 `httpd` 进程的程序 ID 文件（`httpd.pid`）。
- `/etc/rc.d/init.d/httpd` 是一个 shell 脚本，用于启动和停止 Apache Web 服务器。

## 首次启动 Apache

您可以使用 Red Hat 服务配置 GUI 对话框或通过命令行来启动 Apache。以下是从服务配置对话框启动 Apache 的方法：

- 首先，您需要打开 GUI。为此，请单击 **主菜单 | 系统设置 | 服务器设置 | 服务**，或者在命令行中输入以下内容：

```bash
$ redhat-config-services
```

如果您是以普通用户身份启动的，系统会要求输入 root 密码。这样做后，您将看到服务配置对话框：

![](img/b852150740856958b10aff9e8c9d2adc_351_0.png)

该对话框包含您的计算机支持的所有服务列表。复选框指示哪些服务在机器启动时会自动运行（作为 *cron* 任务的一部分）。此外，还有 **启动**、**停止** 和 **重启** 按钮，以便我们可以手动启动和停止服务。

- 滚动对话框左侧的列表，并选择 **httpd** 条目。正如我们所提到的，`httpd` 服务是 Apache Web 服务器服务。查看对话框右下角的 `httpd` 服务状态；如果它是 **已停止** 的（如上所示），请单击 **启动** 按钮来启动它。

如果您希望下次重启机器时它自动启动，请也勾选复选框。然后选择 **文件 | 保存更改** 以保存新设置。这样就完成了；您可以通过选择 **文件 | 退出** 来关闭 **服务配置** 对话框。

要从命令行控制 Apache Web 服务器，我们可以使用 **service** 命令来运行 **httpd** 脚本。以下是我们如何使用它来启动 Web 服务器：

```bash
# service httpd start
Starting httpd:                                     [ OK ]
```

如果在启动 Web 服务器时遇到困难，您将在这里得到通知。例如，如果您尝试在未经 root 权限的情况下执行此操作，您将收到一条消息，告知您权限被拒绝。这是另一个示例：

```bash
# service httpd start
Starting httpd: httpd: Could not determine the server's fully qualified
domain name, using 192.168.0.99 for ServerName
                                                         [ OK ]
```

在这里，消息解释说无法确定服务器的完全限定域名（FQDN），并且它正在使用 IP 地址（192.168.0.99）代替。如果您看到此消息，是因为您既没有为 Linux 服务器设置 FQDN，也没有在 **httpd.conf** 配置文件中配置 *ServerName* 配置指令。

> FQDN 是一个唯一的名称，由主机名和域名组成，可以解析为 IP 地址。例如，www.linux4biz.net 是一个完全限定域名。

回到 **httpd** 脚本本身，有类似的开关用于停止或重启服务：

```bash
# service httpd restart
Stopping httpd:                                    [ OK ]
Starting httpd:                                    [ OK ]
# service httpd stop
Stopping httpd:                                    [ OK ]
```

您可以与 `httpd` 脚本一起使用的其他选项也有一些。如果您在没有选项的情况下运行脚本，生成的用法信息将显示所有可用的选项：

```bash
# service httpd
Usage: httpd
{start|stop|restart|condrestart|reload|status|fullstatus|graceful|
help|configtest}
```

`configtest` 选项特别有用。配置文件相当复杂，因此在对其做出更改后检查错误是很有用的。为此，您使用 `configtest` 选项：

```bash
# service httpd configtest
Syntax OK
```

# 测试 Apache Web 服务器

一旦您启动了 Apache Web 服务器，就应该对其进行测试以查看其是否正常工作。为了做到这一点，我们将使用 Web 浏览器从我们的服务器请求一个网页！默认提供了一个页面用于此目的，您可以通过 URL `http://localhost` 请求它。因此，启动一个 Web 浏览器（**主菜单 | 互联网 | Mozilla Web 浏览器**），并将此 URL 输入到地址框中：

![](img/b852150740856958b10aff9e8c9d2adc_353_0.png)

# 配置您的 Web 服务器

配置您的 Web 服务器是个好主意。Red Hat 确实提供了一个 GUI 工具 `apacheconf` 用于配置 Apache，但它对配置文件的格式化并不好。Webmin（[http://www.webmin.com](http://www.webmin.com) – 见第 13 章）是一种替代的基于 Web 的软件，可用于管理大多数 Linux 服务，包括 Apache Web 服务器。然而，在本节中，我们将向您展示如何通过直接编辑 `httpd.conf` Apache 配置文件来进行一些基本配置。

## 试一试 配置您的 Web 服务器

我们将通过调整几个设置以适应我们的需求来配置 Web 服务器。

1. 启动 gedit 文本编辑器（通过选择 **主菜单 | 附件 | 文本编辑器**），或您喜欢的文本编辑器。使用它打开文件 `/etc/httpd/conf/httpd.conf`。

2. 选择 **搜索 | 查找**，并使用生成的对话框在文件中查找单词 `ServerAdmin`。第一次出现应该是 `ServerAdmin` 指令，其外观如下：

```text
# ServerAdmin: Your server address, where problems with the server should be
# e-mailed. This address appears on some server-generated pages, such
# as error documents. e.g. admin@your-domain.com
ServerAdmin root@localhost
```

如您所见，配置文件对此指令描述得非常清楚。将电子邮件地址更改为您的电子邮件地址，或您为网站管理设置的地址。例如：

```text
# ServerAdmin: Your server address, where problems with the server should be
# e-mailed. This address appears on some server-generated pages, such
# as error documents. e.g. admin@your-domain.com
ServerAdmin webmaster@linux4biz.net
```

3. 现在使用相同的技术查找 `ServerName` 指令（您可能会发现它紧跟在 `ServerAdmin` 指令之后）。首先通过删除前导 # 字符来更改此指令。然后，如果您有注册的 DNS 名称，请在此处添加它（此处我用 `test.linux4biz.net` 作为 DNS 名称进行演示，请替换为您自己的）：

```text
# ServerName gives the name and port that the server uses to identify itself.
# ...
ServerName test.linux4biz.net
```
