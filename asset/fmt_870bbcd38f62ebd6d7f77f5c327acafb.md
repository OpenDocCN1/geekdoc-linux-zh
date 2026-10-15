
在 `/etc/nagios3/objects.cfg` 中添加：

```bash
define service http {
    use generic-service
    host_name server02
    service_description HTTP
    check_command check_http!192.168.1.17
}
```

编辑 `/etc/nagios3/nagios.cfg` 以启用配置文件：

```bash
cfg_file_mode=/etc/nagios3/objects.cfg
```

或者，在 `/etc/nagios3/nagios.cfg` 中使用以下命令：

```bash
cfg_file_cfg=/etc/nagios3/objects/*.cfg
```

重启 nagios 服务：

```bash
sudo systemctl restart nagios
```

现在可以通过浏览器访问 `http://server01/nagios` 来查看监控状态。

# 检查 MySQL 服务器

```bash
define service {
    hostgroup_name mysql-servers
    service_description MySQL
    check_command check_mysql_cmdlinecreated! nagios! secret!
    use $HOSTADDRESS generic-service
    notification_interval 0 ; 如果你想接收通知，请将其设置为 > 0
}
```

需要定义一个 `mysql-servers` 主机组。编辑 `/etc/nagios3/conf.d/hostgroups_nagios2.cfg` 并添加内容：

```bash
# MySQL 主机组
define hostgroup {
    hostgroup_name mysql-servers
    alias MySQL servers
    members localhost, server02
}
```

Nagios 检查需要对 MySQL 进行身份验证。要向 MySQL 添加 nagios 用户，请输入：

```bash
mysql -u root -p -e "create user nagios identified by secret"
```

> 注意
>
> 添加 `mysql-servers` 主机组中的所有主机都需要该 nagios 用户。

重启 nagios 以开始检查 MySQL 服务器。

```bash
sudo systemctl restart nagios3.service
```

## 最后检查 NRPE 以检查 server02 上的磁盘空间

在 server02 上将服务检查添加到 `/etc/nagios3/conf.d/server02.cfg`：

```bash
# NRPE 磁盘检查.
define service {
    use generic-service
    host_name server02
    service_description nrpe-disk
    check_command check_nrpe_larg!check_all_disks
    !172.18.100.101
}
```

现在在 server02 上编辑 `/etc/nagios/nrpe.cfg` 并修改：

```bash
allowed_hosts=172.18.100.100
```

并在下方的定义区域添加：

```bash
command [check_all_disks]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -nce
```

最后，重启 nagios-nrpe-server：

```bash
sudo systemctl restart nagios-nrpe-server.service
```

同时，在 server01 上重启 nagios：

```bash
sudo systemctl restart nagios3.service
```

你现在应该能够在 Nagios CGI 文件中看到主机和服务检查。要访问它们，请将浏览器指向 `http://server01/nagios3`。系统会提示你输入 `nagiosadmin` 用户名和密码。

### 参考文献

本节仅是 Nagios 功能的一个冰角。`nagios-plugins-extra` 和 `nagios-snmp` 插件包含了更多的服务检查。

- 更多信息请参阅 Nagios 网站。
- 特别是 Nagios 在线文档站点。
- 还有一个与 Nagios 和网络监控相关的书籍列表：
- Nagios Ubuntu Wiki 页面也有更多详细信息。

# Munin

## 安装

在 server01 上安装 Munin 之前，需要安装 apache2。默认配置对于运行 munin 服务器已经足够。更多信息请参阅如何设置 Apache。

首先，在 server01 上安装 munin。在终端中输入：

```bash
sudo apt install munin
```

现在在 server02 上安装 munin-node 包：

```bash
sudo apt install munin-node
```

## 配置

在 server01 上编辑 `/etc/munin/munin.conf`，添加 server02 的 IP 地址：

```ini
## 首先是我们的“普通”主机.
[server02]
address 172.18.100.101
```

注意

> 将 `server02` 和 `172.18.100.101` 替换为你服务器实际的主名和 IP 地址。

接下来，在 server02 上配置 munin-node。编辑 `/etc/munin/munin-node.conf` 以允许 server01 访问：

```bash
allow 172.18.100.108$
```

注意

> 将 `172.18.100.108` 替换为你 munin 服务器的 IP 地址。

现在在 server02 上重启 munin-node 使更改生效：

```bash
sudo systemctl restart munin-node.service
```

最后，在浏览器中访问 `http://server01/munin`，你应该能看到指向精美图表的链接，显示来自标准 munin 插件的磁盘、网络、进程和系统信息。

### 注意

由于是新安装，图表可能需要一些时间才能显示有用的内容。

## 附加插件

`munin-plugins-extra` 包包含了性能检查等附加服务，如 DNS、DHCP、Samba 等。要安装该包，在终端中输入：

```bash
sudo apt install munin-plugins-extra
```

确保在服务器和节点机器上都安装该包。

### 参考文献

- 更多详情请参阅 Munin 网站。
- 特别 Munin 文档页面包含了附加插件、编写插件等信息。

# Rsnapshot

Rsnapshot 是一个基于 rsync 的文件系统快照工具。它可以对任意数量机器的本地和远程文件系统进行增量备份。Rsnapshot 大量使用硬链接，因此只有在绝对必要时才会占用磁盘空间。它利用 rsync 的功能来创建调定的增量备份。

要安装它，在终端 shell 中并运行：

```bash
sudo apt-get install rsnapshot
```

如果你想备份远程文件系统，rsn 服务器需要能够通过 SSH 无密码访问目标机器。有关如何启用更多信息请参阅 OpenSSH 文档。如果备份目标是本地文件系统，则无需设置 OpenSSH。

## 配置

Rapshot 配置位于 `/etc/rsnapshot.conf`。在下方你可以找到一些可用选项。

所有快照将存储的根目录：

```bash
snapshot_root /var/cache/
```

你想保留多少份备份？由于 rsnapshot 使用增量备份，我们可以负担得起在删除之前保留较旧的备份。你在 BACKUP 部分设置这些内容。你告诉 rsnapshot 为每种时间间隔保留特定数量的备份：

- `retain daily 6`
- `retain weekly 7`
- `retain monthly 4`

在此示例中，我们保留了 6 个每日策略快照、7 个每周策略快照和 4 个月度策略快照。这些数据将指导 rsnapshot 进行的轮转操作。

如果你通过 SSH 访问远程机器且端口不是默认值 `22`，你需要设置带端口的变量：

```bash
ssh_args -p 22
```

最重要的部分是，你需要决定想备份什么。如果你是备份到本地同一台机器，只需指定你想保存的目录并跟上 `localhost/` 即可，这将是你之前设置的 `snapshot_root` 下的子目录。

```bash
backup /home/
backup /etc/
backup /usr/local/
```

如果你正在备份远程机器，你需要告诉 rsnapshot 服务器在何处以及备份哪些目录：
