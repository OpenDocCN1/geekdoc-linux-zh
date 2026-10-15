

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

Solaris ACL 模型完全支持 NFSv4 在 UNIX 和非 UNIX 客户端之间提供的互操作性。它类似于 Windows NT 风格的 ACL，并提供了比标准文件权限更详细访问控制。这些 ACL 使用 chmod A 和 ls -v、V、dv、dV 命令进行设置和显示。

ACL 模型有两种影响访问检查的访问控制条目（ACEs）：ALLOW 和 DENY。因此，你不能仅从定义一组权限的单个 ACE 推断出该 ACE 中未定义的权限是允许还是拒绝。

### 24.5.1.1 ACL 格式

ACL 有两种基本格式：

- 1. 简单 ACL：仅包含传统 UNIX 用户类别的条目，表示为 owner@、group@ 和 everyone@。

对于新创建的文件，默认 ACL 具有以下条目：

```
0:owner@:read_data/write_data/append_data/read_xattr/write_xattr
```

