
`usql` 提供命令来编辑缓冲区，并使用 `$w`（仅对当前会话有效！）将查询写入配置文件的默认命令。在交互式会话期间，你可以在启动 `usql` 后，从自己的缓冲区中加载并执行命令。文件名和行号的可选参数允许你编辑之前会话中保存到磁盘的查询。`$p` 命令显示缓冲区内容，而 `$w` 重置缓冲区。

`$c FILE`

```bash
$c my://marco:myppassword@localhost/U
```

`$f FILE`

`customers`

使用 `$c` 命令重新执行缓冲区中的查询。如果你也

`$f` 执行 `FILE` 的内容，并且 `$g`

如果你想执行重结果的每一个值，请输入 `$exec`。`$gset` 命令类似，但它会在当前脚本的目录中查找文件。`$w` 是在 `usql` 中存储查询的结果。如果你连接到一个像 `SQLite 3` 这样的无服务器文件数据库，这很有帮助，因为如果你经常使用 `usql`，早晚你都会创建自己的 `usql` 用例库。在这种情况下，`DSN` 有许多简单的结构：`driver:/path/to/file-` 磁盘，可以组织在几个文件夹中，甚至可以相互调用。

## 输出格式

`usql` 的一个很棒的特性是它有许多打印查询结果的选项。驱动程序可以是 `sqlite3`、`sq`，或 `file`，或者命令可能没有指定驱动程序。

你可以以 `CSV`、`JSON` 或表格格式打印，并支持纯文本或 `HTML`。

## 连接数据库

`usql` 通过解析字符串并将其内容传递给相应的数据库驱动程序来打开数据库连接。数据库多到无法描述，但连接字符串（也称为“数据文件 `$HOME/my-sqlite-db.sqlite3`”：大多是显而易见的。`DSN` 可以直接在命令行上传递给 `usql`：

```bash
#> usql sqlite3:$HOME/my-sqlite-db.sqlite3
```

通过字符串有效的 `HTML` 表格属性在交互会话期间的任何时候，都会将这些属性应用于。在交互会话中，你可以

```bash
#> usql $HOME/my-sqlite-db.sqlite3
```

第二个命令可以通过 `$c` 元命令单独传递所有必要的参数（驱动程序、数据库名称等）来正常工作。通常情况下，

## 变量与系统交互

连接到 `PostgreSQL` 或 `MariaDB` 等多用户数据服务器的 `DSN`

我在 `usql` 中特别喜欢的一点是它与其运行的系统交互的能力。在 `Linux` 中，你可以输入 `$!` 来打开交互式 shell。输入 `$!` 后接 shell 命令将仅执行该命令并返回 `usql` 提示符。`usql` 还允许你设置希望使用的正确斜杠数量，这对应于环境变量和内部变量。例如：数据库类型或 `usql` 允许的任何别名。在连接到 `PostgreSQL` 数据库时，驱动程序可能是 `postgres` 或 `pg`，而在使用 `MySQL` 时，你应该使用 `mysql` 或 `my`。用户、`pass`（即密码），

驱动程序部分是驱动程序的名称，只需使用环境变量：

文件名只需要一个：

```bash
#> set MY_NAME 'Marco'
```

```bash
#> set MY_NAME = 'Marco'
```

```bash
#> usql sqlite3://U
```

```bash
#> $unset MY_NAME
```

`$HOME/my-sqlite-db.sqlite3`

```bash
#> $setenv NUMBER_OF_CUSTOMERS
```

```bash
#> usql file:/$HOME/my-sqlite-db.sqlite3
```

`FOUND_CUSTOMERS`

`46`

`2020年11月`

`第240期`

`LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM`

# 深度解析

### Sql

列表1：Shell 脚本伪代码

变量可以是灵活的。只要在名称前加上冒号和任何引号，

```bash
echo "The number of customers is $NUMBER_CUSTOMERS"
```

即可为...赋值。在:

