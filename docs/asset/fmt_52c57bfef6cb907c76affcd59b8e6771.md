
两个文件具有相同的`inode`，因此它们具有相同的权限和相同的所有者。两个文件的内容也相同。实际上，这两个文件现在是等价，这意味着你可以安全地删除原始文件，硬链接文件将保留。`inode`包含一个计数器，记录指向自身的硬链接数量。当计数器降为零时，`inode`将被清空。

### 4.3.2 查找硬链接

你可以使用`find`命令查找特定`inode`的文件。下面的截图显示了如何搜索指向`inode` 81720的文件名。记住`inode`号是唯一的。

```
paul@RHELv4u:~/test$ find -inum 81720 /dev/null
/home/paul/test/file2
/home/paul/test/hardlink_to_file2
```

## 4.4. 符号链接 (symbolic links)

符号链接（也称为软链接）不链接到`inode`，而是创建一个名称映射。符号链接通过`ln -s`创建。如下所示，符号链接拥有自己的`inode`。

```
paul@RHELv4:~/test$ ln -s file2 symlink_to_file2
paul@RHELv4:~/test$ ls -l
total 32
817266 -rw-r--r-- 1 paul 0 Feb 15:38 file1
817270 -rw-r--r-- 2 paul 92 Feb 15:42 file2
817270 -rw-r--r-- 2 paul 0 Feb 15:38 file3
817270 -rw-r--r-- 2 paul 92 Feb 15:42 hardlink_to_file2
817271 -lrwxrwxrwx 1 paul 5 Feb 15:45 symlink_to_file2 -> file2
paul@RHELv4:~/test$
```

符号链接上的权限没有意义，因为应用的是目标的权限。硬链接限于它们所在的分区（因为它们指向`inode`），符号链接可以链接到任何地方（其他文件系统、网络）。

## 4.5 删除链接

可以使用`rm`删除链接。

```
paul@laika:-$ touch data.txt
paul@laika:-$ ln -s data.txt sl_data.txt
paul@laika:-$ ln data.txt hl_data.txt
paul@laika:-$ rm sl_data.txt
paul@laika:-$ rm data.txt hl_data.txt
```

## 4.6. 练习：链接

1. 创建两个名为`winter.txt`和`summer.txt`的文件，并在其中写入一些文本。
2. 创建一个名为`hwinter.txt`的硬链接。
3. 显示这三个文件的`inode`号，硬链接应该具有相同的`inode`。
4. 使用`find`命令列出两个硬链接文件。
5. 文件的所有信息都在`inode`中，除了两点：名称和它们！
6. 创建一个名为`summer.txt`的符号链接。
7. 查找`inode`号为2的文件。这些信息告诉了你什么？
8. 查看目录`/etc/init.d/`、`/etc/rc2.d/`、`/etc/rc3.d/` …… 你看到链接了吗？
9. 使用`ls -l`查看`/lib`。
10. 使用`find`在你的主目录下查找没有(!)一个硬链接的普通文件。

## 4.7 创建两个文件

1. 创建两个名为`winter.txt`和`summer.txt`的文件，并在其中写入一些文本。

```
echo > winter.txt
echo > summer.txt
```

2. 创建一个名为`hwinter.txt`的硬链接。

```
ln winter.txt hwinter.txt
```

3. 显示这三个文件的`inode`号，硬链接应该具有相同的`inode`。

```
ls -li winter.txt summer.txt hwinter.txt
```

4. 使用`find`命令列出两个硬链接文件。

```
find -inum [inode number]
```

5. 文件的所有信息都在`inode`中，除了两点：名称和它们！文件名在目录中，而内容在磁盘的某处。
6. 创建一个名为`summer.txt`的符号链接。

```
ln -s summer.txt summer.txt
```

7. 查找`inode`号为2的文件。这些信息告诉了你什么？它告诉你多个`inode`（每个格式化的分区一个）。
8. 查看目录`/etc/init.d/`、`/etc/rc2.d/`、`/etc/rc3.d/` …… 你看到链接了吗？

```
ls -l /etc/init.d
ls -l /etc/rc2.d
ls -l /etc/rc3.d
```

9. 使用`ls -l`查看`/lib`。

```
ls -l /lib
```

10. 使用`find`在你的主目录下查找没有(!)一个硬链接的普通文件。

```
find ~ -links 1 -type f
```

# 第二部分 磁盘管理

## 目录

| 章节 | 页 |
| :--- | :--- |
| 5. 设备 | 35 |
| 5.1. 术语 | 36 |
| 5.2. 设备命名 | 38 |
| 5.3. 发现磁盘设备 | 39 |
| 5.4. 擦除硬盘 | 44 |
| 5.5. 高级磁盘设置 | 45 |
| 5.6. 练习：磁盘设备 | 46 |
| 5.7. 解决方案：磁盘设备 | 47 |
| 6. 磁盘分区 | 49 |
| 6.1. 关于分区 | 50 |
| 6.2. 发现分区 | 51 |
| 6.3. 分区新磁盘 | 53 |
| 6.4. 关于分区表 | 55 |
| 6.5. GUID 分区表 | 56 |
| 6.6. 使用 `parted` 标记 | 56 |
| 6.7. 练习：分区 | 58 |
| 6.8. 解决方案：分区 | 59 |
| 7. 文件系统 | 60 |
| 7.1. 关于文件系统 | 61 |
| 7.2. 常见文件系统 | 62 |
| 7.3. 在分区上放置文件系统 | 65 |
| 7.4. 调整文件系统 | 66 |
| 7.5. 检查文件系统 | 67 |
| 7.6. 练习：文件系统 | 68 |
| 7.7. 解决方案：文件系统 | 69 |
| 8. 挂载 | 70 |
| 8.1. 挂载本地文件系统 | 71 |
| 8.2. 显示挂载系统 | 72 |
| 8.3. 从开始到结束 | 74 |
| 8.4. 永久挂载 | 75 |
| 8.5. 安全挂载 | 76 |
| 8.6. 挂载远程文件系统 | 77 |
| 8.7. 练习：挂载文件系统 | 78 |
| 8.8. 解决方案：挂载文件系统 | 79 |
| 9. 故障排除工具 | 81 |
| 9.1. `lsof` | 82 |
| 9.2. `fuser` | 83 |
| 9.3. `chroot` | 84 |
| 9.4. `iostat` | 85 |
| 9.5. `iotop` | 86 |
| 9.6. `vmstat` | 87 |
| 9.7. 练习：故障排除工具 | 88 |
| 9.8. 解决方案：故障排除工具 | 89 |
| 10. `uid` 简介 | 90 |
| 10.1. 关于唯一对象 | 91 |
| 10.2. `tune2fs` | 91 |
| 10.3. `uid` | 92 |
| 10.4. 在 `/etc/stab` 作为启动设备的 `uid` | 92 |
| 10.5. `uids`: `uid` 和文件系统 | 93 |
| 10.6. 练习：`uid` 和文件系统 | 94 |
| 10.7. 解决方案：`uid` 和文件系统 | 95 |

`11.4. 练习：raid`
