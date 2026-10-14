
`void (*write_super) (struct super_block *super)`

当数据块的内容发生变化且需要写入磁盘时（例如执行同步时），VFS 调用 `write_super` 操作。

`void (*statfs) (struct super_block *super, struct statfs *buf, int bufsize)`

VFS 调用 `statfs` 获取文件系统信息。参数 `buf` 指向 `statfs` 类型变量，其定义在第 6.4 节。

`int (*remount_fs) (struct super_block *super, int *flags, char *data)`
