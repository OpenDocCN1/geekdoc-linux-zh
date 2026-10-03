
```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/xhtml1-transiti
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Apache2 Debian Default Page: It works</title>
<style type="text/css" media="screen">
margin: 0px 0px 0px 0px;
padding: 0px 0px 0px 0px;
body {
padding: 3px 3px 3px 3px;
background-color: #D8D8E2;
font-family: Verdana, sans-serif;
font-size: 1pt;
text-align: center;
}
div.main_page {
position: relative;
display: table;
```

列表 12-1：Apache Web 服务器 `index.html` 文件

注意，默认网页的内容与我们打开浏览器访问 `localhost` 时显示的文本完全一致，采用 HTML 格式。我们所做的只需编辑或替换此文件，以便我们的 Web 服务器显示我们想要的信息。

## 添加一些 HTML

现在我们的 Web 服务器已经运行，且 `index.html` 文件也处于打开状态，我们可以添加任何我们想要 Web 服务器提供的文本。我们将创建简单的 HTML 块。

让我们创建这个页面。在你的文本编辑器中创建一个新文件，输入列表 12-2 所示的代码。

```html
<html>
<body>
<h1>Hackers-Arise!</h1>
<p>If you want to learn</p>
<p>is the best!</p>
</body>
</html>
```

列表 12-2：简单的 HTML 块

## 看看发生了什么

现在我们的 Web 服务器已经运行，且 `index.html` 文件也处于打开状态，我们可以添加任何我们想要 Web 服务器提供的文本。我们将创建简单的 HTML 块。让我们创建这个页面。在你的文本编辑器中创建一个新文件，输入列表 12-2 所示的代码。

```html
<html>
<body>
<h1>Hackers-Arise!</h1>
<p>If you want to learn</p>
<p>is the best!</p>
</body>
</html>
```

（注：由于原文中存在大量重复内容，译文已按逻辑进行整理并完成翻译）

将模块连接到摄像头接口，然后再次开启。注意，摄像头非常脆弱，绝对不能与通用输入/输出（`GPIO`）引脚接触；否则可能会导致短路并损坏设备。

现在，`SSH` 服务已经启动并运行，将 Raspberry Spy Pi（树莓派间谍摄像头）放置在你的家里、学校或其他任何你想要监控的地方。当然，它已经连接到了局域网，可以通过以太网线连接，理想情况下也可以通过 Wi-Fi 连接。（新的 Raspberry Pi 3 和 Raspberry Pi Zero 都内置了 Wi-Fi。）

现在，你需要获取你的树莓派的 IP 地址。正如你在第 3 章中所学习的，你可以使用 `ifconfig` 获取 Linux 设备的 IP 地址：

```
pi >ifconfig
```

你的 Pi 的 IP 地址为 `192.168.1.101`，但请确保在本章任何出现该地址的地方，你使用的都是自己 Raspberry Spy Pi 的 IP 地址。从你的 Kali 系统，你应该能够直接连接并控制你的 Raspberry Spy Pi，并将其作为远程监控系统使用。在本示例中，你的系统需要与 Pi 处于同一个网络中。

要从你的 Kali 系统通过 `SSH` 连接到远程 Spy Pi，请记住使用你自己 Pi 的 IP 地址：

```
kali >ssh pi@192.168.1.101
pi@192.168.1.101's password:
```

Debian GNU/Linux 系统包含的程序是免费软件；每个程序的具体分发条款在 `/usr/share/doc/*/copyright` 下的单独文件中说明。

Debian GNU/Linux 提供的软件**绝对没有任何担保**，在适用法律允许的范围内

最后登录时间: Tues Jan. 1 12:01:01 2018

`pi@raspberrypi: $`

随后 Spy Pi 将会提示你输入密码。在这种情况下，默认密码为 `raspberry`，除非你更改过它。

## 配置摄像头

接下来，我们需要配置摄像头。为了做到这一点，通过输入以下命令启动树莓派配置工具：

```
pi >sudo raspi-config
```

这将启动一个类似于图 12-3 所示的图形菜单。

### 树莓派软件配置工具 (raspi-config)

| 项目 | 描述 |
| :--- | :--- |
| 1 Expand Filesystem | 确保 SD 卡的所有空间均可用 |
| 2 Change User Password | 更改默认用户的密码 |
| 3 Boot Options | 选择启动到桌面模式 |
| 4 Wait for Network at Boot | 选择等待网络连接 |
| 5 Internationalisation Options | 设置语言和区域设置 |
| 6 Enable Camera | 启用此 Pi 与摄像头配合 |
| 7 Add to Rastrack | 将此 Pi 添加到在线树莓派跟踪器 |
| 8 Overclock | 为你的 Pi 配置超频 |
| 9 Advanced Options | 配置高级设置 |
| 0 About raspi-config | 关于此配置工具的信息 |

