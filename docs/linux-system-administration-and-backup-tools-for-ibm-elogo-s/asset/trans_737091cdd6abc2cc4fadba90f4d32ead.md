

## 5.11 文件系统权限

Linux 具有内置的安全特性，最显著的就是文件系统权限。对文件设置权限允许系统管理员限制对文件部分内容的访问。

文件权限可以设置在文件和目录上。查看此示例的最简单方法是在 `/home` 目录下：

```
mail:/home # ls -l
total 1 396 Nov 15 21:16
drwx-xr-x 19 root       487 Nov 15 13:26
drwx-xr-x 22 root       912 Nov 15 21:05 davej
drwxr-      6 davej users    912 Nov 15 21:03 george
drwxr-      6 george users    912 Nov 15 21:02 ive
drwxr-      6 ive users       912 Nov 15 21:18 jakob
drwxr-      6 jasmin users   912 Nov 15 21:04 jasmine
drwxr-      6 jen users       912 Nov 15 21:04 jens
drwxr-      6 jamins users   912 Nov 15 21:36 jackkins
drwxr-      6 justin users   912 Nov 15 21:06 justin
drwxr-      6 lenz users       912 Nov 15 21:03 lenz
drwxr-      6 linux users     912 Nov 15 21:01 linux
drwxr-      6 malcom users   912 Nov 15 21:04 malcom
drwxr-      6 rachael users   912 Nov 15 21:03 rechael
drwxr-      6 rufus users     912 Nov 15 21:14 rufus
drwxr-      6 ruediger users  912 Nov 15 21:04 ruediger
drwxr-      6 rufus users     912 Nov 15 21:02 rufus
drwxr-      6 ted users       912 Nov 15 21:03 ted
drwxr-      6 uzi users       912 Nov 15 21:04 uzi
mail:/home #
```

图 180. 查看文件权限

以用户 "linux" 为例：

![](img/4e6a76e57a4105be55d8a1cc0750b023_182_0.png)

图 181. `ls` 的解释位于文件/目录权限中。

我们最感兴趣的是文件/目录权限。这些符号在有限的空间内传达了大量信息：

- d - 权限中的第一个字符表示这是一个目录。
  其他文件的表示方式为：

- + - 一个普通文件。
- l 指向另一个文件的符号链接。
- c 指向 `/dev` 目录下的文件。这表示该文件代表一个字符设备。
- b 指向 `/dev` 目录下的文件。这表示该文件代表一个块设备。

rwx - 在这种情况下，它允许文件的所有者（在本例中为 "linux"）读取、写入和执行该文件。

| 类型 | 所有者 | 组 | 世界 |
| --- | --- | --- | --- |
| d | rwx | --- | --- |

文件的所有者是创建该文件的用户。组部分是拥有该文件的组（例如 `users` 组）。世界（world）部分意味着其他所有人；在世界部分设置权限将为每个用户设置权限，该组可以读取和执行文件，而所有人都可以读取，以此此类推。

这里是另一个示例：

```
-rwx-xr-x
```

这意味着这是一个普通文件，所有者可以读取、写入、执行该文件，而其他人可以读取该文件，但不能修改或执行它。

如果你将一个目录设置为：

```
drwxrrw-rw-
```

你是在说只允许目录所有者在目录“内部”执行某些操作。如果另一个用户尝试进入该目录，他们将收到“permission denied”（拒绝访问）错误。这正是主目录的发生情况。

要更改文件的权限，你使用 `chmod`。只有 `root` 用户可以修改不属于自己的文件。你必须拥有该文件才能更改其权限。

更改权限最简单的方法是使用你希望设置的权限的符号表示法。

注意：表示文件权限的另一种方法是使用八进制。有关此的更多信息，请参阅 `chmod` man 页面。

```
chmod g+rw myfile
```

上面的命令允许组内的所有成员读取和写入。如果你使用 `-`（减号）代替 `+`（加号），你将移除这些权限。这意味着组员将不再被允许读取或写入文件。你可以在同一个命令中混合添加和删除权限：

```
chmod u+x-rw myfile
```

这将允许执行文件，但不允许所有者读取或写入。以下是 `chmod` 中可用的符号表示法总结：

- r - 读取
w - 写入
x - 执行
s - 设置 SUID 位。这表示如果文件是可执行的，它将以文件所有者的身份运行，而不是当前用户的身份。

## 6. 备份恢复

系统管理员应该良好维护的项目之一是备份恢复。

[content]

### 6.1 备份硬件

表 8 中列出的产品适用于 IBM @server xSeries 和服务器，并至少支持一种 Linux 备份恢复包：

表 8. Linux 备份工具，支持 Netfinity 磁带设备

| 带设备 | Arkeia | BackupEDGE | BRU |
|---|---|---|---|
| IBM 35/70 GB DLT 磁带 (SCSI-2) | x | x | x |
| IBM 20/40 GB DLT 磁带 (SCSI-2) | x | x | x |
| IBM 20/40 GB 8 mm 磁带 (SCSI) | x | x | x |
| IBM 10/20 GB NS 磁带 (SCSI-2) | x | x | x |
| IBM 100/200 GB 内部 LTO 磁带 (SCSI-2) | x | x | x |

