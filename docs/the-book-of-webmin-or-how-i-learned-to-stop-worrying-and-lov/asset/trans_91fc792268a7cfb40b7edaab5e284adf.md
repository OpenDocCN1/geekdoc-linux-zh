

如果此模块可用，你将在下一行看到仅打印的“Success!”字样。如果模块未安装，则会产生一系列错误。如果模块检查成功，请继续下一节。如果不成功，请访问综合 Perl 档案网络（简称 CPAN）[http://www.cpan.org]。使用搜索功能查找 Authen-PAM 的最新版本，下载它，并按照随附的 README 文件中的说明进行操作。简而言之，所有 CPAN Perl 模块都以相同简单的方式安装。首先通过运行 Makefile.PL 文件生成 makefile，如下所示：

```
[root@grover Authen-PAM-0.13]# perl Makefile.PL
```

如果成功，运行 make 和 make install。

```
[root@grover Authen-PAM-0.13]# make
[root@grover Authen-PAM-0.13]# make install
```

接下来，使用本节开头建议的 Perl 命令来测试模块的可用性。然后在适当位置添加一个名为 usermin 的 PAM 服务。在许多 Linux 发行版中，这涉及创建一个名为 /etc/pam.d/usermin 的文件，其中包含以下内容：

```
#%PAM-1.0
auth       required     pam_unix.so      shadow nullok
account    required     pam_unix.so
password   required     pam_unix.so      shadow nullok use_authtok
session    required     pam_unix.so
```

现在 Usermin 的安装应该会顺利进行。

**NOTE** 你可能能够为你的操作系统下载 Authen-PAM 的软件包，这通常从系统维护的角度来看是更可取的。此外，如果你使用基于 RPM 的 Linux 发行版，你可能能够使用 cpan2rpm 或 cpanflute2 从 Perl 模块自动生成软件包，如果你的厂商没有为你提供软件包。本书中未讨论 cpanflute 的使用。但是，如果你经常安装 Perl 模块，值得研究一下，因为它使生成 Perl 模块 RPM 变得简单而无痛。

## Obtaining Usermin

幸运的是，我们 Usermin 在 BSD 风格许可证下是免费的，就像其功能更强大的兄弟一样。它可以从 Usermin 网站或其镜像站点免费下载。供参考，主要的 Usermin 网站是 [http://www.usermin.com]。与 Webmin 一样，Usermin 以 tarball 的形式提供，以及适用于 Red Hat、MSC Linux、Caldera、Mandrake 和 SuSE 的 RPM。与 Webmin 不同，目前没有 Usermin 的 Solaris 软件包。选择最适合你的系统的选项。

## Installing the Package or Tarball

根据安装方法，你遵循的步骤与安装 Webmin 时类似。对于 tarball，将其复制到所需安装位置（通常为 /usr/local），解压，解包，然后运行 setup.sh 脚本：

```
[root@delilah /root]# cp usermin-0.6.tar.gz /usr/local
[root@delilah /root]# cd /usr/local
[root@delilah local]# gunzip usermin-0.6.tar.gz
[root@delilah local]# tar xf usermin-0.6.tar
[root@delilah local]# cd usermin-0.6
[root@delilah local]# ./setup.sh
```

安装脚本会询问一系列问题，其中大多数应接受默认值。安装脚本运行完成后，你将能够在端口 20000 上登录到 Usermin 服务器。

## Installing Usermin from an RPM

从 RPM 软件包安装，就像 Webmin 一样，比从 tarball 安装更容易。当从软件包安装时，仍然有必要确保你拥有先前记录的 PAM Perl 模块（如你将使用它）。然后使用以下命令进行 RPM 安装：

```
[root@delilah /extra]# rpm -Uvh usermin-0.6-1.noarch.rpm
```

RPM 将自动使用合理的默认值运行安装脚本并启动端口 20000 上的 Usermin 服务器。

## Usermin Configuration

你配置 Usermin，或许具有悖论性，从 Webmin 内部进行。点击 Webmin 选项卡下的 Usermin Configuration 图标会显示几行 Usermin 选项图标，其形式和功能与 Webmin Configuration 模块非常相似（图 4-1）。当然，可配置选项要少得多，但由于 Usermin 基于与 Webmin 相同的 Web 服务器框架（具体为 miniserv.pl），它提供了所有相同的访问控制和安全机制。

## Usermin Module Configuration

首次进入此模块时，显示的只是列出所有具有可配置选项的 Usermin 模块的页面。点击模块名称将打开包含所选模块配置选项的页面。

![](img/d84604054810a13cacfdac212ebee2f7_68_0.png)

图 4-1：Usermin Configuration 索引

## GnuPG Encryption

GnuPG（Gnu Privacy Guard，或简称 gpg）是 PGP（Pretty Good Privacy，一种商业产品）最初提供的加密标准的完整且自由软件实现。它不依赖受专利限制的 IDEA 算法，因此可以无限制地用于商业或非商业用途。GnuPG 为电子邮件和文件提供多种类型的强加密和数字签名。使用 GnuPG 强加密，可以发送私人电子邮件，可以确信只有收件人才能解密消息。此外，消息可以进行数字签名，允许确认发送者身份并验证消息内容（即确认这确实是发送者所撰写的信息，并且在传输过程中未以某种方式被修改）。

此模块只有一个可配置选项，即用于发送和接收密钥文件的密钥服务器。如果你使用 GnuPG 来确认签名，则有必要使用中央密钥服务器，以便可以在集中数据库中查找身份。通过这种方式，可以在能够确认他人身份的个人之间编织信任网络。由于世界各地有大量公共密钥服务器可用，并且它们同步数据，因此选择你附近的一个是个好主意。

## Configurable Options for Mail Forwarding

Webmin 和 Usermin 支持多种不同的邮件传输代理（MTA），即 Sendmail、Postfix 和 Qmail。此选项应设置为你的服务器使用的邮件传输代理。Postfix 未列为选项，因为从用户角度来看 Postfix 完全与 Sendmail 兼容。只需在 Postfix 为 MTA 时选择 Sendmail，一切都会按预期工作。

## Configurable Options for Read Mail

Usermin Read Mail 模块为用户提供了一个完整但基础的基于 Web 的邮件客户端。它允许用户发送和接收邮件，以及保留简单的地址簿并对消息进行数字签名或加密。对于此模块，有许多可配置选项，如图 4-2 和图 4-3 所示。

![](img/d84604054810a13cacfdac212ebee2f7_69_0.png)

图 4-2：Read Mail 的可配置选项

### Default hostname for From: addresses

这是将包含在邮件头 From 字段中的主机名。如果你希望来自你的域的所有邮件都仅以域名（而不是例如 mail.domain.com）寻址，你可以在此处输入它。输入 domain.com 将导致使用 Usermin 邮件客户端从此机器发送的所有邮件看起来都来自 domain.com。

### Allow editing of From: address

如果为 Yes，用户可以在 From 字段中输入他们选择的任何地址。如果为 No，所有邮件将被标记为源自你在上一个选项中选择的域。如果客户端有自己的域名或希望主要使用另一个地址并且不想处理另一个邮箱的回复，允许此更改可能是合适的。

### From: address mapping file

在托管虚拟域时，将 From: 地址设置为适当的用户@virtualdomain.com 地址而不是真实用户名和系统域可能是有用的。此选项将 Usermin 设置为从域映射文件（通常是 generics 表）中选择正确的地址。

### Mail storage format

与上面的 Mail Forwarding 配置一样，此选择应与你的服务器上运行的 MTA 匹配。如果你安装了 Postfix，可以选择 Sendmail 风格的单文件。

### Sendmail mail location

在此选择你的邮件存储目录的位置。这通常位于 /var/spool/mail，另一个常见选项是将其传递到用户的主目录中的 mbox。这取决于你的邮件投递系统的配置（可能并不实际是 Sendmail）。Postfix 可以使用与 Sendmail 兼容的邮件投递选项，因此此处不需要特殊配置。

### Sendmail file in home directory

如果邮件存储在用户的主目录中，请在此处指定收件箱的文件名。通常这是 mbox，但某些邮件服务器或邮件客户端可能会选择其他名称。通常收件箱根本不在用户的主目录中，因此此选项并不总是必要。

### Qmail or MH directory location

如果使用 Qmail 或 MH，请在此处指定系统邮件存储目录的位置。QMail 和 MH 使用自定义邮件存储格式，其实现为一封邮件一文件，与传统 mbox 格式将所有电子邮件放入单个文件不同。一些管理员和开发人员认为这提供了更好的性能和更好的可靠性。

### Qmail or MH directory in home directory

如果邮件存储在用户的主目录中而不是系统邮件 spool 目录中，你可以在此处指定位置。通常，这将是 Maildir 目录，尽管它可能是其他内容。

### Mail subdirectory style

一些邮件投递代理允许将邮件 spool 目录划分为多个子目录，以便于管理并适应某些 UNIX 文件系统的限制。如果你的投递代理不将所有邮件投递到单个邮件 spool 目录，而是将邮件投递到分布在许多子目录中的用户，你可以在此处进行配置。

### POP3 or IMAP server name

除了读取本地邮件外，Usermin 还可以从 POP3 或 IMAP 服务器检索电子邮件。如果你的邮件 spool 位于远程服务器上，你可以在此处指定它。

