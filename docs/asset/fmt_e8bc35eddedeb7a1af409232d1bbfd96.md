
### 24.4.6 用于增量 ZFS 备份的 Bourne Shell 脚本示例

#### 示例 24.7：Bourne Shell 脚本中的 `zfs snapshot` 命令自动化

以下 Bourne shell 脚本通过 `zfs snapshot send/receive` 实现将一台计算机上的文件系统增量备份到远程主机系统。它与之前显示的 `zfs send/receive` 示例代码非常相似，并且是其进一步扩展。

运行此脚本的前提条件是：

- 1. 接收快照的主机必须运行与发送方相同或更高版本的 ZFS。
- 2. 你必须在接收备份的主机上拥有 root 访问权限。
- 3. 你必须发送到具有 ZFS `create/receive` 属性的账户。
- 4. 你之前已创建了源的快照。
- 5. 你之前已在目标上创建了名为 `/tank/test` 的 Z 文件系统。

```
#!/bin/sh
# This assigns a local file system as the source to be
# transmitted
pool="/usr/src"
# This assigns a remote destination
# destination="tank/test"
# This names the IP address of the remote target host
# host="192.168.0.7"
# This sets the date format for today in PC-BSD
# For Solaris the date format should be today = 'date +
"%Y-%m-%d"'
# today='date +"%Y-%m-%d"'
# This sets the date format for yesterday in PC-BSD
# For Solaris the date format should be yesterday = 'date
# -d"-1 day" + "%Y-%m-%d"'
yesterday='date -v -1d +"%Y-%m-%d"'
# Create today's snapshot
snapshot_today="$pool@$today"
# Look for a snapshot with this name, and if none exists,
# take the snapshot
if zfs list -H -o name -t snapshot | sort | grep "$snapshot_today$" > /dev/null
then
    echo " snapshot, $snapshot_today, already exists"
    exit 1
else
    echo " taking todays snapshot, $snapshot_today"
    zfs snapshot -r $snapshot_today
fi
# Look for yesterday's snapshot
snapshot_yesterday="$pool@$yesterday"
# If it exists, ZFS sends today's snapshot
if zfs list -H -o name -t snapshot | sort | grep "$snapshot_yesterday$" > /dev/null
then
    echo " yesterday snapshot, $snapshot_yesterday, exists, send todays backup"
    zfs send -R -i $snapshot_yesterday $snapshot_today | ssh root@$host zfs receive -Fduv \
    $destination
    echo " backup complete destroying yesterdays snapshot"
    zfs destroy -r $snapshot_yesterday
    exit 0
else
    echo " missing yesterday snapshot aborting, $snapshot_yesterday"
    exit 1
fi
```

## 24.5 使用访问控制列表（ACLs）和属性来保护 Solaris ZFS 文件

与传统的 UNIX 权限模型相比，传统的 UNIX 权限模型通过读、写和执行等权限来定义对文件或目录等对象的安全访问，访问控制列表（ACL）模型为用户提供了更细粒度的对象安全基础控制。

在权限模型中，组权限是文件所有者将访问权委托给用户基础中不同组成员的唯一方式。这是因为任何文件只能属于一个组。因此，为了服务于不同的组成员，必须存在许多不同的组。只有管理员可以创建和分配组成员身份。而使用权限模型，在协作工作项目团队之间共享文件变得不可行。

ACLs 提供了更大的自主裁量权，但代价是更高的复杂性、更大的存储需求以及底层文件系统（无论是 VFS 还是 ZFS）性能变慢。我们的两个 UNIX 基础系统 PC-BSD 和 Solaris，均使用 ZFS，支持权限模型和 ACL 模型（本文中称为 NFSv4）。由于存在多种 ACL 模型，这里值得注意的是 ZFS 仅支持 NFSv4 ACLs。

我们在第 5 章第 5.4 节和 5.5 节展示了权限模型。本节所示的方法适用于 Solaris ZFS 文件。在第 23 章第 9.3 节中，我们详细说明了在 PC-BSD 系统上管理 ZFS 文件和目录的 ACL 的类似方法。

我们在以下子节中涵盖以下主题：

- 24.5.1 Solaris ACL 模型
- 24.5.2 在 ZFS 文件上设置 ACL 以及设置 ACL 的命令语法
- 24.5.3 在 ZFS 文件上设置 ACL 继承

### 24.5.1 Solaris ACL 模型

Solaris ACL 模型完全支持 NFSv4 在 UNIX 和非 UNIX 客户端之间提供的互操作性。它类似于 Windows NT 风格的 ACL，并提供了比标准文件权限更详细访问控制。这些 ACL 使用 `chmod A` 和 `ls -v`、`V`、`dv`、`dV` 命令进行设置和显示。

ACL 模型有两种影响访问检查的访问控制条目（ACEs）：`ALLOW` 和 `DENY`。因此，你不能仅从定义一组权限的单个 ACE 推断出该 ACE 中未定义的权限是允许还是拒绝。

#### 24.5.1.1 ACL 格式

ACL 有两种基本格式：

- 1. 简单 ACL：仅包含传统 UNIX 用户类别的条目，表示为 `owner@`、`group@` 和 `everyone@`。

对于新创建的文件，默认 ACL 具有以下条目：

```
0:owner@:read_data/write_data/append_data/read_xattr/write_xattr
/read_attributes/write_attributes/read_acl/write_acl/write_owner/synchronize:allow
```

```
1:group@:read_data/read_xattr/read_attributes/read_acl/synchronize:allow
2:everyone@:read_data/read_xattr/read_attributes/read_acl/synchronize:allow
```

对于新创建的目录，默认 ACL 具有以下条目：

```
0:owner@:list_directory/read_data/add_file/write_data/add_subdirectory/append_data/read_xattr/write_xattr/execute/delete_child/read_attributes/write_attributes/read_acl/write_acl/write_owner/synchronize:allow
1:group@:list_directory/read_data/read_xattr/execute/read_attributes/read_acl/synchronize:allow
2:everyone@:list_directory/read_data/read_xattr/execute/read_attributes/read_acl/synchronize:allow
```

- 2. 非平凡 ACL：包含针对已添加用户类别的条目。这些条目可能还包括继承标志，或按非传统方式排序。一个非平凡条目可能如下例所示，其中权限被专门授予用户 `mansoor`。

```
0:user:mansoor:read_data/write_data:file_inherit:allow
```

#### 24.5.1.2 ACL 条目描述

Solaris 中 NFSv4 ACL 命令规范的组成部分：
