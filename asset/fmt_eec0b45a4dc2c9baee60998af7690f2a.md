
```
install snd-intel8x0 /sbin/modprobe --ignore-install snd-intel8x0
&&
  /usr/sbin/alsactl restore >/dev/null 2&|1 || \
  remove-snd-intel8x0 ( /usr/sbin/alsactl store >/dev/null 2&|1 || ;\
  /sbin/modprobe -r --ignore-remove snd-intel8x0
alias usb-controller ehci-hcd
alias usb-controller ohci-hcd

## TWW: 这些是我为特定系统添加的
# I2C 模块选项
alias char-major-8 i2c-dev

# nvidia 内核模块
alias char-major-19 nvidia_1_0

# 设置 PVR (视频捕获)
alias char-major-20 video
alias char-major-21 deep
alias char-major-22 deep
alias char-major-23 tuner
alias char-major-24 tuner
## 添加此以修复 tuner 问题
options tuner=57,55 # 新用法
install /sbin/modprobe --ignore-install options once=1
# 如果使用 FireWire
install /sbin/modprobe --ignore-install ohci-hcd1394
```

现在处理了所有的硬件驱动，就可以进行最后的`MythTV`配置了。

## 配置并测试`MythTV`

现在你安装了`MythTV`和驱动，在使用`MythTV`之前需要执行以下操作：

- 为`MythTV`配置`MySQL`数据库
- 通过`zap2it.com`注册`MythTV`的频道数据（`DataDirect`）
- 配置`MythTV`后端和启动
- 配置`MythTV`前端和启动
- `KDE`特定调整

## 第 4 章 — 使用`MythTV`创建个人视频录像机

### 为`MythTV`配置`MySQL` Server

按照步骤为`MythTV`配置`MySQL` Server：

1. 检查是否已安装并准备就绪`MySQL`：

```
# rpm -qa|grep mysql
mysql-23.58-fc3
mysql-dev-23.58-fc3
mysql-server-23.58-fc3
```

版本可能有所不同，确保软件包已安装。同时验证`MySQL`服务已设置为启动时开启，并启动它：

```
# chconfig -list mysql
0:off 1:off 2:on 3:on 4:on 5:off
# /etc/init.d/mysql start
Starting MySQL...
```

2. 接下来，设置一个不容易忘记的`MySQL`密码（建议与系统`root`密码相同）：

```
# mysql -u root
mysql> UPDATE USER SET Password=PASSWORD('ROOT_PWD') WHERE user='root';
mysql> FLUSH PRIVILEGES;
mysql> quit
```

将`ROOT_PWD`改为你想要的`MySQL`密码。

3. 将`MythTV`架构导入`MySQL`：

```
# mysql -u root -p < /usr/share/doc/mythtv-0.18.1/database/mc.sql
ERROR 1064 at line 4: You have an error in your SQL syntax near 'TEMPORARY mythconn.* TO mythtv@localhost IDENTIFIED BY 'mythtv' at line 1
```

输入刚刚设置的`root`密码。第 4 行的错误 1064 可以忽略（如果你使用`Fedora Core 4`及更高版本则不会显示此错误）。

4. 现在你需要对`MySQL`服务器以及客户端进行一些更改。主服务器配置文件为`/etc/my.cnf`。编辑此文件，将`[mysql]`部分的内容大致匹配适用于`MySQL` 3.23（适用于`Fedora Core 3`）：

```
[mysql]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
### MySQL 3.23 的 MythTV 
set-variable = key_buffer = 16M
set-variable = table_cache = 128
set-variable = sort_buffer = 2M
set-variable = myisam_sort_buffer_size = 8M
```

# 108 第二部分 — 多媒体项目

如果你运行`Fedora Core 4`或更高版本，你可能运行的是`MySQL` 4.x，并将使用以下新增内容：

```
[mysql]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
### MySQL 4.x 的 MythTV 调整
key_buffer = 128
table_cache = 128
sort_buffer_size = 2M
myisam_sort_buffer_size = 8M
query_cache_size = 16M
```

5. 像所示重启`MySQL`服务器：

```
# /etc/init.d/mysqld restart
Stopping MySQL: [ OK ]
Starting MySQL: [ OK ]
```

现在你已经准备好设置在线频道数据服务，以便获取所有的本地频道列表。

### 设置`DataDirect`频道列表服务

`DataDirect`是由`zap2it.com`托管的免费互联网频道列表。它主要是一个免费服务，每三个月获取一次，用于偶尔填充他们的设备。这是`MythTV`获取频道列表的新方法。旧方法（每当他们更改`Web`界面的视觉外观时就需要重新设置）依赖于`libcurl`和屏幕爬取。

### 订阅`DataDirect`

要加入免费（无需付费）的服务，你只需要邮政邮编和几分钟时间（以及互联网连接）。如果指令不起，可能是`MythTV`的某些内容发生了变化。

1. 首先，使用浏览器访问`http://zap2it.com/`并点击 "New User? Sign-Up"。阅读许可协议并点击 "Accept"。
2. 在订阅注册屏幕上，输入来自`MythTV.org` `HOWTO`的证书代码：

`www.mythtv.org/docs/mythtv-HOWTO-5.html#ss5.30`

3. 填写问卷并点击 "Submit"。
4. 继续使用`Lollipop`向导，输入你的邮编和频道供应商，并开始选择你通过任何电缆/供应商套餐接收的频道（见图 4-5）。记住这个`zap2it.com`服务的用户名和密码，因为你将调整`MyTV`配置以从互联网拉取频道列表。

## 第 4 章 — 使用`MythTV` 10 创建个人视频录制器

带有破折号（`-`）列出的节目为`HD`。如果你没有制作`HD`版`Myth`盒子，请勿选择`HD`频道。

![](img/1b8a24a162893627b8005ac678b79236_133_0.png)

![](img/1b8a24a162893627b8005ac678b79236_133_1.png)

图 4-5：在`Zap2it`的线路向导上选择频道数据

如果你没有始终开启的`Internet`连接，或者至少晚上无法从你的`MythTV`盒子启动调制号器`PPP`号，你仍然可能让它运行起来。系统的体验不会像始终连接的`MythTV`盒子那样完美。

![](img/1b8a24a162893627b8005ac678b79236_133_2.png)

### `/video/` 下所需的目录

在运行实际的`mythtvsetup`程序之前，你需要创建一些目录，`mythbackend`服务需要这些目录来存储在你观看电视和录制内容时存储在硬盘上的大文件。

1. 以`root`用户身份，在你的挂载的`/video/`文件系统目录下创建以下目录，并将每个目录的文件/目录权限设置为`777`，如下：

```bash
# mkdir /video/buffer; chmod 777 /video/buffer
# mkdir /video/mythmusic; chmod 777 /video/mythmusic
# mkdir /video/.mythtv; chmod 777 /video/.mythtv
```

直到`/video/`目录下拥有以下目录为止：
