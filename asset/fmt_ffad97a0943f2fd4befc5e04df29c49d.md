
address 10.10.10.2

netmask 255.255.255.0

broadcast 10.10.10.255

gateway 10.10.10.1

dns-namesvers 10.10.10.100

auto br100

iface br100 inet static

bridge_ports eth1

bridge_stp off

bridge_maxwait 0

bridge_fd 0

address 192.168.3.1

netmask 255.255.0.0

broadcast 192.168.255.255

重启网络：

```
localadmin@turing~$: sudo /etc/init.d/networking restart
```

由于这台服务器将作为所有节点的网络时间协议（NTP）服务器，它需要同步到官方 NTP 服务器。安装 NTP 服务器：

```
localadmin@turing~$: sudo apt-get install ntp
```

配置其即使在未连接互联网时也能提供服务，请在 `/etc/ntp.conf` 中包含以下两行：

```
server 127.127.1.0
```

```
fudge 127.127.1.0 stratum 10
```

重启 NTP 服务使更改生效：

```
localadmin@turing~$: sudo /etc/init.d/ntp restart
```

安装 Glance：

```
localadmin@turing~$: sudo apt-get install glance
```

安装 MySQL Server：

```
localadmin@turing~$: sudo apt-get install -y mysql-server
```

配置 MySQL。首先，编辑 `/etc/mysql/my.cnf` 将绑定地址更改为以下内容：

```
bind-address = 0.0.0.0
```

重启 MySQL 服务器：

```
localadmin@turing-$: sudo restart mysql
```

将这些步骤中的密码替换为您的 MySQL 密码。如果您在 MySQL 安装过程中没有设置密码，请现在设置一个：

```
localadmin@turing-$$: mysqladmin -u root password secretpassword
```

创建一个名为 nova 的数据库：

```
localadmin@turing-$$: sudo mysql -uroot -psecretpassword -e 'CREATE DATABASE nova;'
```

允许 root 从任何 IP 登录：

```
localadmin@turing-$$: sudo mysql -uroot -psecretpassword -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;"
```

为从任何 IP 登录的 root 设置 MySQL 密码：

```
localadmin@turing-$$: sudo mysql -uroot -psecretpassword -e "SET PASSWORD FOR 'root'@'%' = PASSWORD('secretpassword');"
```

安装 Nova 组件：

```
localadmin@turing-$$: sudo apt-get install -y rabbitmq-server nova-common nova-doc python-nova nova-api nova-network nova-volume nova-objectstore nova-scheduler nova-compute
```

安装 euca2ols：

```
localadmin@turing-$$: sudo apt-get install -y euca2ols
```

安装 unzip：

```
localadmin@turing~$: sudo apt-get install -y unzip
```

将 `/etc/nova/nova.conf` 的内容替换为如下：

```
-- dhcpbridge_flag=/etc/nova/nova.conf
-- dhcpbridge=/usr/bin/nova-dhcpbridge
-- logdir=/var/log/nova
-- lock_path=/var/lock/nova
-- state_path=/var/lib/nova
-- verbose
-- s3_host=10.10.10.2
-- rabbit_host=192.168.3.1
-- cc_host=192.168.3.1
```

启用 iscsitarget：

```
localadmin@turing$: sudo sed -i 's/false/true/g' /etc/default/iscsitarget
```

重启 iscsitarget 服务：

```
localadmin@turing~$: sudo service iscsitarget restart
```

创建物理卷（使用前面的步骤之一创建的 Linux VM 分区，此处用 `/dev/sda6` 表示；您的位置可能不同）：

```
localadmin@turing~$: sudo pvcreate /dev/sda6
```

创建一个名为 nova-volumes 的卷组：

```
localadmin@turing~$: sudo vgcreate nova-volumes /dev/sda6
```

创建一个名为 nova 的组：

```
localadmin@turing~$: sudo groupadd nova
```

更改 `/etc/nova/` 的所有者以及 `/etc/nova/nova.conf` 的权限：

