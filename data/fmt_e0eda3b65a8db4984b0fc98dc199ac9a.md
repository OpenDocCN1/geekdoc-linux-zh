
# 使用 `ldd` 查看依赖库

```bash
[master@server myroot]$ ldd $(type -P ls)

linux-vdso.so.1 (0x00007fd266bac000)

libselinux.so.1 => /lib64/libselinux.so.1 (0x00007f5d1f3c9000)

libcap.so.2 => /lib64/libcap.so (0x00007f5d1f3c2000)

ibc.so.6 => /lib64/libc.so.6 (0x00007f5d1f19000)

libpcre2-8.so.0 => (0x00007f5d1f1b6000)

libdl.so.2 => /lib64/libdl.so.2 (0x00007f5d1f164000)

lib64/ldd-linux-x86-64.so (0x00007f5d1f434000)

libthread.so.0 => /lib64/libthread.so.0 (0x00007f5d1f142000)
```

现在我们知道哪些库需要就绪，我们创建目录并复制 64 位的库（因为我们运行的是 64 位的操作系统）。首先，我们创建 `/tmp/myroot/lib64` 目录：

```bash
[master@server myroot]$ mkdir /tmp/myroot/lib64/
```

接下来，我们复制 `/bin/bash` 需要的所有共享库：

```bash
[master@server myroot]$ cp /lib64/libselinux.so.1 lib64/

[master@server myroot]$ cp /lib64/libcap.so.2 lib64/

[master@server myroot]$ cp /lib64/libc.so.6 lib64/

[master@server myroot]$ cp /lib64/libpcre2-8.so.0 lib64/

[master@server myroot]$ cp /lib64/libdl.so.2 lib64/

[master@server myroot]$ cp /lib64/ldd-linux-x86-64.so lib64/

[master@server myroot]$ cp /lib64/libthread.so.0 lib64/
```

## 进入 `chroot` 环境

现在我们使用 `chroot` 命令进入环境并运行 `bash`：

```bash
[master@server myroot]$ chroot /tmp/myroot /bin/bash
```

现在你在 `chroot` 环境中了，根目录已经变成了 `myroot`：

```bash
root@bash# pwd

/

root@bash# cd /

root@bash# /
```

## 测试环境

现在尝试运行 `ls` 命令：

```bash
root@bash# ls

bin

lib64
```

你可以尝试进入 `bin` 目录：

```bash
root@bash# cd bin

root@bash/bin# ls

bash
```

尝试运行 `bash`：

```bash
root@bash/bin# bash

root@bash# pwd

/bin

root@bash# exit

root@bash/bin#
```

最后，退出 `chroot` 环境：

```bash
root@bash/bin# exit

[master@server myroot]$
```
