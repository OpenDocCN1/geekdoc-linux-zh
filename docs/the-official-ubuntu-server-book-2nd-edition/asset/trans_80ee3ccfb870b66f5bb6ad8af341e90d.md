
扩展节点就像设置常规 KVM 服务器一样。节点拥有的资源（RAM、CPU 和磁盘）越多，它能够托管的虚拟机就越多。

## 安装 UEC 前端服务器

安装前端服务器与安装其他任何 Ubuntu Server 实例一样简单。只需用 Ubuntu Server 光盘引导机器，在启动菜单中你会看到第二个选项是 Install Ubuntu Enterprise Cloud。选择该选项，然后按照标准的 Ubuntu 安装菜单完成安装。

安装进行到中途时，系统会询问几个问题，以便你配置 UEC。安装程序会自动探测网络，检查是否存在前端服务器；由于目前没有（因为我们正在设置它），安装程序默认会将此实例设置为前端服务器。接下来，系统会要求你为集群命名，最后你必须提供一段 IP 地址范围，供前端服务器分配给你创建的实例。请务必选择一段未被任何其他机器使用的 IP 地址范围，并且该范围要包含你的前端服务器和节点。最后，完成安装并重新启动进入你的新服务器。

## 安装 UEC 节点服务器

设置节点服务器比安装前端服务器还要简单。只需用 Ubuntu Server 安装光盘引导节点服务器，并从启动菜单中选择 Install Ubuntu Enterprise Cloud。安装程序会自动检测你的前端服务器，并默认将该机器设置为节点。只需确认默认设置并完成安装即可。安装程序会自动管理节点在集群中的注册，因此一旦节点启动完成，你就可以获取凭据并管理你的 UEC 集群了。

## 管理你的云

服务器安装并运行后，下一步是从云中获取凭据，以便你能注册并管理它。所有将要使用该云的人都必须遵循相同的过程。

在你自己的电脑上（也可以选择在前端服务器本身上）打开 Web 浏览器，浏览到 https://frontendserver:8443。将 frontendserver 替换为你的前端服务器的主机名或 IP 地址。接受证书，并使用用户名和密码 admin 登录。首次登录时，你会进入一个首次配置界面，需要修改 admin 密码并设置一个要使用的联系电子邮件地址。完成此过程后，你将看到默认的 UEC 管理界面（图 9-7）。

在此界面上，你可以添加其他有权查看和管理云实例的用户，但你首先要做的应该是选择 Credentials（凭据）选项卡，并单击 Download Credentials（下载凭据）。然后，在本地机器上创建一个名为 ~/.euca 的目录，并将凭据解压到那里：

```
$ mkdir ~/.euca
$ cd ~/.euca/
$ unzip ~/Desktop/euca2-admin-x509.zip
Archive: ~/Desktop/euca2-admin-x509.zip
To setup the environment run: source /path/to/eucarc
inflating: eucarc
inflating: cloud-cert.pem
inflating: jssecacerts
inflating: euca2-admin-9f543bf5-pk.pem
inflating: euca2-admin-9f543bf5-cert.pem
```

![](img/304f637afcecc491b152ee8ac5afadee_383_0.png)

图 9-7 选中 User 选项卡时的 Ubuntu Enterprise Cloud 管理界面

最后，在管理你的云之前，你需要在已下载并解压凭据的机器上安装 euca2ools 软件包，并测试凭据是否可用：

```
$ sudo apt-get install euca2ools
$ . ~/.euca/eucarc
$ euca-describe-availability-zones verbose
AVAILABILITYZONE	cluster1	192.168.0.74
AVAILABILITYZONE	|- vm types	free / max	cpu	 ram	disk
AVAILABILITYZONE	|- m1.small	0002 / 0002	1	192	2
AVAILABILITYZONE	|- c1.medium	0002 / 0002	1	256	5
AVAILABILITYZONE	|- m1.large	0001 / 0001	2	512	10
AVAILABILITYZONE	|- m1.xlarge	0001 / 0001	2	1024	20
AVAILABILITYZONE	|- c1.xlarge	0000 / 0000	4	2048	20
```

## 安装新服务器镜像

终于，你可以在集群上设置第一个服务器了。回到 https://frontendserver:8443 的 Web 界面，并选择 Store（商店）选项卡。Store（商店）选项卡列出了许多已经为你构建好的服务器镜像。你只需选择 Install（安装），镜像就会下载到你的本地集群。镜像下载完成后，点击 Install 按钮下方出现的“如何运行？”链接，获取有关如何运行该镜像的说明（图 9-8）。

![](img/304f637afcecc491b152ee8ac5afadee_384_0.png)

图 9-8 UEC Store 正在下载 Karmic i386 镜像
