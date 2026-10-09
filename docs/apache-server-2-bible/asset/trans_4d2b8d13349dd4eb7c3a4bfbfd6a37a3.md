
## 使用 makesite 脚本生成虚拟主机配置

**使用 makesite 脚本**

如果您为 ISP 或大型组织工作，且市场部经常创建新的产品网站，导致添加虚拟主机成为每日或每周的常规任务，那么您需要 `makesite`。这是一个我多年前编写的简单 Perl 脚本，我至今仍在用它来创建新的虚拟主机。该脚本随 CD-ROM 提供，也可以从 http://sourceforge.net/projects/mkweb/ 下载。

例如，要创建一个新的名为 `newsite.com` 的虚拟主机，您只需运行 `makesite newsite.com`，该脚本就会创建并追加必要的 `httpd.conf` 配置。它还会通过两个模板文件创建必要的 DNS 配置文件。要使用 `makesite`，请遵循以下步骤：

1. 将 `makesite` 脚本、`named.template` 和 `httpd.template` 文件复制到服务器上的合适位置。我通常将 `makesite` 放在 `/usr/bin` 目录中，使其位于常规路径下。我建议创建 `/var/makesite` 目录，并将 `named.template` 和 `httpd.template` 文件移动到该目录中。在以下步骤中，我假设您将执行相同的操作。

2. 使用您喜欢的文本编辑器修改 `makesite` 脚本。您需要修改以下一行或多行：

```perl
my $MAKESITE_DIR = '/var/makesite';
my $USER = 'httpd';
my $GROUP = 'httpd';
my $PERMISSION = '2770';
my $BASE_DIR = '/www';
my $HTDOCS = '/htdocs';
my $CGIBIN = '/cgi-bin';
my $NAMED_PATH = '/var/named';
my $NAMED_FILE_EXT = '.zone';
my $NAMED_TEMPLATE = "${MAKESITE_DIR}/named.template";
my $NAMED_CONF     = '/etc/named.conf';
my $HTTPD_CONF     = '/usr/local/apache/conf/httpd.conf';
my $VHOST_TEMPLATE = "${MAKESITE_DIR}/httpd.template";
my $LOG_FILE       = "${BASE_DIR}/makesite.log";
```

您可能需要按以下方式进行修改：

- 如果您遵循了我的建议并创建了存放 `named.template` 和 `httpd.template` 的 `/var/makesite` 目录，则无需更改 `${MAKESITE_DIR}`。
- 如果您使用不同于 `httpd` 的用户/组来运行 Apache，请更改 `${USER}` 和 `${GROUP}` 的值。如果希望默认 Web 目录权限不是 `2770`，请更改 `${PERMISSION}` 的值。
- `${BASE_DIR}` 设置为 `/www`，这是虚拟主机站点目录的创建位置。虚拟主机站点目录将为 `/www/ virtual_hostname`，其下将有 `htdocs`（由 `${HTDOCS}` 设置）和 `cgi-bin`（由 `${CGIBIN}` 设置）子目录。根据需要更改这些值。
- 如果您希望文档根目录不是 `htdocs`，请更改 `${HTDOCS}`。
- 类似地，如果您不使用传统的 `/cgi-bin/` 别名作为 `ScriptAlias`，请相应更改 `${CGIBIN}`。
- 在 Linux 系统上，默认的 DNS 记录目录是 `/var/named`；如果您已将其更改为其他路径，请确保更改 `${NAMED_PATH}`。
- 如果您将 `httpd.conf` 保存在不同于 `/usr/local/apache` 的路径下，请更改 `${HTTPD_CONF}` 的值。

3. 修改 `/var/makesite/named.template` 文件，使其反映您系统的主名称服务器和 Web 服务器主机名。默认的 `named.template` 文件假设您的主名称服务器和从名称服务器分别为 `ns1.domain.com` 和 `ns2.domain.com`；您的邮件服务器为 `mail.domain.com`；您的 Web 服务器为 `www.domain.com`。请确保相应更改这些主机名。

4. 确保 `/var/makesite/httpd.template` 包含您想要通过此脚本添加到每个新虚拟主机中的所有指令。

现在，您已准备好运行脚本来创建新的虚拟主机。作为预防措施，请备份您的 `/etc/named.conf` 和 `/usr/local/apache/httpd.conf` 文件。要创建名为 `vhost1.com` 的新虚拟主机，请运行 `makesite vhost1.com` 命令。查看 `/usr/local/httpd.conf` 文件；您应该会看到：
