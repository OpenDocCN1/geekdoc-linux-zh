
-r--r--r root 0 May 10 16:14 file-nr

在这些列列表中，`dir-notify-enable` 和 `file-max` 是可以写入的，因此可以用于配置内核。其他文件仅提供当前设置的反馈。

更改 `/proc/sys/` 中的值是通过将新值 `echo` 到文件中来实现的。例如，要在运行的内核上启用系统请求（System Request），请使用命令：

```bash
echo 1 > /proc/sys/sysrq
```
