

# 368 第三部分 ♦ 在 SUSE Linux 中使用命令行

`cpio` 和 `tar`，这两者都可能让新用户感到头疼。与 `tar` 相比，它提供了一个更整洁的解决方案，用于将带有权限、时间戳和符号链接的整个目录树从一个地方精确地复制到另一个地方。

创建一个 pax 归档文件，可以使用以下命令：

```
pax -w -f archive.tar /path/to/directory
```

解压 pax 归档：

```bash
pax -r -f archive.tar
```

使用 cpio 创建归档：

```bash
find . | cpio -o > archive.cpio
```

提取 cpio：

```bash
cpio -i < archive.cpio
```
