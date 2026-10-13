
- 点击“属性”。

![](img/d549b948a29b14d0d8313a8ed09b5698_163_2.png)

- 点击“共享”。

![](img/d549b948a29b14d0d8313a8ed09b5698_163_3.png)

- 点击“确定”。

![](img/d549b948a29b14d0d8313a8ed09b5698_163_4.png)

- 重启系统。

![](img/d549b948a29b14d0d8313a8ed09b5698_163_5.png)

# 8.4 共享到 Windows PC 的打印机

## 3 显示打印机。

按照以下顺序打开：

## 5 输入打印机名称。

- 点击“共享”
- 输入打印机名称。

![](img/d549b948a29b14d0d8313a8ed09b5698_164_0.png)

## 4 选择要的打印机。

- 右键点击要共享的打印机。

![](img/d549b948a29b14d0d8313a8ed09b5698_164_1.png)

- 点击“属性”
- 点击“共享”。

![](img/d549b948a29b14d0d8313a8ed09b5698_164_2.png)

- 点击“确定”图标。

显示了硬盘形状的共享打印机。

![](img/d549b948a29b14d0d8313a8ed09b5698_164_3.png)

## 网页是如何显示的

`Apache`

Web 是互联网上最熟悉的服务。网页由 Web 服务器提供。当安装红帽 Linux 时，系统也会自动安装一个名为 *Apache* 的 Web 服务器。`Apache` 在 Linux 中表现为一个特殊的目录，作为文档根（网页根）。将文件放置在此目录中，允许它们作为网页被查看。如果你共享该目录，就可以从个人电脑（PC）创建网页。

## 网页是如何工作的

来自 CoriolisOpen Press 出版社 CoriolisOpen 系列书籍的网页。

![](img/d549b948a29b14d0d8313a8ed09b5698_167_0.png)

传输的文件将显示在浏览器中。

## URL 的含义

| 用于打开网页的协议标记。 | 主机主机名称（IP 地址也有效）。 | 目录名和文件名（要显示的页面文件）。 |
| :--- | :--- | :--- |

```
http://coriolis.com/books/CoriolisOpen/index.htm
```

访问 URL 时所指定的路径地址将显示在 Web 浏览器的地址栏中。红帽 Linux 配备了 Web 服务器功能（`Apache`），用于提供网页。

# 9.1 网页是如何显示的

## Apache 的角色

## Linux 中分配给 Web 选的特殊目录

在计算机的浏览器中输入以下 URL 以连接到网络并显示 Apache 网页。

![](img/d549b948a29b14d0d8313a8ed09b5698_168_0.png)

成功了！

如果你看到这条消息，说明到 Web 上的 `Apache` 的连接已成功。你现在可以向此目录添加 HTML 内容并刷新页面了。

```
http://192.168.1.1/
```

如果你看到错误消息“无法连接到服务器”（Unable to connect to the server），请检查你的网络连接并确保 `Apache` 服务正在运行，且没有防火墙拦截它。

| Linux 电脑（通过 IP 地址指定） | `Apache` 已设置为此网页的根目录。 |
| :--- | :--- |

根目录已按默认设置安装。有关 HTTP Linux 的文档和信息，请参阅 `Apache` 服务器官方网站。

## Apache 分配的文档根目录

```
http://192.168.1.1/
```

此目录等同于文档根。

```
/home/httpd/html
```

例如，打开文件 `/home/httpd/html/manual/index.html` 的 URL 如下所示：

```
http://192.168.1.1/manual/index.html
```

| Linux 电脑（通过 IP 地址指定） | 相对路径 `/home/httpd/html`。 |
| :--- | :--- |

如果分配给此根的目录 `/home/httpd/html` 被 `Samba` 或 `netatalk` 共享，那么任何人都可以创建网页。

> 注意：请使用第 5 章介绍的 DHCP 服务器将其他个人电脑连接到网络。除非提前进行设置，否则这些电脑无法正常连接。

## 自定义你的 Web 服务器

### 修改设置文件

`Apache` 设置文件位于 `/etc/httpd/conf` 目录。它们被分为三个文件：`access.conf`、`httpd.conf` 和 `srm.conf`。可以通过编辑这些文件更改 `Apache` 设置。

本节将检查 `Apache` 的基本设置、如何更改它们以及如何验证此操作。每次更改设置后，必须重启 `Apache`。

### 修改文档根目录

- 1 创建目录。

输入命令。

```bash
[root@server /root]# mkdir /usr/local/www
[root@server /root]#
```

- 2 编辑 `srm.conf`。

输入命令。

```bash
[root@server /root]# mkdir /usr/local/www
[root@server /root]# vi /etc/httpd/conf/srm.conf
```

`DocumentRoot`: 你从中提供文档的目录。默认情况下，所有请求都从此目录中获取，但可以使用符号链接和别名（`aliases`）指向其他位置。

`DocumentRoot /home/httpd/html`

更改为准备好的目录，保存并退出。

`DocumentRoot`: 你从中提供文档的目录。默认情况下，所有请求都从此目录中获取，但可以使用符号链接和别名（`aliases`）指向其他位置。

`DocumentRoot /usr/local/www`

# 9.2 自定义你的 Web 服务器

- 3 编辑 `access.conf`。

输入命令。

```bash
# 这应该更改为你设置的任何 DocumentRoot 值。
<Directory /home/httpd/html>

# 这应该更改为你设置的任何 DocumentRoot 值。
<Directory /usr/local/www>
```

更改为准备好的目录，然后保存并退出。

- 4 重启 `Apache`。

切换目录。输入命令。

```bash
[root@server /]# cd /etc/rc.d/init.d
[root@server init.d]# ./httpd restart
Shutting down http: httpd
Starting http: httpd
[root@server init.d]#
```

## 将特殊目录分配给文档根的子目录

- 1 编辑 `srm.conf`。

输入命令。

```bash
[root@server #]# vi /etc/httpd/conf/srm.conf
# 注意，如果在文件名末尾包含斜杠，服务器将要求在 URL 中包含它。
# 在此例中没有使用别名。
Alias /icons/ /home/httpd/
```

- 2 写入要添加的目录。

# 注意，如果在文件名末尾包含斜杠，服务器将要求在 URL 中包含它。

# 在此例中没有使用别名。

`Alias /icons/ /home/httpd/`

添加用于 Web 的名称和 Linux 目录名，然后保存并退出。

- 3 重启 `Apache`。

输入命令。

```bash
[root@server ~]# cd /etc/init.d/
[root@server ~]# ./httpd restart
Shutting down http: httpd
Starting http: httpd
```

## 添加新索引文件

# 编辑 `srm.conf`。

输入命令。

```bash
[root@server ~]# vi /etc/httpd/conf/srm.conf
```

# `DirectoryIndex`: 作为默认页的文件或文件。

# 如果列出了多个文件，将使用第一个存在的。

`DirectoryIndex index.html`

# 如果列出了多个文件，将使用第一个存在的。

`DirectoryIndex index.html index.cgi`

## 修改 Linux 用户的目录

- 2 重启 `Apache`。

切换目录。输入命令。

```bash
[root@server /root]# cd /etc/rc.d/init.d
[root@server init.d]# ./httpd restart
Shutting down http: httpd
Starting http: httpd
[root@server init.d]#
```

## 为每个用户创建网页

# 创建网页的目录。
