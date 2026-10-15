
# apt-get install apache

在配置过程中，系统会询问你是否想要启用 `suexec` 机制。`suexec` 特性增加了 CGI 的安全性，通常建议启用。你稍后可以使用 `debconf` 重新配置 `apache` 包。有关 `debconf` 的更多信息可以在第 9 章中找到。

# 第 23 章 ♦ 运行 Linux, Apache, MySQL 和 PHP (服务器) 599

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_629_0.png)

此安装过程安装的是 Apache 1.3 版本，这里的所有的配置示例都已在该版本上通过测试。如果你想安装 Apache 2.0，它可以在 `apache2-mpm-prefork` 包中找到，并使用 `libapache2-mod-php4` 代替本章后面提到的 `php4` 包。

安装完成后，服务器应该会自动启动，这意味着你现在已经准备好安装 PHP 了。

## 安装 PHP

现在你已经准备好在 Apache 中安装并测试 PHP 模块了。这是安装 PHP 的常用方法，但在多用户系统上会引入一些安全问题，因为所有 PHP 脚本将以与 Apache 守护进程相同的用户运行。在允许其他用户访问操作服务器上的 PHP 文件之前，请务必阅读 http://php.net/manual/en/security.php 获取 PHP 手册安全章节。

Apache 模块包含在 `php4` 包中，通过 APT 安装。以下行下载并安装该模块以及 mysql 扩展，配置 Apache 自动加载该模块，并指示 Apache 重新加载配置：

```bash
# apt install php4 php4 mysql
@ apache-modconf apache enable mod_php4
正在用新版本替换文件 /etc/apache/modules.conf
@ apachectl restart
```

如果第二行没有像示例中那样打印出消息，请不要担心。这仅意味着模块已经配置过了。

此时，Apache 应该已经准备好处理 HTTP 请求，包括对 PHP 文件的处理。要测试它，创建一个 `/var/www/info.php` 文件，其中包含对 `phpinfo()` 的调用：

```bash
# cat /var/www/info.php
<?php
phpinfo();
?>
^D
# chmod 644 /var/www/info.php
```

`^D` 命令意味着你应该在键盘上按下 Ctrl-D。这表示输入结束。现在尝试通过访问 `http://你的服务器地址/info.php` 打开该页面。你应该能看到一个关于你的 Apache 和 PHP 安装的完整信息页面，如图 23-1 所示。

# 600 第五部分 ♦ 运行服务器

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_630_0.png)

**图 23-1：** PHP 信息页面。

如果提示你下载文件而不是信息页面，请检查相应的 PHP 安装章节（本章较前的部分）以验证所有步骤是否已成功完成。

在完成所有测试并运行后，可以安全地删除创建的 `info.php` 文件：

```bash
rm -f /var/www/info.php
```
