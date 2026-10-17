
SSL 运行时选项由 `SSLOptions` 指令控制。此处显示的选项支持在无需密码的情况下访问安全网站（`+FakeBasicAuth`）、使用刚刚创建的 SSL 密钥（`+ExportCertData`）以及拒绝访问不适当的系统（`+StrictRequire`）。

```
SSLOptions +FakeBasicAuth +ExportCertData +StrictRequire
```

某些文档建议针对 CGI/SSI 环境变量包含 `ApacheEnvVars` 选项，但该选项在 Ubuntu 版本的 Apache 实现中已不再可用。（欲更多信息，请参阅 https://bugs.launchpad.net 中的 bug 17995。）

接下来两个指令用于访问创建的证书和密钥文件：

```
SSLCertificateFile /etc/ssl/certs/server.crt

SSLCertificateKeyFile /etc/ssl/private/server.key
```

对默认虚拟机的其他更改遵循与普通虚拟主机相同的规则。不要忘记为安全网站创建适当的目录和 HTML 文件，并为任何你想跟踪的网站创建专用日志目录。进程完成后，重启 Apache 服务。然后你应该能够像访问任何其他安全网站一样访问该安全网站。

## 准备 Apache 文档供 Web 访问

如果你希望在本地网络上可以使用 Apache 文档，安装它非常简单。只需采取以下步骤：

- 1. 运行 `sudo apt-get install apache2-doc` 来安装指定的软件包。该操作会将当前的 Apache 文档主要安装在 `/usr/share/doc/apache2-doc/manual` 目录下——包含多种语言。
- 2. 检查 `/etc/apache2/conf.d` 目录下的 `apache2-doc` 配置文件。使用此处所示 `Alias` 指令：
  `Alias /manual /usr/share/doc/apache2-doc/manual/`
  可以将与 Apache 文档相关的 HTML 文件放在配置妥当的 `/var/www/manual` 目录。
- 3. 使用以下命令从 `/var/www/manual` 创建到 `/usr/share/doc/apache2-doc/manual/` 的链接：

```bash
$ sudo ln -s /usr/share/doc/apache2-doc/manual /var/www/manual
```

## Ubuntu 服务器管理

![](img/fadb0f527b947cf4d02cbbbb791a6562_426_0.png)

图 15-6. 本地可访问的 Apache 文档

- 4. 查看此指令，它遵循符号链接目录。它允许访问 `manual/` 子目录下的 Apache 文档主页，如图 15-6 所示。

`Options Indexes FollowLinks`

我 导航到 `http://ServerIPAddress/manual/`；得益于 `LanguagePriority` 指令的默认值，显示的是英文网页。

供你参考，网页顶部附近的可用语言。包括德语 (`de`)、英语 (`en`)、西班牙语 (`es`)、法语 (`fr`)、日语 (`ja`)、韩语 (`ko`) 和巴西葡萄牙语 (`pt-br`)。

## 总结

网站管理员可能对 Ubuntu 实现的 LAMP 栈感兴趣。其组件是 Linux、Apache、MySQL 和 PHP。其他 LAMP 栈可以使用 Perl 或 Python 替换 PHP，这些替代方案的软件包也可用。由于 MySQL 和 PHP 的配置通常是数据库管理员和程序员的职责，本章的重点是 Apache Web 服务器。

大多数 Apache 配置文件位于 `/etc/apache2/mods-enabled/` 目录。已启用的虚拟主机配置在 `/etc/apache2/sites-enabled/` 目录下的文件中。虚拟主机可以共享同一个 IP 地址。这些文件中的信息整合在 `/etc/apache2/apache2.conf` 配置文件中。整体语法可以使用 `apachectl configtest` 命令进行检查。

Apache 能够轻松地创建和配置使用 TCP/IP 端口 443 访问安全网站所需的安全密钥、CSR 和证书。通过少量的额外的配置更改，你可以在用于普通虚拟机的相同 IP 地址上设置虚拟主机。

# 第 16 章

## 创建文件服务器

与 Linux 相关有两个文件服务器：网络文件系统 (`NFS`) 和 Samba。虽然可以使用许多 GUI 工具来创建服务器，但本章将向你展示如何从命令行配置这些服务。如果你知道如何使用这些服务，通过直接编辑关键配置文件，可以在更短时间内完成更多工作。Ubuntu 的共享文件夹（Shared Folders）GUI 工具可以管理 NFS 和 Samba 系统，你将看到如何使用它。如果你学会直接编辑服务器配置文件，你将遥遥竞争对手。

`NFS` 是一种允许访问远程系统目录的协议。对 NFS 挂载目录的访问是透明的；某些网络从中央服务器配置 `/home` 目录。假设网络足够快，用户将无法区分 NFS 挂载的 `/home` 系统与 `/home` 目录的区别。由于 NFS 最初是为 Unix 设计的，Linux 继承了它的优点，作为一种与其它 Linux 和 Unix 工作站共享文件的简用且强大的方式。

Samba 是服务器消息块 (`SMB`) 的开源实现，该协议最初由 IBM 开发并由微软适配。作为一种文件和打印机共享服务，它支持与其他 Linux 甚至微软工作站共享。它整合了微软通过通用互联网文件系统 (`CIFS`) 所的更改。Samba 也可以配置在

## 两个文件服务器

`NFS` 是一种允许访问远程系统目录的协议。对 NFS 挂载目录的访问是透明的；某些网络从中央服务器配置 `/home` 目录。假设网络足够快，用户将无法区分 NFS 挂载的 `/home` 系统与 `/home` 目录的区别。由于 NFS 最初是为 Unix 设计的，Linux 继承了它的优点，作为一种与其它 Linux 和 Unix 工作站共享文件的简用且强大的方式。

Samba 是服务器消息块 (`SMB`) 的开源实现，该协议最初由 IBM 开发并由微软适配。作为一种文件和打印机共享服务，它支持与其他 Linux 甚至微软工作站共享。它整合了微软通过通用互联网文件系统 (`CIFS`) 所的更改。Samba 也可以配置在

`NFS` 的一个弱点是不加密。默认情况下，`NFS` 共享是不加密的。然而，你可以使用 SSH 隧道来加密。

## 创建文件服务器

在某种程度上，安装哪个版本的 NFS 并不重要。`NFS` 服务器相对容易配置。只需注意 NFS 服务取决于服务器和客户端之间的一性。

在本章中，你将学习如何配置 `/exports` 文件，导出这些共享，然后从 NFS 客户端进行连接。或者，你可以使用 Ubuntu 的共享文件夹工具，将在章节末尾讨论。

### 内核服务器

对于 NFS 内核服务器，有三个软件包与 NFS密切相关：`portmap`、`nfs-common` 和 `nfs-kernel-server`。由于它们默认未安装，你可能需要使用如下命令将它们集成到系统中：

```bash
$ sudo apt-get install portmap nfs-common nfs-kernel-server
```

此安装包含了 `/etc/exports` 中的 NFS 内核服务器配置文件，以及 `/etc/default` 目录中的另外三个。

### 用户服务器

安装 NFS 用户服务器更简单。安装 `nfs-user-server` 软件包只需要 `portmap` 支持。由于它们默认未安装，你可以使用如下命令将它们集成到系统中：

```bash
$ sudo apt-get install nfs-user-server portmap
```
