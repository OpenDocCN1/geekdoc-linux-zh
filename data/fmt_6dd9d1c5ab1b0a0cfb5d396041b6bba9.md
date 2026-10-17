
# 项目背景与资源

Bharat Devatta 最初创建了 `Gallery`，但现在有一大批开发者、测试人员和其他贡献者。除了 Bharat，`Gallery` 的贡献者包括 Alan Hader, Andy Staudacher, Andrew Lindeman, Beckett Madden-Woods, Chad Kiefer, Kelly Kris, Christian Mohn, Dariush Molavi, Dave Moore, Donald Webster, Ernesto Bachny, Felix Rabinovich, Jay Rossister, Jen Tetz, Jesse Mullan, Paul Macalliard, Joellen Duran, Michael Kleinert, Michael Scheitzer, Pierre-Luc Pour, Robert Balooks, Ross Reyn 以及许多人。

> 注意 `Gallery` 有许多贡献者列在此：`http://gallery.sourceforge.net/wiki.php?page=Development%20Team`

`Gallery` 软件免费提供。如果你喜欢这个软件，我鼓励你通过任何一种方式支持该项目。在 `Gallery` 主页 (`gallery.sourceforge.net`) 上，你可以点击 `Gallery` 按钮捐赠以维持项目。或者，选择 `Support` 链接了解如何向 `Gallery` 团队付费或安装你的 `Gallery` 软件。

要获取更多关于 `Gallery` 的信息或参与 `Gallery` 社区，请选择 `Gallery` 主页上的 `Wiki` 链接。从那里你可以找到邮件列表、教程、文档、开发以及其他了解 `Gallery` 的方法：之前的开发团队页面介绍了如何加入。

`Linux Toys II` 描述了经过测试的 `Gallery 1.5`。在本文写作时，`Gallery 2.0` 正在开发中。当你读到这里时，`Gallery 2.0` 可能已经可用。

`Gallery 2.0` 的特点是完全重写了界面，但包含了本章描述的所有功能。你可以查看 `Gallery` 网站获取从 `Gallery 1.5` 升级到 `2.0` 的信息，或者简单地下载后来的 `2.0` 版本并用它代替随书的软件。

## 安装 Linux

要在 Linux 中运行 `Gallery`，你需要在服务器的 Linux 系统上至少安装 `Apache Web` 服务器软件和 `PHP` 脚本软件。你还需要一些可选工具用于图像处理等任务（如 `NetPBM` 或 `ImageMagick`）。

## 第 3 章 — 创建 Web 照片库

1. 将 `Linux Toys II` CD 插入你的 CD 驱动器。如果你的 CD 自动挂载，你可以跳过第一条命令。如果没有自动挂载，请以 `root` 用户身份从终端运行以下命令（可能需要将 `/media/cdrecorder` 替换为 CD 挂载的位置）：

```bash
### mount /media/cdrecorder
```

2. 接下来，进入到 `Gallery` 的 `RPMS` 目录并按照如下方式运行 `installme` 脚本：

```bash
### cd /media/cdrecorder/RPMS/ch03-gallery
$ .installme
```

这将安装运行此项目所需的所有 `RPMS`（在本情况下，仅为 `jade` 软件包）。

## 安装 Gallery

以下是在你的 Linux 服务器上初始安装 `Gallery` 的步骤：

> `Linux Toys II` CD 的副本直接源自 `Gallery` 项目网站。在安装之前，请访问 `http://gallery.sourceforge.net` 查看 `Gallery` 网站，确认是否有任何关键软件包可用。事实上，如果 `Gallery 2.0` 可用，你应该考虑使用该版本（尽管用户界面大部分部分与此处显示的有所不同）。最后，我建议订阅 `gallery-announce` 邮件列表（低带宽），以获取任何关键更新通知。

1. 将 `Gallery` 解压到 Web 服务器可以访问的目录中。无论你在何处解压软件，它都会创建一个名为 `gallery` 的子目录。如果你打算让 `Gallery` 公开（或至少在局域网内可用），你必须将其安装在 Web 服务器可以访问的位置。例如，为名为 `chris` 的用户安装 `Gallery` 可以放在 `/home/chris/public_html/gallery/`。系统级安装可以放在 `/var/www/html/`。

