
`-d` 显示默认 ACL

`-R` 递归进入子目录

### 步骤 2
从你刚刚创建的文件获取默认 ACL 信息：

```
# getfacl file1
# file: file1
# owner: root
# group: root
user::rw-
group::r-
other::r-
```

除了默认权限外，没什么特别兴奋的。
你现在可以使用 `setfacl` 命令为此文件创建一些额外的 ACL。

语法：`setfacl [options] file`

选项：

- `-m` 修改 ACL
- `-x` 移除 ACL
- `-n` 不重新计算掩码
- `-R` 递归进入子目录

### 步骤 3
用户 `user01` 也对此文件有访问权限：
```
# setfacl -m user:user01:rwx /opt/backup/file
```

### 步骤 4
现在再次检查 ACL 权限：
```
# getfacl file1
# file: file1
# owner: root
# group: root
user::rw-
user:user01:rw-
group::r-
mask:rw-
other::r-
```

你可以看到 `user01` 现在已添加到列表中，对该文件具有读、写和执行权限。显然，在进行更复杂的 ACL 设置之前，你必须考虑父目录的权限。假设你刚刚终止了 `user01`，并需要从你之前授予过权限的关键文件中移除他的权限。

### 步骤 5
再次使用 `setfacl` 命令移除 `user01` 的 ACL：
```
# setfacl -x u:user01 /opt/backup/file1
```

### 步骤 6
验证 ACL 已经移除：
```
# getfacl file1
# file: file1
# owner: root
# group: root
user::rw-
group::r-
```

### 步骤 7
用户 `user01` 也对此文件有访问权限：
```
# setfacl -m user:user01:rwx /opt/backup/file
```

### 步骤 4
现在再次检查 ACL 权限：
```
# getfacl file1
# file: file1
# owner: root
# group: root
user::rw-
user:user01:rw-
group::r-
mask:rw-
other::r-
```

你可以看到 `user01` 现在已添加到列表中，对该文件具有读、写和执行权限。显然，在进行更复杂的 ACL 设置之前，你必须考虑父目录的权限。假设你刚刚终止了 `user01`，并需要从你之前授予过权限的关键文件中移除他的权限。

### 步骤 5
再次使用 `setfacl` 命令移除 `user01` 的 ACL：
```
# setfacl -x u:user01 /opt/backup/file1
```

### 步骤 6
验证 ACL 已经移除：
```
# getfacl file1
# file: file1
# owner: root
# group: root
user::rw-
group::r-
```

# 第 4 章：文件系统及其他 143

```
cd -fstype=iso9660,ro,noudev,nodev :/dev/cdrom
```

# 以下项目用于激发你的想象力

```
#linux -ro,soft,intr ftp.example.org:/pub/linux
#boot -fstype=ext2 :/dev/hda1
#floppy -fstype=auto :/dev/fd0
#floppy -fstype=ext2 :/dev/fd0
#efloppy -fstype=ext2 :/dev/fd0
#jaz -fstype=ext2 :/dev/hdc1
#removable -fstype=ext2 :/dev/hdd
```

在创建条目时，使用以下语法：`[相对路径] [挂载选项] [位置]`

你可以看到大多数内容都被注释掉了，而 CD-ROM 驱动器被实际定义。这允许在 CD 不使用时对其进行挂载。

### 步骤 1
在 `Client01` 系统上，你可以在 `/etc/auto.misc` 文件中创建条目：`company_data -rw,sync rhel01:/opt/company_data`

### 步骤 2
保存文件并重载 `autofs` 服务：
```
# service autofs reload
```
正在重载映射（Reloading maps）

现在你导航到 `/misc`，你会看到另一个名为 `company_data` 的目录。当访问此目录时，它会自动将来自 `RHEL01` 的远程 NFS 共享挂载到 `/misc/company_data`。如你所见，这对于作为系统管理员为客户端提供多个资源非常方便。

> 注意：使用间接映射（indirect maps）需要注意的一点是，它们允许使用两个通配符。如果你想挂载家目录，可以在间接映射文件中创建以下条目：

```
* -rw,sync &:/home/
```

系统会为用户名进行正确的替换，并自动搜索所有可用 NFS 服务器上的正确资源。这使得对 NFS 服务器上的家目录进行更集中的管理变得更容易。默认的 `/etc/auto.master` 文件中没有示例，直接映射（direct maps）与间接映射类似。

### 步骤 3
在 `/etc/auto.master` 文件中，你需要创建一个如下条目：`/. /etc/auto.direct_maps`

# 144 红帽® 考试实战指南：RHCSA® 和 RHCE® 认证指南与实验手册

这告诉 `/etc/auto.master` 文件引用 `/etc/auto.direct_maps` 以获取关于直接映射的额外信息。在创建间接映射时，你为每个映射指定相对路径；而对于直接映射，你只需为想要挂载的每个映射指定绝对路径。例如，在 `Client01` 系统上，你希望将 `RHEL01` 的 `/opt/company_data_directory` 映射到本地的 `/usr` 目录，而不是 `/misc`。

### 步骤 4
你需要创建 `/etc/auto.direct_maps` 文件并添加以下条目：

```
/usr/data -rw, sync rhel01:/opt/company_data
```

### 步骤 5
保存文件并重载 `autofs` 服务：

```
# service autofs reload
```