`0:`

```bash
usql -f mysqlscript_1 -o USQL-OUTPUT.csv
```

`02, usql, 查询：`

在第一行中，`usql` 定义了一个变量并为其分配了值

### 结论

一旦你使用 `$set` 创建了变量并为其赋值了值，你就可以在不创建任何文件的情况下 `usqlscript_2`。

然而，如果 `mysqlscript_2` 文件包含这些复合语句，就像你可以包含这种 `usql` 命令的组合

## 输出。

`usql` 命令最强大的特性是它可以即时使用变量。

# 深度解析

## Mistborn

### 保护家庭网络上的互联网服务：单源

`Mistborn` 将你家庭网络中重要的互联网服务整合在一起，并通过 `WireGuard VPN` 隧道、`Pi-hole`、`iptables` 规则以及独立的容器对其进行安全保护。`Ferdinand Thommes` 利用当前的形势和疫情期间的安全漏洞，几乎无法跟上关闭服务内部安全风险的任务进度。

`COVID-19` 迫使许多人居家办公，依赖互联网服务进行文件共享、视频会议以及 `Zoom` 视频会议平台 [1]，该平台自初期以来用户激增。

为了避免这些陷阱，`Cyber5k` 的安全软件开发者 `Steven Foerster` 除了面临可能更糟糕的外部威胁外，还需要为他家人所有的网络活动提供一个易于实现的安全解决方案。结果就是 `GitLab` 上的 `Mistborn` [2] 项目，该项目完全基于自由软件。（名称源自布兰登·桑德森同名的史诗奇小说系列。）

`Mistborn` 提供了通过脚本控制的 `WireGuard VPN` 隧道设置，以及通过使用 `DNSCrypt` [3] 的 `Pi-hole` 广告拦截（图 1）。此外，`Mistborn` 还允许你激活并管理其他服务，如 `Nextcloud`、`Cockpit`、`Syncthing`、`Rocket.Chat`、`Home Assistant`、`Jellyfin`、`Bitwarden`、`ONLYOFFICE`、`Tor` 和 `Jitsi`。

## 安装

在我们的实验室，我们使用一台 `Lenovo ThinkPad X220` 作为服务器，一台 `ThinkPad X230` 作为客户端，两者都运行 `Ubuntu 20.04 LTS (Focal Fossa)`。从外部的访问由集成防火墙控制。你可以通过任何设备的 Web 界面控制软件。

图 1：通过 `Mistborn`，所有流量都通过 `WireGuard` 隧道运行。

![](img/d1478ca893bfbd12a417e8f50e507b16_293_0.png)
![](img/d1478ca893bfbd12a417e8f50e507b16_293_1.png)

```bash
File git  status  diff  help

$ mistborn:~$ git clone https://gitlab.com/cyber5k/mistborn.git

Clones after 'mistborn'

remote: Downloading objects: 174, done

remote: Counting objects: 100% (174/174), done

remote: Compressing objects: 100% (174/174), done

remote: Total 489 (delta 118), reused 02 (delta 63), pack-received 386

Receiving: 100% (174/174), 2.50MB | done

Resolating: 100% (201/201), Finished.

mistborn:~$ sudo bash ../mistborn/scripts/install.sh

Creating user mistborn

Adding mistborn to sudoers

/home/pi PowerShell

wi-fi is currently blocked by rfkill.

use raspi-config to set the country before.

Running mistborn
```

![](img/d1478ca893bfbd12a417e8f50e507b16_298_0.png)

`(Mistborn)` 设置默认管理员密码:

```bash
File git  status  diff  help

$ Removing intermediate container 6b99a480cfb

== Removed container 6b99a480cfb

==> Running in 87s (1/1)

==> Finishing intermediate container

==> step 4/6 Pull sha256 00e83

==> Running in 87s (2/6)

==> step 5/6 Extracting file layers

==> step 6/6 Verifying container layers
```