以下是你在终端窗口中输入的命令，用于解压 `Linux Toys II` CD 以进行 `Gallery` 安装（请将 `chris` 替换为你的用户名）：

```bash
$ mkdir /home/chris/public_html
$ cd /home/chris/public_html
$ tar xvfz /media/cdrecorder/Sources/ch03-gallery/gallery*.gz
```

2. 在你的目录中创建 `.htaccess` 和 `config.php` 文件以及一个名为 `albums` 的目录，并将所有者设置为你的用户名（例如，使用用户名 `chris`）并将用户组设置为 `apache`，如下所示：

```bash
$ touch gallery/.htaccess gallery/config.php
$ mkdir gallery/albums
$ chown chris:apache gallery/.htaccess gallery/config.php
$ chown chris:apache gallery/albums
$ chmod 664 gallery/.htaccess gallery/config.php
```

3. 为了确保如果 `Gallery` 安装在你的主目录下，`Apache` 服务器可以访问 `Gallery` 文件，你可以如下更改权限：

```bash
$ chmod 711 $HOME
$ chmod 775 $HOME/public_html
```

4. 如果你为 `/var/www/html/gallery` 目录安装 `Gallery`，则不需要对 `Apache` 进行任何特殊配置来访问 `Gallery`。然而，为了从你的主目录访问 `Gallery`，你需要修改 `/etc/httpd/conf.httpd.conf`，允许所选用户的 `public_html` 目录能够发布 Web 内容。首先，你应该注释掉 `UserDir` 行，如下所示，这样该功能就不会被禁用：

```apache
# UserDir disable
```

接下来，添加以下 `Directory` 条目以允许从所选目录发布内容。例如，如果 `Gallery` 安装在 `/home/chris/public_html` 目录，你应该放入内容：

```apache
<Directory /home/chris/public_html/gallery>
AllowOverride Options FileInfo
</Directory>
```

此时，如果你刚刚安装完成，就应该准备好开始检查和配置 `Gallery` 软件了。

![](img/1b8a24a162893627b8005ac678b79236_62_0.png)

如果你喜欢，还可以进行更多 `Apache Web` 服务器的配置。更详细的 `Apache` 设置可以在《`Red Hat Fedora and Enterprise Linux 4 Bible`》等书中找到。此外，`Apache` 本身带有一个详尽的在线手册，一旦你理解了基础知识将非常有用 (`http://localhost/manual`)。

## 检查并配置 Gallery

要检查基础设置是否正常工作，你可以运行 `Gallery` 配置向导。要运行向导，启动你的 Web 服务器并打开 `Gallery` `gallery/setup` 目录下的 `index.php` 文件。操作如下：

1. 启动 `Apache` 服务器，请以 `root` 用户输入：

```bash
### /etc/init.d/httpd start
```

2. 启动配置向导，使用任何浏览器打开 `Gallery` `setup` 目录下的 `index.php` 文件。例如，如果你的设置满足以下条件：
   - `Apache` 配置为允许用户从主目录下的 `public_html` 目录发布 Web 内容。
   - 用户名为 `chris` 的用户将 `Gallery` 安装到 `localhost` 上 `/home/chris/public_html` 中的 `gallery` 目录。

你将在浏览器的地址栏尝试以下内容来启动 `Gallery` 配置向导：

`http://localhost/~chris/gallery/setup/index.php`

图 3-1 显示了 `Gallery` 配置向导第一个屏幕的示例。

![](img/1b8a24a162893627b8005ac678b79236_63_0.png)

**图 3-1: 启动 `Gallery` 配置向导**

以下步骤描述了如何使用向导检查并设置 `Gallery`。

### 步骤 1：检查系统

在第一步中（如图 3-1 所示），系统检查页面将显示对运行 Linux 系统所需组件的检查结果。在继续之前，你应该修正页面上列出的问题。