![](img/1d1085ba208631ba5cace7619c3050fa_165_0.png)

图 12-3: 树莓派配置工具

向下滚动到 **6 Enable Camera**（启用摄像头）并按回车键。现在，滚动到菜单底部并选择 **Finish**（完成）并按回车键，如图 12-4 所示。

![](img/1d1085ba208631ba5cace7619c3050fa_165_1.png)

图 12-4: 完成配置

当配置工具询问你是否想要重启时（如图 12-5 所示），选择 **Yes**（是）并再次按回车键。

![](img/1d1085ba208631ba5cace7619c3050fa_165_2.png)

图 12-5: 重启 Pi 以启用更改。

现在，你的 Raspberry Spy Pi 摄像头应该启用并准备好进行监控了！

## 开始监控

一旦你的 Raspberry Spy Pi 重启并且你已经通过 Kali 终端通过 `SSH` 登录，你就可以开始通过拍摄静态照片来使用它进行监控。

Raspian 操作系统有一个名为 `raspistill` 的应用程序，我们将用它从小小的 Raspberry Spy Pi 拍照。在终端中输入 `raspistill` 查看该工具的界面及其所有选项：

```
@raspberrypi: raspistill
raspistill Camera App v1.3.8
runs camera for specific time, and takes JPG capture at end if requested
usage: raspistill [options]
Image parameter commands
--snip--
```

让我们使用 Raspberry Spy Pi 拍摄远程监控照片吧！

`raspistill` 命令有许多你应该探索的选项，在这里我们将使用默认值。要拍摄照片并将其保存为 JPEG，请输入以下：

```
@raspberrypi: raspistill -o firstpicture.jpg
raspistill Camera App v1.3.8
width 2592, Height 1944, quality 85, filename firstpicture.jpg
Time delay 5000, Raw no
--snip--
```

我们使用 `-v` 选项提供详细输出，并使用 `-o` 选项告诉 `raspistill` 我们即将给它一个使用的文件名；然后我们在 Raspberry Spy Pi 上进行长列表，我们可以看到文件 `firstpicture.jpg`，如下：

```
@raspberrypi: ls -l
total 24
drwxr-xr-x 2 pi 4096 Mar 18 Desktop
drwxr-xr-x 2 pi 4096 Mar 18 Documents
-rw-r--r-- 1 pi 0 Jan 1 00:00
drwxr-xr-x 2 pi 4096 Mar 18 Downloads
drwxr-xr-x 2 pi 4096 Mar 18 Music
drwxr-xr-x 2 pi 4096 Mar 18 Pictures
```

随后 Spy Pi 将提示你输入密码。在这种情况下，默认密码为 `raspberry`，除非你更改过它。

## 从 MySQL 提取信息

MySQL 被广泛应用于许多应用程序。SQL 有多种实现，每个实现都有自己的命令和语法，但这里有一些常用命令：

- `select` 用于检索数据
- `union` 用于合并多个 `select` 操作的结果
- `insert` 用于添加新数据
- `update` 用于修改现有数据
- `delete` 用于删除数据

你可以为每个命令添加条件，以具体说明你想做什么。例如，该行：

`select user, password from customers where user='admin';`

将返回 `customers` 表中 `user` 值为 "admin" 的 `user` 和 `password` 字段的值。

## 启动 MySQL

在 MySQL 的默认配置中，`root` 用户的密码是空的。显然，这是一个安全漏洞，你应该在首次登录后通过密码来修复它。

要启动 MySQL 服务，输入以下：

```
kali >service mysql start
```

接下来，你需要通过登录进行身份验证。输入以下：

```
kali >mysql -u root -p
Enter password:
Welcome to MySQL monitor.
Your connection id is 4
Server version: 5.6.30 (Debian)
Copyright (c) 2000-2016, Oracle and/or affiliates. All rights reserved
Oracle is a registered trademark of Oracle Corporation and/or affiliates. Other names may be trademarks of their respective owners.

Type 'help'; 或 'h' 获取帮助。输入 "\c" 清除当前输入语句。
```

让我们通过输入以下内容查看 MySQL 系统中已经哪些用户。（注意 MySQL 命令以分号结束。）

