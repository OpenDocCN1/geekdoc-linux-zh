
主映射位于`/etc/auto_master`文件中，将目录与映射关联。主映射是指定 Autofs 应检查的所有映射的列表。以下示例显示`auto_master`文件可能包含的内容：

```
# Master map for automounter
#
+auto_master
/net  -hosts  -nosuid,nobrowse
/home  auto_home -nobrowse
/xfn  -xfn
```

此示例显示默认的`auto_master`文件。以`#`开头的行是注释。包含`+auto_master`的行指定 Autofs NIS 表映射，其在第 18 章“Name Services.”中进行了解释。主映射`/etc/auto_master`中此后的每一行具有以下语法：

```
<mount-point> <map-name> <mount-options>
```

每个字段在表 17.8 中描述。

## 表 17.8

## /ETC/AUTO_MASTER 字段

| 字段 | 描述 |
|-------|-------------|
| `mount-point` | This is the full (absolute) pathname of a directory that is used as the mount point. If the directory does not exist, Autofs creates it if possible. If the directory does exist and is not empty, mounting on it hides its contents. In this case, Autofs issues a warning. Using the notation `/-` as a mount point indicates that a direct map with no particular mount point is associated with the map. |
| `map-name` | This is the map that Autofs uses to find directions to locations or mount information. If the name is preceded by a slash (`/`), Autofs interprets the name as a local file. Otherwise, it searches for the mount information using the search specified in the name-service switch configuration file (`/etc/nsswitch.conf`). Name service switches are described in Chapter 18. |
| `mount-options` | This is an optional comma-separated list of options that applies to the mounting of the entries specified in `map-name`, unless the entries list other options. Options for each specific type of file system are listed in Table 17.3 under the `mount` command syntax. For NFS-specific mount points, the `bg` (background) and `fg` (foreground) options do not apply. |

每个 Solaris 安装都带有一个名为`/etc/auto_master`的主映射，其中包含刚刚显示的默认条目。在不更改通用系统设置的情况下，客户端应能够通过`/net`挂载点访问远程文件系统。`/etc/auto_master`中的以下条目允许这种情况发生：

```
/net  -hosts  -nosuid,nobrowse
```

例如，假设你有一个名为`apollo`的 NFS 服务器，其上导出了`/export`文件系统。网络上存在另一个名为`zeus`的系统。该系统具有默认的`/etc/auto_master`文件，并且默认情况下具有名为`/net`的目录。如果你键入

```
ls /net
```

命令返回显示目录为空——其中没有东西。现在键入

```
ls /net/apollo
```

系统作出如下响应：

```
export
```

为什么我第一次发出`ls`命令时它是空的？当我发出`ls /net/apollo`时，为什么它能找到一个子目录？这是 automounter 的作用。当我指定`/net`并带主机名时，`automountd`查看映射文件——在这种情况下为`/etc/hosts`——并找到`apollo`及其 IP 地址。然后它转到`apollo`，找到导出的文件系统，并为`/net/apollo/export`创建一个本地挂载点。它还在`/etc/mnttab`文件中添加了此条目：

```
-hosts  /net/apollo/export  autofs  nosuid,nobrowse,ignore,nest,dev=2b80005 941812769
```

`/etc/mnttab`文件中的此条目称为触发节点。

如果你键入`mount`，此时你看不到任何已挂载的内容：

```
mount
/ on /dev/dsk/c0t3d0s0 read/write/setuid/largefiles on Mon Nov  1 06:05:46 1999
/usr on /dev/dsk/c0t3d0s6 read/write/setuid/largefiles on Mon Nov  1 06:05:46 1999
/proc on /proc read/write/setuid on Mon Nov  1 06:05:46 1999
/dev/fd on fd read/write/setuid on Mon Nov  1 06:05:46 1999
/export on /dev/dsk/c0t3d0s3 setuid/read/write/largefiles on Mon Nov  1 06:05:49 1999
/export/swap on /dev/dsk/c0t3d0s4 setuid/read/write/largefiles on Mon Nov  1 06:05:49 1999
/tmp on swap read/write on Mon Nov  1 06:05:49 1999
```

> 注意
> 以数字符号 (`#`) 开头的行是注释，其后直到行尾的所有内容都会被忽略。要将长行拆分为较短的行，请在行尾放置反斜杠 (`\`)。条目的最大字符数为 1024。

现在键入以下内容：

```
ls /net/apollo/export
```

你会注意到`automountd`挂载文件系统时有一点延迟；然后系统作出如下响应：

```
files  lost+found
```

列出的文件位于`apollo`上的`/export`目录中。如果你键入`mount`，你会看到一个之前未列出、挂载在`apollo`上的文件系统：

```
mount
/ on /dev/dsk/c0t3d0s0 read/write/setuid/largefiles on Mon Nov  1 06:05:46 1999
/usr on /dev/dsk/c0t3d0s6 read/write/setuid/largefiles on Mon Nov  1 06:05:46 1999
/proc on /proc read/write/setuid on Mon Nov  1 06:05:46 1999
/dev/fd on fd read/write/setuid on Mon Nov  1 06:05:46 1999
/export on /dev/dsk/c0t3d0s3 setuid/read/write/largefiles on Mon Nov  1 06:05:49 1999
/export/swap on /dev/dsk/c0t3d0s4 setuid/read/write/largefiles on Mon Nov  1 06:05:49 1999
/tmp on swap read/write on Mon Nov  1 06:05:49 1999
/net/apollo/export on apollo:/export nosuid/remote on Fri Nov  5 09:48:03 1999
```

`automounter`自动挂载位于`apollo`上的`/export`文件系统。现在再次查看`/etc/mnttab`文件，你会看到额外的条目：
