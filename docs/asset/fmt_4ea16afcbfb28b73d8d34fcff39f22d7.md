
# Pocket Linux Guide

```bash
bash# make
bash# cp disk-utils/mkfs ~staging/sbin
bash# cp fdisk/fdisk ~staging/sbin
bash# cp login-utils/agetty ~staging/sbin
bash# ls agetty ~staging/utils/sbin/bin
bash# cp login-utils/login ~staging/bin
bash# cp misc-utils/kill ~staging/bin
bash# cp mount/mount ~staging/bin
bash# cp mount/umount ~staging/bin
bash# cp mount/swapon ~staging/bin
bash# cp sys-utils/dmesg ~staging/bin
```

### 5.3.3. 检查库依赖

```bash
bash# ldd ~/staging/bin/* | more
bash# ldd ~/staging/sbin/* | more
bash# ls ~/staging/lib
```

`ldd` 命令显示的所有依赖项都已存在于该暂存区域中，不需要复制任何新内容。

## 5.3.4. 剥离二进制文件以节省空间

```bash
bash# strip ~/staging/bin/*
bash# strip ~/staging/sbin/*
```

### 5.3.5. 创建额外的设备文件

```bash
bash# mknod ~/staging/dev/ram0 b 1 0
bash# mknod ~/staging/dev/fd0 b 2 0
bash# mknod ~/staging/dev/null c 1 3
```

### 5.3.6. 创建 fstab 和 mtab 文件

```bash
cd ~/staging/etc
```

使用编辑器 `vi`、`emacs` 或 `proc` 创建 `fstab` 并将其保存为 `~/staging/etc/fstab`。

| proc /proc proc | defaults 0 0 |
| /dev/ram0 ext2 | defaults 1 1 |

创建一个空的 `mtab` 文件。

```bash
bash# echo -n >mtab
```

### 5.3.7. 编写脚本来检查并挂载本地文件系统

使用编辑器创建以下 shell 脚本并将其保存为 `~/staging/etc/init.d/local_fs`：
