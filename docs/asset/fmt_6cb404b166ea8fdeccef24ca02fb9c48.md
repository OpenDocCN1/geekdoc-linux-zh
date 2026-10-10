
`sudo raspi-config`

步骤 7：选择选项 3：启用启动到桌面/Scratch 并按回车键。这将进入图 7.11 所示的“启动选项”窗口。选择第二个选项。

步骤 8：使用键盘选择 `Finish`，系统将重启，如图 7.12 所示。
步骤 9：通过输入以下命令更新到最新固件：

```
sudo rpi-update
```

### 7.1.1.2 安装 Raspberry Pi 摄像头

要启用摄像头，我们必须将摄像头模块物理安装在电路板上。
步骤 1：如图 7.13 所示进行初始设置。摄像头模块的银色接口应朝上。
步骤 2：将银色接口朝上的支架滑动到位置。如图 7.14 和 15 所示，将支架卡回原位。
软件安装，请按照以下步骤操作。
步骤 1：启动 Raspberry Pi。
步骤 2：打开终端并运行

```
sudo raspi-config
```
选择启动选项
控制台文本，需要登录（默认）
以用户 `pi` 登录桌面
启动时启动 Scratch 编程环境
`<Ok>` `<Cancel>`

图 7.11 Raspberry Pi 启动选项

![](img/21e96ea63cf1b8de0bc286a38acbcfc4_372_0.png)

图 7.12 Raspberry Pi 桌面

如果没有“camera”选项，运行

```
sudo apt-get update
sudo apt-get upgrade
```

运行配置命令

```
sudo raspi-config
```

现在你应该看到“camera”选项了。

![](img/21e96ea63cf1b8de0bc286a38acbcfc4_373_0.png)

图 7.13 初始设置

![](img/21e96ea63cf1b8de0bc286a38acbcfc4_373_1.png)

图 7.14 Raspberry Pi 摄像头

步骤 3：导航到“camera”选项并启用它（见图 16）。然后选择 `<Finish>` 并重启 Raspberry Pi。要以 jpeg 格式捕图像，在终端输入：

```
raspill -o image.jpg
```

注意“image”是图像名称。

![](img/21e96ea63cf1b8de0bc286a38acbcfc4_374_0.png)

图 7.15 带有摄像头的 Raspberry Pi

| info | 关于此工具的信息 |
| --- | --- |
| expand_roots | 扩展根分区填充 SD 卡 |
| overscan | 更改过扫描 |
| configure_keyboard | 设置键盘布局 |
| change_pass | 更改 'pi' 用户的密码 |
| change_locale | 设置区域设置 |
| change_timezone | 设置时区 |
| change_hostname | 设置主机名 |
| memory_split | 更改内存划分 |
| overclock | 配置超频 |
| ssh | 启用或禁用 ssh 服务器 |
| boot_behaviour | 启动时启动桌面？ |
| camera | 启用/禁用摄像头 |

图 7.16 启用摄像头

### 7.1.1.3 设置 Wi-Fi 以实现 Raspberry Pi 远程控制

虚拟网络计算（VNC）是一种桌面共享系统，允许从任何计算机远程控制桌面。在此设置中，可以访问 Raspian OS 对 Raspberry Pi 进行必要的更改。如果缺少 VNC，则使用以下步骤。注意最新的 Raspberry Pi 自带 VNC。

步骤 1：打开终端并安装 TightVNC 包

```
sudo apt-get install tightncserver
```

步骤 2：运行 TightVNC Server 会提示输入密码和一个可选的只读密码：`tightvserver`。

步骤 3：输入

```
vncserver :1
```

步骤 4：安装 VNC 客户端：

```
sudo apt-get install xtightncviewer
```

步骤 5：查找 Raspberry Pi 的 IP 地址：

```
ifconfig
```

记录下作为本地 IP 地址的“inet addr”。

步骤 6：在连接到 Raspberry Pi 的笔记本电脑上，从此网站下载 VNC 软件：

http://tightvnc.com/download.php

步骤 7：安装软件。

步骤 8：设置完成后，打开 TightVNC 客户端，在“Remote Host”框中输入 IP 地址并在后面添加 ":1”。输入初始设置中选择的密码并点击“connect”。完成后，将显示 Raspberry Desktop。

### 7.1.1.4 从 Raspberry Pi 远程复制文件

FileZilla 使用 SSH 传输通过 Raspberry Pi 传输文件

步骤 1：从此链接下载 FileZilla

https://filezilla-project/

步骤 2：如图 7.17 所示加载程序。

步骤 3：点击 `File -> Site Manager`，如图 7.18 所示。

步骤 4：输入主机和端口信息。协议应改为 `SFTP - SSH` 文件传输协议，登录类型应为标准。输入用户和密码（User: `pi`, Password: `Raspberry`）然后连接。此时，可以看到工作桌面和 Raspberry Pi 目录中的文件。WinSCP 可以代替 FileZilla。可以从 https://winscp.net/eng/download.php 下载。

### 7.1.1.5 远程控制 Raspberry Pi 终端

TTY 客户端允许通过相同的 SSH 连接由计算机远程控制 Raspberry Pi 终端。可以从此处下载：http://www.chiark.greenend.org.uk/~sgatham/putty/download.html

如果使用 `tightncserver` 的自动脚本不起作用。

### 7.1.1.6 设置数据库和 PHP 网页

Apache 是一种可以安装在 Raspberry Pi 上的 Web 服务器应用程序。Apache 可以通过 HTTP 提供 HTML 文件，并带有额外的模块，可以使用 PHP 等脚本语言提供动态网页服务。

## 360 不确定环境下的嵌入式机电系统设计

![](img/21e96ea63cf1b8de0bc286a38acbcfc4_376_0.png)

图 7.17 FileZilla GUI

![](img/21e96ea63cf1b8de0bc286a38acbcfc4_376_1.png)

图 7.18 FileZilla 输入 SSH 信息

## 树莓派嵌入式系统设计 366

第 1 ：安装 Apache

```
sudo apt-get install apache2 -y
```

第 2 ：默认情况下，安装 Apache 会在网页文件夹 `www` 创建测试 HTML 文件。可以通过 `http://localhost/` 或 `http://192.168.1.16`（取决于树莓派的 IP 地址）访问默认网页。

第 3 ：通过浏览器访问第 2 步中的网页。会出现 Apache2 Debian 默认页面。

HTML 文件是用于操作以更改网页设计的文件。它位于树莓派目录下的 `/var/www/html/index.html`。默认情况下，HTML 目录和 `index.html` 都由用户“root”所有。输入以下命令更改所有者以权限：

```
sudo chown pi:data index.html
```

允许 Apache 服务器处理 PHP 文件，安装 PHP5 和 Apache 的 PHP5 模块。输入以下命令安装：

```
sudo apt-get install php5 libapache2-mod-php5 -y
sudo rm index.html
sudo nano index.php
```

创建一些 PHP 内容进行显示：

```php
<?php echo "hello world"; ?>
```

现在访问网页将看到白色页面上打印出 hello world。PHP5 和 Apache2 已安装完成。使用 MySQL 设置了数据库管理系统来存储和维护数据。由于训练分类图像需要大量的图像数据库，因此创建此 Web 服务器是为了邀请他人提高分类准确性。相比之下，PhpMyAdmin 为用户提供了一个易用的界面。

- PhpMyAdmin: https://www.siteground.com/tutorials/phpmyadmin/phpmyadmin_create_database.html

- 数据库: http://www.onlinebuff.com/article_step-by-step-to-upload-an-image-and-store-in-database-using-php_40.html
