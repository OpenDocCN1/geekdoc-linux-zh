
保持 Nextcloud 更新非常重要，特别是如果你运行的是面向云的实例。这个界面让操作变得简单。

……Web 服务器，但如果你更倾向于使用轻量级的 Nginx（用于 LEMP 栈），这并不重要：两者都需要极少的配置即可运行。我们将在教程中使用 Debian，但这些指令在树莓派 Ubuntu 或适配了其他发行版的 Ubuntu 上也能良好运行。如果你在远程服务器上运行此操作，请伸好手指并 SSH 登录。首先，让我们从更新系统开始：

```bash
$ sudo apt update
```

现在我们将安装 Nextcloud，因为我们已经准备好了 PHP 软件包。Nextcloud (13) 带有 PHP 5（Debian 其他版本的默认版本）或最后一个支持的版本。因此，是否使用 Debian 默认的 PHP 7.0 取决于你，这将需要使用一些外部仓库（如 Ondrej）。

```bash
$ sudo apt install mariadb-server libapache2-mod-php70
```

最后一个是 Apache 的 PHP 模块，它告诉 PHP 解释本教程中的脚本。我们将使用官方 PHP 软件包和 PHP 服务器。由于我们要手动安装 Nextcloud，不受包管理器的控制，我们还必须安装所需的 PHP 模块。这些模块相当多，因此你可能希望从官方文档 https://docs.nextcloud.com 查看并复制。

> 我们的经验
>
> Jonny Bidwell 曾被吸血鬼咬过。在随后的混乱中，他邀请了 Linux 新闻业的未来，结果文章因加密货币拍卖而延迟了。最好不要……

## 快速提示

DNS 和 SSL 证书的设置非常简单，我们无法把指令全部写在这里！你可以在 https.org 和 https://certencrypt.org 找到指南，了解如何为前者提供的域名获取证书信。

## 安装 LAMP 栈

Nextcloud 需要 LAMP/LEMP 栈才能运行，因此我们先设置它。如果你是初学者，请参阅 https://nextcloud.com/docs/installation.html 中的手册。

# Linux Format 2020

接下来我们将获取 PGP 签名并进行验证：

* `wget https://nextcloud.com/server/releases/nextcloud-13.0.4.tar.bz2`
* `gpg verify nextcloud-13.0.4.tar.bz2.asc`

如果你看到一行以 `pg: Good signature from "Nextcloud Security" <security@nextcloud.com>` 开头的文字，那么你就可以松口气了。这说明我们下载的公钥确实来自 Nextcloud 且未被篡改。为了确保万无一，如果你收到（或看到）LXF223-224，请信任 John Lane 的签名：请合理确保它确实是 Nextcloud 的真实签名：

* `tar -xvf nextcloud-13.0.4.tar.bz2`

这会将所有内容解压到 `nextcloud/` 目录，除非你已经领先了一步，正处于目标机器的家目录中。我们需要 Web 服务器能够看到 Nextcloud 文件，因此让它们移动到 Apache 的文档根目录并适当更改所有权：

## 配置 Apache

我们现在配置 Apache 来提供 Nextcloud 应用服务，但在此之前，让我们检查 Apache 是否正在运行。在输入输入目标 IP 地址（如果不知道，请运行 `ip`），Apache 的配置将与 Debian/Ubuntu（及其衍生版本）设置不同，以保留你的个人设置、打开的文件并启用每个站点（或我们想要的任何内容）。所以让我们为我们的 Nextcloud 实例创建一个配置文件：

```
sudo mv nextcloud /var/www/
sudo chown -R www-data /var/www/nextcloud
```

```
sudo nano /etc/apache2/sites-available/nextcloud.conf
```

现在填充内容。这会将 `/nextcloud` URL 指向我们需要安装 Nextcloud 的目录

## 使用 NEXTCLOUD 网页版安装

![](img/b82853b6232162a20e963fd53f1b434b_103_0.png)

### 1 选择管理员凭据

