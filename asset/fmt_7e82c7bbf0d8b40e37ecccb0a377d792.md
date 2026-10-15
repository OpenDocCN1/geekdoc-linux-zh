
```
jesse@Punjabism ~ $ sudo /opt/lampp/lampp stop
password for user:
Stopping XAMP for Linux 1.7.1..
XAMP: Stopping Apache with SQL...
XAMP: Stopping MySQL...
XAMP: Stopping ProFTPD...
stopping done.
jesse@Punjabism ~ $ sudo /opt/lampp/lampp start
Starting XAMP for Linux 1.7.1..
XAMP: Starting Apache with SQL (and MySQL)...
XAMP: Starting MySQL...
XAMP: Starting ProFTPD...
OK.
XAMP for Linux started.
```

![](img/4a38974b8034a42576d180572f120df8_29_0.png)

好了，现在目标达成。

刷新你的浏览器页面

出于安全考虑，它将要求你移除 `settings.php` 文件的写入权限。让我们这样做：

打开终端，输入以下命令：

```
jesse@Punjabism ~ $ sudo chmod a-w /opt/lampp/htdocs/drupal/sites/default/settings.php
```

### 终端

```
jesse@Panjabim ~$ sudo /opt/lampp/lampp stop
[sudo] password for jesse:
stopping XAMP for Linux 1.7.1...
XAMP: Stopping Apache with SSL...
XAMP: Stopping MySQL...
XAMP: Stopping ProFTPD...
jessie@Panjabim ~$ sudo /opt/lampp/lampp start
Starting XAMP for Linux 1.7.1...
XAMP: Starting Apache with SSL (and PHP)...
XAMP: Starting MySQL...
XAMP: Starting ProFTPD...
jessie@Panjabim ~$ sudo chmod a-w /opt/lampp/htdocs/drupal/sites/default/settings.php
jessie@Panjabim ~$ _
```

![](img/4a38974b8034a42576d180572f120df8_30_0.png)

刷新浏览器后，你将看到网站的主页

## 大功告成……!!!

你做到了..

现在，你可以在本地电脑上开始构建你的网站了。

## XAMPP 服务的自动启动

但每次启动电脑时，你都要通过在终端窗口输入命令（`sudo /opt/lampp/lampp start`）来启动 Xampp 服务器，我正尝试让这对每个人变得简单。你应该将 Xampp 服务放入启动项，这样每当你启动电脑时，Xampp 服务器就会自动启动。为了实现这一点，你需要按照以下步骤操作。

- 1. 首先，找到你的默认运行级别（run level），它实际上是系统在启动时加载启动服务的文件夹。

![](img/4a38974b8034a42576d180572f120df8_31_0.png)

打开终端并输入命令

```
jesse@Punjabizm / $ egrep :initdefault:/etc/init.d/
```

你不应该看到包含两个冒号之间的数字的行。

大多数情况下是 3 或 5（如果你使用的是 Debian）。在这里我选择 `rc3.d` 文件夹，因为我的电脑从那里加载启动配置。

- 2. 通过终端窗口输入命令进入配置启动项的目录

```
jesse@Punjabizm / $ cd /etc/rc2.d/
```

如果你的系统没有提供 `/etc/rc2.d`，请也尝试 `/etc/init.d/rc2.d` 和 `/etc/rc2.d`。现在在命令模式下输入以下命令。

```
jesse@Punjabizm /etc/rc2.d $ sudo ln -s /opt/lampp S99lampp
jesse@Punjabizm /etc/rc2.d $ sudo ln -s /opt/lampp K01lampp
```

![](img/4a38974b8034a42576d180572f120df8_32_0.png)

此命令将 Xampp 启动服务的快捷方式 `S99lampp` 和 `K01lampp` 放入 `/etc/rc2.d` 文件夹中。你也可以在 `rc2.d` 文件夹中看到它们。

![](img/4a38974b8034a42576d180572f120df8_33_0.png)

现在，当你的电脑启动或关机时，XAMPP 应该会自动启动和停止。

（这两个 CMS 的安装仅适用于 GNOME Linux 平台）

Rupinder singh Dhammu

HIIAS | Shimla

jesse@email.ru