```
localadmin@turing~$: sudo chmod -R root:nova /etc/nova
localadmin@turing~$: sudo chmod 644 /etc/nova/nova.conf
```

重启所有 nova 相关的服务：

```
localadmin@turing~$: sudo /etc/init.d/libvirt-bin restart
-> nova-network; sudo restart nova-compute; sudo restart nova-api; sudo restart
-> nova-objectstore; sudo restart nova-scheduler; sudo restart nova-volume;
-> sudo restart glance-api; sudo restart glance-registry
```

在 MySQL 数据库中创建 nova 架构：

```
localadmin@turing~$: sudo nova-manage db sync
```

在 nova.conf 内部创建用于网络的固定 IP 列表：

```
localadmin@turing~$: sudo nova-manage network 192.168.3.0/24
```

从 10.10.10.255 开始为实例分配公 IP 地址：

```
localadmin@turing~$: sudo nova-manage floating create 10.10.10.255/27
```

在 nova 上创建一个 admin 权限的用户：

```
localadmin@turing~$: sudo nova-manage user admin
```

创建一个名为 proj 的项目：

```
localadmin@turing~$: sudo nova-manage project create proj
```

创建下载 nova 文件的目录：

```
localadmin@turing~$: mkdir /home/localadmin/creds
```

生成访问和管理云的凭据：

```
localadmin@turing~$: sudo nova-manage project zip /home/localadmin/creds/nova.zip
```

你需要 `nova.zip` 文件。必须将其复制到想要运行 `nova-manage` 命令的任何机器。

进入 creds 文件夹并解压 zip 内容：`cert.pem`, `nova.pem` 和 `pk.pem`。

```
localadmin@turing~$: cd /home/localadmin/creds
unzip nova.zip
sudo chown localadmin:localadmin /home/localadmin/creds
```

`nova.pem` 包含在使用某些 `nova-manage` 命令前必须识别的环境变量。通过源文件来设置它们：

```
localadmin@turing~$: source /home/localadmin/creds/nova.pem
```

重启所有 nova 相关的服务：

```
localadmin@turing~$: sudo /etc/init.d/libvirt-bin restart; sudo restart nova-network; sudo restart nova-compute; sudo restart nova-api; sudo restart nova-objectstore; sudo restart nova-scheduler; sudo restart nova-volume; sudo restart glance-api; sudo restart glance-registry
```

确认凭据已应用且 nova 设置正确：

```
localadmin@turing~$: nova-manage describe-availability-zones verbose
```

如下所示输出将确认安装正确：

```
AVAILABILITYZONE - available
AVAILABILITYZONE - nova-compute
AVAILABILITYZONE - nova-scheduler
AVAILABILITYZONE - nova-network
AVAILABILITYZONE - nova-volume
```

最后的任务是设置 Ubuntu/OpenStack dashboard，这是一个用于管理的 Web 界面。安装 Bazaar，以便从 Launchpad 下载所需的软件：

```
localadmin@turing~$: sudo apt-get install -y bzr
localadmin@turing~$: sudo easy-install virtualenv
```

从 Launchpad 匿名检出 OpenStack dashboard 代码：

```
localadmin@turing~$: sudo bzr init-repo
localadmin@turing~$: sudo bzr branch lp:openstack-dashboard -r 6 /opt/osdb
localadmin@turing~$: cd /opt/osdb
localadmin@turing~$: sudo sh run_tests.sh
localadmin@turing~$: cd openstack-dashboard
```

编辑 `/opt/osdb/openstack-dashboard/local/settings.py` 以包含连接 nova-api 的所需的。您的安装详情可以在之前创建的 `nova.pem` 文件中找到，并与这些密钥不同：