首先为管理员账户输入用户名和密码。该账户对 Nextcloud 的所有内部机制具有绝对控制权，因此我们创建一个通用用户。还剩下三步：请配置我们之前设置的数据库详细信息（数据库、用户、密码：`nextcloudpassword`）。服务器可以保持为 `localhost`：

![](img/b82853b6232162a20e963fd53f1b434b_103_1.png)

### 2 可选应用

等待后，你最终会看到欢迎界面。这会将你引导至桌面、Android（由于 Nextcloud 现在是免费的）和 iOS 应用，并将你的桌面日历、联系人和文件与你的 Nextcloud 集成。在此阶段你不需要进行这些任何操作；现在不做呢？

![](img/b82853b6232162a20e963fd53f1b434b_103_2.png)

### 3 默认用户

默认文件已安装。已安装的应用（最初仅安装 Activity 和 Gallery）通过左上角的图标访问。查看“文档”和“照片”文件夹，可以看到导航和预览的工作情况。头像出现在右上角的菜单中，可以在那里配置应用、设置和用户。

### 4 创建新用户

要添加新用户，请使用上述名称并选择。然后只需在框中输入用户名和密码并创建。你可以添加组（默认只存在 admin 组），并添加用户，以及控制他们的存储配额或直接删除账户。我们可以安全地退出管理员账户。

## Nextcloud 教程

Alias nextcloud /var/www/nextcloud/

```
<Directory /var/www/nextcloud/>
Options +FollowSymlinks
AllowOverride All
```

```
<IfModule mod_dav>
</IfModule>
```

```
SetEnv HTTP_HOME /var/www/nextcloud
SetEnv HTTP_VAR /var/www/nextcloud
```

```
<Directory>
```

- 现在启用新定义的站点：

`sudo a2enite nextcloud`

`sudo a2enmod`

`sudo a2mod env`

`sudo a2enmod dir`

你会看到一条消息，提示重加载 Apache 使更改生效，但在之前我们启用额外的 Apache 模块以便 Nextcloud 能够完成...

`sudo systemctl restart apache`

最后三个在全新的 Debian 安装中是默认启用的，但检查它们并没有坏处。你需要重启 Apache 服务器。在此阶段，Nextcloud 正在通过其 IP 地址工作。你现在可以连接它，例如在本地机器的浏览器上访问 `http://192.168.1.100/`。希望 Nextcloud 安装顺利。在 `nextcloud` 目录中，检查 MariaDB 是否运行（`sudo systemctl mysql`）并双重检查所需包是否已安装。将服务器的 IP 地址添加到你想访问的机器的 `/hosts` 文件中。你可以通过添加以下行来实现：192.168.1.100

服务器可以通过 `nextcloud.local` 访问。所以我们将遵循我们的四步指南来完成你的 Web 配置。

## 最后调整

在继续之前，有几件事需要配置。首先，没有人喜欢长 URL，所以我们可以使用 Nextcloud 重写。编辑（或覆盖）`/nextcloud/config/config.php`，在最后一行之前添加（如果你有主机名），该命令直到我们运行维护脚本之前生效：

```
sudo -u www-data php /var/www/nextcloud/occ maintenance:update
```

注意我们在上述步骤使用了 `https` 而不是 `http`。启用（并强制）加密是一个好主意，因为敏感数据可能会被窃听，我们需要处理：

```
sudo a2enmod ssl
sudo systemctl restart apache
```

如果你现在访问 `https://nextcloud.local`，你会看到关于你的网站不安全的警告。这是因为默认配置使用了自签名证书。在本地网络中，除非从公共证书机构获取证书，否则你无法信任它。这比现在要好得多。我们可以强制 Apache 通过 HTTPS 提供资源；由于我们要使用我们的服务器，我们将在 `/nextcloud/.htaccess` 文件中进行这些更改。滚动到下面的部分并在末尾添加行：

```
<IfModule mod_rewrite>
RewriteCond SERVER_PORT 80
RewriteCond %REQUEST_URI ^/nextcloud/
RewriteRule ^(.*)$ https%{SERVER_NAME}/nextcloud/$1 [R=301]
</IfModule>
```

