
`[root@deep #] rm -rf /chroot/httpd/etc/`

`[root@deep #] rm -rf /chroot/httpd/home/`

`[root@deep #] rm -rf /chroot/httpd/usr/sbin`

## 第 11 步

测试 chroot 服务 syslogd。通常，进程通过 `/dev/log` 与 syslogd 通信。由于 chroot 监狱，这是可能的，因此需要告诉 syslogd 监听 `/chroot/httpd/dev/log`。为了做到，编辑 syslog 启动脚本指定额外的监听位置。

编辑脚本 (`vi /etc/rc.d/init.d/syslog`) 修改该行：

```
daemon syslogd -m 0
```

为：

```
daemon syslogd -m 0 -a /chroot/httpd/dev/log
```

## 第 12 步

Apache 的默认脚本文件在 chroot 监狱之外启动，我们必须改为从 chroot 监狱启动。编辑 httpd 脚本 (`vi /etc/rc.d/init.d/httpd`) 并修改该行：

```
daemon httpd
```

为：

```
/usr/sbin/chroot /chroot/httpd /usr/sbin/httpd -DSSL

rm -f /var/run/httpd.pid

/chroot/httpd/var/run/httpd.pid
```

## 第 13 步

最后，我们必须测试我们的 chroot 监狱化的 Apache Web 服务器。

- 第一件事是使用以下命令重启我们的 syslog 守护进程：
  `[root@deep #] /etc/rc.d/init.d/syslog restart`
- 现在，使用以下命令启动 chroot 监狱化的 Apache：

关于本书的意见和建议请邮寄至 `gmourani@videotron.ca`

```bash
[root@deep |# /etc/rc.d/init.httpd start

Starting httpd:

[ OK ]
```

- 如果没有遇到任何错误，执行 `ps ax | grep httpd` 并检查它们是否正在运行：
```bash
[root@deep |# ps ax | grep httpd

14373 ? S 0:00:httpd-DSSL

14376 ? S 0:00:httpd-DSSL

14377 ? S 0:00:httpd-DSSL

14378 ? S 0:00:httpd-DSSL

14379 ? S 0:00:httpd-DSSL

14380 ? S 0:00:httpd-DSSL

14381 ? S 0:00:httpd-DSSL

14382 ? S 0:00:httpd-DSSL

14383 ? S 0:00:httpd-DSSL

14384 ? S 0:00:httpd-DSSL

14385 ? S 0:00:httpd-DSSL

14386 ? S 0:00:httpd-DSSL

14387 ? S 0:00:httpd-DSSL

14388 ? S 0:00:httpd-DSSL

14389 ? S 0:00:httpd-DSSL

14390 ? S 0:00:httpd-DSSL

14391 ? S 0:00:httpd-DSSL

14476 ? S 0:00:httpd-DSSL

14477 ? S 0:00:httpd-DSSL

14478 ? S 0:00:httpd-DSSL
```

如果是的话，让我们通过选取一个进程号并执行 `ls -la /proc/that_process_number/root/` 来检查它是否已 chroot。

```bash
[root@deep |# ls -la /proc/14373/root/
```

如果你看到：
`dev`
`etc`
`home`
`lusr`
`var`

## "/etc/logrotate.d/apache" 文件的配置

现在 Apache 日志位于 "`chroot/var/log/httpd`" 目录而不是 "`var/log/httpd`"，为此我们需要修改路径以指向新的 chroot 目录。我们还通过编译时加载了 `mod ssl`，并将额外添加一行，以允许 logrotate 程序轮转 "`ssl_request_log`" 和 "`ssl_engine_log`" 文件。配置你的 "`/etc/logrotate.d/apache`" 文件以每周自动轮转日志文件。

创建 apache 文件（`touch /chroot/var/log/httpd/apache`）并添加内容：

```bash
/chroot/var/log/httpd/access_log {

  missingok

  postrotate

  /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

  endscript

}

/chroot/httpd/var/log/error_log {

  missingok

  postrotate

  /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

  endscript

}

/chroot/httpd/var/log/httpd/ssl_request_log {

  missingok

  postrotate

  /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

  endscript

}

/chroot/httpd/var/log/httpd/ssl_engine_log {

  missingok

  postrotate

  /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd

  endscript

}
```

## 优化 Apache

Apache 的 `mod_mmap_static` 模块是 Apache Web 服务器的一个特殊模块，它通过为 RootDirectory 中静态配置的频繁请求但未更改的文件列表提供映射，来提高你的 Web 服务器的性能。由于 Apache 显示的文件并不经常更改，你可以使用此模块对静态文档进行内存映射，从而提高你的 Apache Web 服务器的速度。

需要注意的是，在 Apache 的配置和编译期间必须启用 `mod_mmap_static` 模块才能使用它。如果你遵循了我上面在配置和编译时间的描述，这已经在 Apache 中完成了（`-add-module../mod_mmap_static.c`）。

### 步骤 1

- 要对静态文档进行内存映射，使用以下命令：
  `[root@deep ] # find /home/httpd/on- -type f | sed -e 's/.*/mmapfile &/' > /etc/httpd/conf/mmap.conf`

`/home/httpd/on-` 是 RootDirectory，更准确地说，是我们提供文档的目录，而 `</etc/httpd/conf/mmap.conf-` 是我们想要创建此 "`mmap.conf`" 文件的位置，其中包含了我们 RootDirectory 下所有文档的静态内存映射。

### 步骤 2

一旦在所选择的保留位置创建了 "`mmap.conf`"，我们必须将其包含在 Apache 的 `httpd.conf` 文件中，以便在我们的服务器上使用该功能。

编辑 `httpd.conf` 文件（`vi /etc/httpd/conf/httpd.conf`）并添加以下行：

```apache
<IfModule mod_include.c>

Include conf/mmap.conf

</IfModule>
```