```
NOVA_DEFAULT_ENDPOINT = 'http://localhost:8773/services/Cloud/'
NOVA_DEFAULT_REGION = 'nova'
NOVA_ACCESS_KEY = 'b6a7e3ca-f894-473b-abca-84329d92fa-proj'
NOVA_SECRET_KEY = 'd261a361-965a-4ed6-966a-d9f54b25531'
NOVA_ADMIN_USER = 'novaadmin'
NOVA_PROJECT = 'proj'
```

为了让 dashboard 发送通知邮件，需要配置邮件传输协议（SMTP）。现在现在。

进一步编辑 `/opt/osdb/openstack-dashboard/local/settings.py` 以包含连接邮件服务器所需的详情，根据需要进行自定义：

```
EMAIL_HOST = 'turing.example.com'
EMAIL_PORT = 25
EMAIL_USER = ''
EMAIL_PASSWORD = ''
EMAIL_TLS = 'True'
```

为 dashboard 创建数据库。在提示时，提供创建用于 dashboard 的管理员账户所需的名称、电子邮件地址和密码：

```
localadmin@turing~$: sudo tools/venv.sh dashboard/manage.py syncdbd
```

启动默认 Django 服务器，指定你希望 dashboard 可用的端口。此示例使用 8000：

```
localadmin@turing~$: sudo tools/venv.sh dashboard/manage.py runserver -- 10.10.10.2:8000
```

通过打开浏览器并打开此 URL 来测试安装：

```
http://10.10.10.2:8000
```

如果一切正常，你将能够使用刚才创建的凭据登录。其他人将能够访问界面创建账户，在授予访问之前必须由现有管理员批准。

默认情况下，dashboard 使用 SQLite。使用 MySQL 或 PostgreSQL 的说明可以从 http://cloud.ubuntu.com 获取。

# 准备服务器 2

从用于服务器 1 的相同 64 位 Ubuntu 11.10 服务器启动物理服务器。从菜单中选择 Install Ubuntu Server 并继续基础安装，使用本节随后的特定自定义设置。

安装 bridge-utils：

```
localadmin@burroughs~$: sudo apt-get install bridge-utils
```

将 `/etc/network/interfaces` 的内容替换为如下：

```
auto lo
iface lo inet loopback
auto eth0
```

# Ubuntu 云与 OpenStack

```
iface eth0 inet static
address 10.10.10.3
netmask 255.255.255.0
broadcast 10.10.10.255
gateway 10.10.10.1
dns-namesvers 10.10.10.100
auto br100
iface br100 inet static
bridge_ports eth1
bridge_stp off
bridge_maxwait 0
bridge_fd 0
address 192.168.3.2
netmask 255.255.0.0
broadcast 192.168.255.255
```

重启网络：

```
localadmin@burroughs-$: sudo /etc/init.d/networking restart
```

安装 NTP：

```
localadmin@burroughs-$: sudo apt-get install ntp
```

通过向 `/etc/ntp.conf` 中添加此行来配置 NTP 同步到服务器 1：

```
server 10.10.10.2
```

重启 NTP：

```
localadmin@burroughs-$: sudo /etc/init.d/ntp restart
```

该服务器正被准备作为计算节点，因此它只需要以下 nova 组件和依赖项：

```
localadmin@burroughs-$: sudo apt-get install -y nova-common python-novanova-compute vlan
```

安装 euca2：

```
localadmin@burroughs-$: sudo apt-get install -y euca2tools
```

安装 unzip：

```
localadmin@burroughs-$: sudo apt-get install -y unzip
```

# 第 32 章 云端 Ubuntu

用以下内容替换 `/etc/nova/nova.conf` 的内容：

```
--dhcpbridge flagfile=/etc/nova/nova.conf
--dhcpbridge=/usr/bin/nova-dhcpbridge
--logdir=/var/log/nova
--lock_path=/var/lock/nova
--state_path=/var/lib/nova
--verbose
--s3_host=10.10.10.2
--rabbit_host=192.168.3.1
--cc_host=192.168.3.1
--ec2_url=http://10.10.10.2:8773/services/Cloud
--fixed_range=192.168.0.0/16
--network_size=8
```