最后，这是最后的触摸以及重加载 Apache 使重定向生效：

```
sudo systemctl restart apache
```

你已经完成了 Nextcloud 的操作！

![](img/b82853b6232162a20e963fd53f1b434b_104_0.png)

Nextcloud 可以通过不断增长的应用选择进行扩展，你可以以管理员身份进行探索。

## 快速提示

除了代码，还有许多与 Nextcloud 连接的应用程序。流行的树莓派可以将你的自托管服务（如 Gmail）集成到 Nextcloud 界面中。

## 获取你的完整免费版，立即订阅 http.ly/Linux

# 终端：LSHELL

## 限制用户对你个人发行版的访问

担心用户通过无限制的访问搞乱你的系统吗？**Shashank Sharma** 使用 lshell 来限制他们的使用。

![](img/b82853b6232162a20e963fd53f1b434b_105_0.png)

大多数现代 Linux 发行版都自带几个不同的 shell。这些 shell 包含了帮助你完成任何任务的工具，例如移动或删除文件、移除机器、执行脚本和管理用户。这种力量的缺点是可能会损害系统。通过 lshell，用户可以获得一组命令的权限、在 SSH 上输入危险命令、实施限制等！

使用 lshell 来限制用户执行命令是合理的。例如，一旦不小心使用 `dd` 删除了磁盘或使用 `cat` 将 ISO 写入 4GB 的 USB 盘的情况就会发生，但通过 lshell，每个用户都受到限制，无法运行 `dd` 或 `disk` 等命令，这些命令如果使用当可能会破坏系统。

该工具在软件存储库可用，但安装非常直观。你必须在计划下载的目录中安装 `python` 和 `git`：启动终端并切换到使用 `setup.py` 安装。

你现在可以通过 `cat /etc/shells` 检查 lshell 是否在已安装的 shell 列表中：

Shashank Sharma 是德里的一位律师，也是热爱的 Linux 用户。他总是关注极客信息。

```
## echo SHELL
### /bin/bash
### /bin/sh
### /etc/shells: 有效的登录 shell
### /bin/bash
### /bin/dash
### /bin/bash
### /usr/bin/lshell
```

确定默认 shell。你可以使用 `chsh -s /usr/bin/lshell` 更改用户的 shell。

- `[global]` - 全局范围设置，例如日志记录。
- `[default]` - 适用于所有用户和组的设置。
- `[username]` - 仅适用于特定用户的中心化设置。
- `[groupname]` - 适用于组及其所有成员设置。

## 配置 lshell

通过 lshell，你可以为不同的用户创建配置和定义。默认 lshell 存储在 `/etc/shells` 并适用于所有用户。

配置可以分为四个部分：

| 字段 | 描述 |
|---|---|
| `[global]` | 全局范围设置，例如日志记录。 |
| `[default]` | 适用于所有用户和组的设置 |
| `[username]` | 仅适用于特定用户的中心化设置 |
| `[groupname]` | 适用于组及其所有成员设置 |

配置的优先级是：用户 > 组 > 默认。这意味着 lshell 首先查找用户设置并应用其中提供的设置，然后是组和默认设置。在冲突的情况下，用户名设置将覆盖组设置。

或者，你可以在创建新用户时使用 `sudo adduser --shell=/lshell/` 将 lshell 设置为默认。

```
2/ 终端缺失
$ luser@linux-bound:~$ chsh -s /usr/bin/lshell
密码: 
$ 输入 '7' 获取可用命令列表
$ clear echo exit help list ls is lshell
$ 没有任何命令
$ 优先级
$ home@user:~$
$ 禁止命令: name
```

新安装的 lshell 配置没有 (username) 或 (groupname) 部分。这些必须手动添加。你可以通过定义以下来配置 lshell 想要保留的日志量：

用户只能运行受限于所有路径和命令列表的 lshell 命令

loglevel 取值。它接受从 0 到 4 的设置，其中 0 表示不记录日志，而 4 会记录用户输入的每一个命令。

