
许多树莓派指南的主题都围绕树莓派本身的大小和便携性展开，这使得它能够接管过去需要使用台式或小型计算机才能完成的任务。拥有一个私有云是树莓派能力的另一个极佳应用场景，因为你可以将它藏在某个隐蔽的地方，日常维护需求极低。请确保投资一些优质的便携 `USB` 存储设备（如外部 `HDD`），并在此过程中为您的树莓派准备一个外壳。

![](img/daaca9116bc2b1db669c224de81abc7c_59_1.png)

### 所需材料

- 外部存储设备
- 稳定的互联网连接

> `左图` 您可以将云存储在自己的家中，而不是将所有媒体和文件存储在位置未知的云服务器上。

### 01 设置静态 `IP`

在设置好有线或无线网络连接后，您需要将其设置为静态 `IP`。使用 `sudo nano /etc/network/interfaces` 打开网络设置文件。找到 `iface eth0` 行，以便对其进行修改和添加：

```
iface eth0 inet static
address 192.168.0.50
gateway 192.168.0.1
netmask 255.255.255.0
network 192.168.0.0
broadcast 192.168.0.255
```

### 02 安装大量软件

您需要 `Apache` 软件和 `PHP`。使用以下命令安装所需的一切：

```
$ sudo apt-get install apache2 php5 php5-json php5-gd php5-sqlite curl libcurl3 libcurl4-openssl-dev php5-curl php5-gd php5-cgi php-pear php5-dev build-essential libpcre3-dev libapache2-mod-php php-apc
```

### 03 设置 `PHP` 加速器

使用 `sudo pecl install apc` 安装您的加速器，并为其创建一个 `ini` 文件。为此，请使用 `sudo nano /etc/php5/cgi/conf.d/apc.ini`，然后向文件中添加以下内容：

```
extension=apc.so
apc.enabled=1
apc.shm_size=30
```

![](img/daaca9116bc2b1db669c224de81abc7c_60_1.png)

### 04 配置文件限制

使用 `sudo nano /etc/php5/apache2/php.ini` 进入 `Apache` 配置文件。这是一个很大的文件，但您需要找到两个文件大小选项，并按照下文添加第三个扩展选项：

```
upload_max_filesize = 2048M
post_max_size = 2200M
extension = apc.so
```

### 05 设置 `SSL`

首先，您需要在 `Apache` 中启用 `SSL`；使用 `sudo nano /etc/apache2/sites-enabled/000-default` 将 `AllowOverride` 选项中的 `"None"` 更改为 `"All"`。然后执行以下两个命令：

```
$ sudo a2enmod rewrite
$ sudo a2enmod headers
```

### 06 完成 `Apache` 配置

现在您需要执行两组命令：一组大型命令（需要一些信息）以及重启命令：

```
$ sudo openssl genrsa -des3 -out server.key 1024
$ sudo openssl rsa -in server.key -out server.key.insecure
$ sudo openssl req -new -key server.key -out server.csr
$ sudo openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
$ sudo cp server.crt /etc/ssl/certs; sudo cp server.key /etc/ssl/private; sudo a2enmod ssl
$ sudo a2ensite default-ssl
$ sudo service apache2 restart
```

### 07 下载并安装 `ownCloud`

在这里，您有一系列要运行的命令，用于下载、解压并将 `ownCloud` 安装到正确的位置：

```
$ wget https://download.owncloud.org/community/ownCloud-7.0.0.tar.bz2
$ sudo tar -xjf owncloud-7.0.0.tar.bz2
$ sudo cp -r owncloud /var/www
```

### 08 `ownCloud` 权限

确保您的硬盘已连接并按您想要的方式挂载。首先，授予 `Web` 服务器使用 `ownCloud` 的权限：

```
$ sudo chown -R www-data:www-data /var/www/owncloud/
```

接下来，使用 `sudo nano /var/www/owncloud/.htaccess` 并进行与上述 `php.ini` 文件相同的更改。最后，使用以下命令授予挂载硬盘位置的权限：

```
$ sudo chown -R www-data:www-data [mount]
```

![](img/daaca9116bc2b1db669c224de81abc7c_60_2.png)

### 09 设置 `ownCloud`

打开 `Midori` 并导航到 `https://[ipaddress]/owncloud` 以开始 `ownCloud` 设置过程。您需要做的第一件事是将数据位置更改为外部驱动器的挂载点，这可以在高级选项中找到。完成！

### 获取灵感

需要关于下一步该做什么的创意吗？看看我们的媒体投射教程，也许您可以将这两个概念融合在一起。将视频上传到您的云中，并在网络上播放它们。

![](img/daaca9116bc2b1db669c224de81abc7c_61_0.png)

## `AirPi`

使用自己的传感器站预测天气

`AirPi` 的出身背景与树莓派基金会的使命完美契合。该项目由两名高中生创建，旨在测量各种形式的污染。得益于树莓派基金会的一些宣传，该项目的 `popularity` 迅速爆发，如今它已成为在树莓派上创建气象站的首选方式。

`AirPi` 套件默认附带少量传感器，可以通过额外的分线板和模块进行升级和改进。套件中包含气压传感器、湿度和温度传感器、紫外线辐射传感器以及用于噪声污染的麦克风。

您需要做的第一件事是组装套件，这需要一把焊台和稳定的双手。套件附带一些基本说明，您可以遵循，但查看一些在线图片以弄清楚每个组件的具体位置也无妨。焊接所有电阻器时要小心，确保不要熔化底部的 26 针连接器，否则它将无法安装到您的树莓派上。

完成后，您需要开始设置树莓派。打开终端并获取您将要使用的一些 `Python` 工具：

```
$ sudo apt-get install git-core python-dev python-pip python-snibus
```

下载并安装 `python-eeml` 包：

```
$ sudo apt-get install libxml2-dev libxslt-dev python-lxml
$ git clone https://github.com/peterivi/python-eeml.git
$ cd python-eeml
$ sudo python setup.py install
```

您需要为压力传感器安装 `i2c` 支持，因此首先使用 `sudo nano /etc/modprobe.d/raspi-blacklist.conf` 并移除黑名单 `i2c-bcm2708` 行的注释。

接下来，使用 `sudo nano /etc/modules` 打开模块文件，并在文件底部添加 `i2c-dev`。保存并安装：

```
$ sudo apt-get install i2c-tools
```

使用以下命令将您的 `Pi` 添加到 `i2c` 用户组：

```
$ sudo adduser pi i2c
```

在继续之前，请重新启动您的树莓派。最后，使用以下命令安装最终的 `Python` 模块：

```
$ sudo apt-get install python-smbus
```

现在我们可以安装 `AirPi` 代码。仍在终端中，使用：

```
$ git clone -b non-modular https://github.com/tonmharcley/AirPi.git
```