```mysql
mysql >select user, host, password from mysql.user;
```

| user | host | password |
| --- | --- | --- |
| root | localhost | |
| root | aphrodite.kali.org | |
| root | 127.0.0.1 | |

这显示 `root` 用户没有设置密码。要为 `root` 分配密码，我们首先需要选择一个数据库进行操作。你系统上的 MySQL 已经预装了一些数据库。使用 `show databases` 命令可以查看所有可用的数据库：

```mysql
mysql >show databases;
```

| Database |
| --- |
| information_schema |
| mysql |
| performance_schema |

3 rows in (0.23 sec)

MySQL 默认带有三个数据库，其中两个（`information_schema` 和 `performance_schema`）是我们这里不会使用的管理数据库。我们将使用非管理数据库 `mysql`，它是为了你的目的而包含的。要开始使用 `mysql` 数据库，输入：

```mysql
mysql >use mysql;
```

读取表信息以完成表名和列名
你可以使用 `-A` 参数关闭此功能以获得更快的启动

Database changed

此命令连接到我们的 `mysql` 数据库。现在，我们可以通过以下命令为 `root` 用户设置密码为 `hackers-arise`：

此命令将通过将用户的 `root` 密码设置为 `hackers-arise` 来更新用户。

## 访问远程数据库

要访问本地 `localhost` 上的 MySQL 数据库，我们使用以下语法：

```bash
kali >mysql -u <username> -p
```

如果没有给出主机名或 IP 地址，此命令默认使用本地 `localhost` 上的 MySQL 实例。因此，要访问远程数据库，我们需要提供托管 MySQL 数据库的系统主机名或 IP 地址。这里有一个例子：

```bash
kali >mysql -u root -p 192.168.1.101
```

这将连接到 `192.168.1.101` 上的 MySQL 实例并提示我们输入密码。为了演示，我正在连接到我本地局域网（LAN）上的一个 MySQL 实例。如果你网络中有一个安装了 MySQL 的系统，请在此处使用其 IP 地址。我假设你已经成功绕过密码并以 `root` 身份登录系统（你已经知道默认情况下 `mysql` 数据库没有密码）。

这打开了 MySQL 命令行界面，它为我们提供了界面——包括原生的 MySQL Workbench 以及第三方的 Navicat 和 TOAD for MySQL）。对于作为黑客来说，命令行界面可能是利用 MySQL 数据库的最佳机会，因此我们在这里关注它。未经授权的数据库进入者不太可能会看到易于使用的 GUI。

> 此屏幕提醒我们，所有命令必须以分号或 `\` 结束（与微软的 SQL Server 不同），我们可以通过输入 `help` 或 `/` 来获取帮助。

现在我们已经以系统管理员身份登录，可以无阻碍地浏览数据库。如果我们以普通用户身份登录，我们的浏览将受到系统管理员为该用户提供的权限限制。

## 连接到数据库

访问系统后，我们想要四处查看。下一步是找出是否有任何值得探索的数据库。以下是查找被访问系统上包含哪些数据库的命令：

```mysql
mysql >show databases;
```

+--------------------------------------+
| Database                             |
+--------------------------------------+
| information schema                   |
| mysql                                |
| creditcardnumbers                    |
| performance_schema                  |
+--------------------------------------+

4 rows in set (0.26 sec)

哈！我们发现了一个名为 `creditcardnumbers` 的值得探索的数据库。让我们连接它。

在 MySQL 中，与其他数据库管理系统（DBMS）一样，我们可以通过输入 `use *basename*` 连接到我们感兴趣的数据库；

```mysql
mysql >use creditcardnumbers;
```

Database changed

`Database changed` 响应表示我们现在连接到了 `creditcardnumbers` 数据库。
当然，不必说，一个不太可能的数据库管理员会如此配合地将数据库命名为 `creditcardnumbers` 这样易于识别的名字，因此你可能需要进行一些探索来找到感兴趣的数据库。

## 数据库表

我们现在连接到了 `creditcardnumbers` 数据库，可以进行一些探索看看它可能包含哪些信息。数据库中的数据组织成表，每个表都可能包含一组不同的相关数据。我们可以通过输入以下命令来查看此数据库中有哪些表：

```mysql
mysql >show tables;
```

+--------------------------------------+
| Tables_in_creditcardnumbers         |
+--------------------------------------+
| cardnumbers                          |
+--------------------------------------+

1 row in set (0.14 sec)
