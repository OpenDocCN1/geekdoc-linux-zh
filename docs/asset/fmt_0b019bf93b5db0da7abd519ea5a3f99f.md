
```
/dev/hda6      /usr      ext2      0 0
```

这种方法可能会让你的机器难以更新，因此请谨慎使用这种策略。

# 主机安全 1073

- 挂载除 `/` 和 `/usr` 外的文件系统时使用 `nosuid` 选项，以防止在该文件系统上执行程序。例如：

```
/dev/hda4      /var      ext3  nosuid 0 0

/dev/hda5      /usr/local ext3  nosuid 0 0
```
