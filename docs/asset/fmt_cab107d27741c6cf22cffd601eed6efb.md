
这会在 `/usr/local/etc` 下产生一个名为 `httpd` 的目录。

`2a-export_linux2_0_0_tar` 会在 `/usr/local/etc/httpd` 下解压。

此，在 `/usr/local/etc/httpd` 下产生一个名为 `bin` 的目录。

以及在 `/usr/local/etc/httpd` 下产生一个名为 `conf` 的目录。

以及在 `/usr/local/etc/httpd` 下产生一个名为 `lib` 的目录。

以及在 `/usr/local/etc/httpd` 下产生一个名为 `logs` 的目录。

以及，在 `/usr/local/etc/httpd` 下产生一个名为 `var` 的目录。

以及在 `/usr/local/etc/httpd` 下产生一个名为 `www` 的目录。

`/usr/local/etc/httpd/bin` 包含执行文件 `/usr/local/etc/httpd/conf` 包含一个

`/usr/local/etc/httpd/lib` 的文件。 `/usr//////d//logs` 包含一个名为 `/usr/local/etc/httpd/logs` 的文件。 `/usr/local/etc/httpd/var` 的文件。 `/usr/local/etc/httpd/www` 的文件。

`/usr/local/etc/httpd/conf/access.conf`

`/usr/local/etc/httpd/conf/httpd.conf`

`/usr/local/etc/httpd/conf/srm.conf`

`/usr/local/etc/httpd/conf/access.conf` 包含一个名为 `/usr/local/etc/httpd/conf/access.conf` 的文件。 `/usr/local/etc/httpd/conf/httpd.conf` 包含一个名为 `/usr/local/etc/httpd/conf/httpd.conf` 的文件。 `/usr/local/etc/httpd/conf/srm.conf` 包含一个名为 `/usr/local/etc/httpd/conf/srm.conf` 的文件。

# 352 第 4 章：设置 Web 服务器

## CERN 服务器

CERN Web 服务器（也称为 W3C httpd）是一个通用公共领域服务器。它于 1996 年 7 月 15 日发布。CERN 服务器会检测你正在使用的 UNIX 系统，并在 `../WWW/Daemon/` 下创建一个执行文件。

配置文件存储在 `/etc/httpd.conf`。

如果你没有使用 CERN 服务器，只要当前目录是 WWW，就可以运行 `make` 命令：

```
make
```