默认情况下，该工具使用 syslog 记录日志，但也支持自定义格式。例如，如果你使用 ver logs，请将 /etc/syslog.conf 中的 logname 替换为 logname-suffix。

Sudo 会为每个会话、每个用户和守护进程启动的进程创建一个日志目，并将日期和年份写入文件。要添加这些内容，你还可以使用 %Y 为条目添加时间戳，或使用任何其他命令来记录日志。

allowed 选项用于提供所有允许运行的命令列表。如果你想让用户运行所有命令，可以将其设置为 all。同样地，你可以限制用户访问某些路径，例如 /etc/。timeout 选项限制了用户在给定计时器下使用终端的时间：

- allowed: ['all', ['var/*','cd','cp','mv']]
- forbidden: ['/var/*','/usr/local/*']
- [user]
- allowed: ['+pwd','ping','cp']
- forbidden: ['+etc']

在此块中，我们为用户 adnina 和 inumala 创建了两个条目。对于第一个，我们定义了允许访问的目录。

允许访问。使用 allowed 选项，我们限制了对某些目录的访问，但以 - 开头的目录除外。符号表示用户的来源。

同样，对于用户 inumala，我们定义了对 Default 部分描述的目录的访问。同样，还了该节描述的命令。

你可以使用 over 选项获取可用命令列表。另一个有用功能是定义用户通过 SSH 连接时可以运行的命令。为此，你必须使用 over 选项：

- allowed: ['+pwd','ping','cp']
- forbidden: ['+/var/*','/home/user/*']
- restricted: ['+root','/script/*']

与之前一样，我们使用 over 选项描述了 Default 部分中允许用户 inumala 运行的额外命令。另一方面，符号 - 用于限制用户在通过 SSH 连接时运行或 sc 命令。

# 绕过受限 shell (RESTRICTED SHELL)

它们本身，Bash、Ksh 和 Zsh 都都具有一个受限 shell。如果你的 Linux 发行版中将 bash 定义为你的 shell，你可能已经安装了 bash。受限 shell bash 具有每种有限的能力。

如果你安装了 bash，可以将其作为终端、受限 shell 来运行。

你可以通过在终端上运行 bash 来启动受限 bash。要将其设置为默认 shell，而不是更改 shell，请设置 PATH 或 SHELL 变量：

当运行受限 shell 时，用户不允许运行 PATH 或 SHELL 变量以外的命令，重定向输出到：

使用受限 bash 的缺点是用户可以。例如，如果 /bin/ 在 PATH 中，用户可以使用 bash 逃逸受限 shell，然后运行完整版本的

```
adina@raspberry-budget:~$
set shell=/bin/bash
```

现在用户可以恢复全功能的 bash，而不是只有最基本命令且容易逃逸的 bash Raspberry。这种技术也适用于 shell 本身，但仅当你在允许列表中使用它时。使用简短的允许命令列表效果更好，即允许所有并阻止访问少数几个。

> 小贴士
>
> 当使用文本编辑器时没有自动将 /usr/bin/ 添加到 shell/ /etc/shells 文件时，请确保在文件末尾留有一个换行符。

# 2020 Linux 格式年度报告

# 安全

## 保持你的桌面安全可靠

Linux 本身可以阻止大多数攻击，但 Mayank Sharma 可以随时帮助你为计算机周围建立一个 10 级强力力场……

Mayank Sharma 是一位技术作家，他花费大量时间玩与其他不同的 Linux 游戏。

运行 Linux仅仅是因为你认为它比 Windows 好？重新想一下。Linux 的安全性是直接从内核到桌面的内置功能，但它仍然留下了让别人知道你的 /Home 文件夹的空间。Linux 对为 Windows 编写的病毒和蠕虫免疫，但攻击者还有其他技巧可以非法访问你珍贵的比特和字节，这可能会让一切变得相等发送给你信用卡的邮件。

用用户名和密码锁定数据应该是你唯一的防线，它无法挡住坚定的攻击者。随着攻击数量和种类的日益增加，你应该花精力采取额外措施来完全保护你的计算机。
