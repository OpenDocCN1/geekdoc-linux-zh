
## 再次验证你的系统设置：

```bash
# chkconfig --list | grep httpd

httpd      0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

使用关键字从特定的运行级别启动 Apache。

# 使用 Red Hat 的 redhat-config-services 客户端控制 Apache

你也可以在 X 会话期间使用名为 `redhat-config-services` 的 `chkconfig` 图形版本来设置 Apache 的启动或停止的时间以及所在的运行级别。要启动 `redhat-config-services`，可以从桌面面板主菜单的“服务器设置”菜单中选择“服务”项，或者在终端窗口中输入如下命令：

```bash
$ redhat-config-services &
```
