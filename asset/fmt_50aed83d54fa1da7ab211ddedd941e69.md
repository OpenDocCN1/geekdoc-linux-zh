
-oremove,nochgroup,nochmode,nochowner,quiet \
-f /path/to/distfile

`rm -f /tmp/rdist_net.lck`

`echo` `date` `>` `/tmp/rdist.log`

`exit 0`

```
## 第21 章：构建多服务器 Web 网络

你可以使用 `/etc/crontab` 中的 cron 任务，利用上所示的 rdist 脚本每隔大约 10 分钟更新一次 Web 服务器。

```
*/10,20,30,40,50 * * * * httpd \
/path/to/rdist.sh > /dev/null
```

这里，cron 任务被设置为在 `ns.aminews-lan.com` 系统上以 `httpd` 用户身份运行 `rdist.sh` 脚本。因此，你必须确保该用户存在，并且被允许访问 `/www` 分区中的所有文件和目录。一旦你已经在 `ns.aminews.com`（与 `ns.aminews-lan.com` 相同）上设置了所有服务，就可以配置 Web 服务器了。

## 设置每台 Web 服务器

首先，你应该按照第 12 章所讨论安装 Apache Web 服务器。你不需要在 Apache 中进行任何特殊配置即可在此环境中运行。但是，请记住在使用 `<VirtualHost>` 指令为客户端创建虚拟主机时，使用 `192.168.2.x` IP 地址。换句话说，`192.168.2.1` 服务器上的虚拟主机将使用以下配置语法：

```
<VirtualHost 192.168.2.1>

# 在此处写入虚拟主机特有的配置

</VirtualHost>
```

你应该在每台 Web 服务器上设置 `www.aminews.com` 虚拟网站。接下来，你需要将 Web 服务器计算机配置为 NFS 客户端。

## 设置 NFS 客户端配置

由于 `/www/data` 是由 `ns.aminews-lan.com` 服务器导出到 Web 服务器的，你可以向你的 `/etc/fstab` 添加以下行：

```
ns.aminews-lan.com:/www/data    data nfs
```

添加此行后，创建一个 `mount -a t nfs` 命令来自动将 `ns.aminews-lan.com` 的 `/www/data` 挂载到 `/data` 目录。运行 `df` 命令以确保你可以成功挂载 `/www/data` 目录。在你的其他文件系统中，你应该能看到类似下面的一行：

```
ns.aminews-lan.com:/www/data 27728 7588 18705 23%    /data
```

## 第七部分：针对性能进行优化

一旦你在两台 Web 服务器上完成了此配置，并能够挂载来自 `ns.aminews-lan.com` 的 `/www/data`，你就完成了 NFS 配置。现在在 Web 服务器上设置 sendmail 守护进程。

## 设置 sendmail 程序进行智能中继

由于 Web 服务器上的 sendmail 程序仅通过 `192.168.1.0` 网络将邮件中继到 `mail.aminews.com`，你需要设置 `/etc/sendmail.cf` 文件使用智能中继（smart relay）。你可以在其中添加以下行：

```
ns.aminews.com
```
