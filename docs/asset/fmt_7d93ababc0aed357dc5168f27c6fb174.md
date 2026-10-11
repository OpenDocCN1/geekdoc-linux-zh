
`makeinfo -o doc/com_err.info ..lib/et/com_err.texinfo`

`install -v -m644 doc/com_err.info /usr/share/info`

`install-info --dir-file=/usr/share/info/dir /usr/share/info/com_err.info`

### 6.49.2. E2fspros 的内容

- 安装的程序：
`badblocks`, `chattr`, `compile_et`, `debugfs`, `e2fsck`, `e2free`, `e2fsck`, `e2image`, `label2 deundo`, `e4defrag`, `fileck`, `fsckext2`, `fsckext3`, `fsckext4`, `logsave`, `lsattr`, `mk_kdms`, `mkfs2`, `mkfs`, `mkfs3`, `mkfs4`, `mkfs4dev`, `mklost+found`, `resize2`, and `tune2fs`
- 安装的库：
`libcom_err.so`, `lib2p`, `libext2fs.so`, `libss.so`
`/usr/include/e2p`, `/usr/include/ext2fs`, `/usr/include/ss`

#### 描述
- `badblocks`: 在设备上的坏块
- `chattr`: 修改文件属性
- `compile_et`: 将名称转换为代码
- `debugfs`: 文件系统的调试器
- `e2fsck`: 用于检查和修复
- `e2free`: 报告可用空间
- `e2image`: 用于创建
- `label2`: 为文件系统标记
- `e2undo`: 重放撤销操作
- `e4defrag`: 在线碎片整理
- `fileck`: 检查文件错误
- `fsckext2`: 检查 ext2 系统
- `fsckext3`: 检查 ext3 系统
- `fsckext4`: 检查 ext4 系统
- `logsave`: 保存日志输出
- `lsattr`: 列出文件属性
- `mk_kdms`: 创建字符串表
- `mkfs2`: 创建 ext2 系统
- `mkfs`: 创建文件系统
- `mkfs3`: 创建 ext3 系统
- `mkfs4`: 创建 ext4 系统
- `mkfs4dev`: 创建 ext4 开发系统
- `mklost+found`: 创建 lost+found 目录
- `resize2`: 增大或缩小文件系统
- `tune2fs`: 调整调优参数
- `libcom_err`: 通用错误例程
- `lib2p`: 用于 dumpefs
- `libext2fs`: 用于 lsattr
- `libss`: 用于 debugfs

修复某些权限，以便非根用户可以编译并运行测试：

```
chown -Rv nobody .
```

现在运行测试。确保 `su` 环境中的 `PATH` 包含 `/tools/bin`。

```
su nobody -s /bin/bash \
-c "PATH=$PATH make RUN_EXPENSIVE_TESTS=yes check"
```

已知 `test-login` 测试在虚拟控制台（如这里的 chroot 环境）上会失败，但在 X 终端中运行则可以通过。

删除临时组：

```
sed -i '/dummy/d' /etc/group
```

安装软件包：

```
make install
```

将程序移动到 FHS 指定的位置位置：

```
mv -v /usr/bin/{cat,chgrp,chmod,chown,cp,date,dd,df,de,echo} /bin
mv -v /usr/bin/{false,ls,mkdir,knod,mv,mv,pwd,rm} /bin
mv -v /usr/bin/{rmdir,stty,sync,true,uname} /bin
mv -v /usr/bin/chroot /usr/bin
mv -v /usr/share/man/man1/chroot.1 /usr/share/man/man8/chroot.8
sed -i s/\1\8"/1 /usr/share/man/man8/chroot
```

LFS-Bootscripts 软件包的部分依赖于 `head`、`sleep` 和 `nice`。由于在启动早期阶段可能无法使用 `/usr`，这些二进制文件不在根分区上：

```
mv -v /usr/bin/{head, sleep,nice,test,[]} /bin
```
