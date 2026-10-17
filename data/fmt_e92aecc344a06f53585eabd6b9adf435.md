
通过选取其中一个进程号并执行以下操作来确保它是 chroot 的：
`[root ~]## ls -la /proc/14373/root/`

如果你看到：
`dev`
`etc`
`home`
`lib`
`usr`

如上所述，如果你使用 Perl，你需要将任何系统库、perl 库 `"/usr/lib"` 和二进制文件复制或硬链接到 chroot 区域。SSL、PHP、LDAP、PostgreSQL 和其他程序也同样。

## "etc/logrotate.apache" 的配置

现在 Apache 日志位于 `"chroot/var/log/httpd"` 目录而不是 `/var/log/httpd`，因此，我们需要修改 `"etc/logrotate.apache"` 文件指向新的 chroot 目录。此外，我们在编译 Apache 时使用了 `mod_ssl`，因此我们又增加了一行，允许 `logrotate` 程序轮转 `"ssl_request_log"` 和 `"ssl_engine_log"` 文件。配置你的 `"etc/logrotate.apache"` 文件每周自动轮转日志。

创建 apache 文件（`touch /chroot/logrotate.apache`）并添加：

```
/chroot/httpd/var/log/httpd/access_log {

missing

postostrate

/usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

endscript

}
```

```
/chroot/httpd/var/log/httpd/error_log {

missing

postostrate

/usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

endscript

}
```

```
/chroot/httpd/var/log/httpd/ssl_request_log {
```

## 服务器软件（Web 网络服务） | 第 9 章

```
missingok

postrotate

/usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

endscript
```

```
/chroot/httpd/var/log/httpd/ssl_engine_log {

missingok

postrotate

/usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

endscript}
```

## 优化 Apache

`mod_mmap_static` 是 Apache 分发中的一个特殊模块，用于提高您的 Web 服务器的性能。该模块通过为您的根目录（`RootDirectory`）中静态配置的、频繁请求但不会更改的文件列表提供映射来工作。如果 Apache 显示的文件不经常更改，您可以使用此模块对静态文档进行内存映射，并提高您的 Apache Web 服务器的速度。

需要注意的是，在使用 Apache `mod_mmap_static` 模块之前，必须在 Apache 的配置和编译期间启用它。如果您按照上述对配置和编译时间的描述进行操作，那么该模块已经包含在 Apache 中了（`-add-module-/mod_mmap_static.c`）。

### 第一步

- 使用以下命令对静态文档进行内存映射：
`[root]@deep# /find /home/httpd/httpd/ona -type f -print -1 | sed -e 's/\/"/g' /mmapfile &/ > /etc/httpd/conf/mmap.conf`

`/home/httpd` 是根目录，或者确切地说，是我们从中提供文档的目录，而 `/etc/httpd/mmap.conf` 是我们想要创建此名为 `"mmap.conf"` 文件的位置，该文件包含您的根目录下所有文档的静态内存映射。

### 第二步

一旦在选定的位置创建了 `"mmap.conf"` 文件，我们必须将其包含在 Apache 的 `"httpd.conf"` 文件中，以便在 Web 服务器上使用其功能。

编辑 `/etc/httpd/httpd.conf` 文件并添加以下行：

```
<IfModule mod_mmap_static>
Include conf/mmap.conf
</IfModule>
```

注意：请参阅 Apache 文档以获取更多关于 `mod_mmap_static` 使用的信息。请记住，此功能仅当您的网站上提供不经常更改的文档时才可以使用。

#### 第三步

您必须重启 Apache Web 服务器使更改生效：

Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture & OpenDocs Publishing

- 重启 Apache 请使用以下命令：

```
[root@deep ~]# /etc/rc.d/init.d/httpd restart

Shutting down http: [ OK ]

Starting http: [ OK ]
```
