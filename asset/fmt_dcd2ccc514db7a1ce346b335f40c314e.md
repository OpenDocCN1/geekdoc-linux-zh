
| bufused bufsize numrecs numpages numwrites recs/pages pages/io |
|---|---|---|---|---|---|---|---|
| L-3 | 0 | | 21 | 5 | 5 | 4.2 | 1.0 |
| Subsystem numrecs Log Space used |
|---|---|---|---|
| OLDRSAM | 21 | | 1092 | |
| address number flags uniqid begin size used used |
|---|---|---|---|---|---|---|---|
| 10039324 | U---- | 1 | 100233 | 250 | 250 | |
| 10039340 | U---- | 2 | 10032d | 250 | 250 | 100.0% |
| 1003935c | U---- | 3 | 100427 | 250 | 250 | 100.0% |
| 10039378 | U---- | 4 | 100521 | 250 | 250 | 100.0% |
| 10039394 | U---- | 5 | 10061b | 250 | | | |
| 100393b0 | U---L | 6 | 100715 | 250 | 7 | 2.50% |

你还会注意到，我们在创建 `physdbs` 数据库空间之后执行了 `onantame` 命令。这对于让 `physdbs` 数据库空间变得可用至关重要。运行 `onstat -l` 显示逻辑日志文件的输出也发生了变化，因为我们使用 `onantame` 执行备份命令。现在运行 `onstat -d` 命令，在我们转出物理日志后再次运行它。

```
rebel:root # onstat -d
```

Informix Dynamic Server Version 7.30.UC10 -- Quiescent-Up 00:52:05 -- $888$ Kbytes

数据库空间

| address number flags fchunk nchunks flags owner name |
|---|---|---|---|---|---|---|---|
| 1011e13c | 1 | | 1 | 1 | | N | informix rootdbs |
| 1011efa8 | 2 | | 2 | 1 | | N | informix physdbs |

2 个活动，2047 最大

块 (Chunks)

| address chk/dbs offset free bpages pathname |
|---|---|---|---|---|---|
| 1011eff8 | 1 | 0 | 10000 | 6921 | /opt/data/rootdbs |
| 1011f064 | 2 | 0 | 10240 | 1187 | /opt/data/physdbs |

2 个活动，2047 最大

现在你可以看到 `physdbs` 空间了。输出显示的大小是不正确的，但你只需将其乘以二，就是 20MB。运行 `onparams` 查看可用选项。

```
onparams
用法: -a DBSpace [-s size]
       -d log [-y]
       -p size [-y]
-a - 添加逻辑日志
-d - 删除逻辑日志
-p - 修改物理日志的大小和位置
-y - 对所有提示回答"yes"
```

我们将使用 `-p` 选项创建一个 20MB 的 `physdbs`。记住，我们最初为物理日志分配了 50MB，但只使用了 20MB。这将为我们留出增长空间。创建 `physdbs`，请使用以下 `onparams`：

```
onparams -p 50000 -physdbs -y
```

观察运行命令时发生了什么：

```
rebel:root # onparams -s 20000 -d physdbs -y
正在关闭，请稍候 ...
正在初始化，请稍候 ...
正在恢复，请稍候 ...
rebel:root # onstat -d
```

Informix Dynamic Server Version 7.30.UC10 -- Quiescent-Up 00:00:31 -- 8288 Bytes

| address number flags chunk nchunks flags owner name |
|---|---|---|---|---|---|---|---|
| 1011e3c | 1 | | 1 | | N | informix rootdbs |
| 1011e428 | 2 | | 1 | | N | informix physdbs |

2 个活动，2047 最大

| address chk/dbs offset size free bpages pathname |
|---|---|---|---|---|---|
| 1011ef8 | 1 | 0 | 10000 | 7421 | /opt/data/rootdbs |
| 1011e348 | 2 | 0 | 10240 | 187 | /opt/data/physdbs |

2 个活动，2047 最大

物理日志原始大小为 1MB，这是引擎安装时的默认值。现在我们可以看到它在我们新的 20MB `physdb` 中使用了字节。你会发现 `rootdbs` 获得了 1MB 的可用空间。当我们转出逻辑日志时，`rootdb` 将获得更多。如果你查看 `/opt/data` 目录，你会看到你创建的新物理日志数据库：

```
rebel:root # ls -1
total 40643
drwxr-xr-x 2 informix informix 1024 Jan 24 11:14 .
drwxr-xr-x 17 root root 1024 Jan 18 10:22 .
-rw-rw-r-- 1 informix informix 20971520 Jan 24 12:25 physdb
-rw-rw-r-- 1 informix informix 20480000 Jan 24 12:25 rootdbs
```

`Physdb` 也比 `rootdbs` 略小——这是因为我们所有的命令引用的 KB 而非 MB。20000KB 等于 20480MB（即我们给 `rootdbs` 的大小）。20480KB 等于 20971520 字节，即 `physdbs` 的实际大小，这是我们在使用 `onspaces` 命令使用 KB 大小时创建的。

在大多数情况下，几乎没有例外，Informix 命令将引用 KB 而非 MB 信息。注意 Informix 命令的这一特征非常重要，即要在正确的语境中使用它们；即你首先考虑的是 KB，而不是 MB。你可以考虑 MB，但仅限于 KB 转换为 MB 的角度。

# Logdbs

现在，让我们为目前位于 `rootdbs` 中的逻辑日志创建 `logdbs`。确保你的引擎处于静止模式，然后按照以下步骤创建 `logdbs`。

我们将创建 20 个逻辑日志，每个 1MB，因此我们需要至少 26MB 的逻辑日志数据库空间，甚至更多，将其做得大一点是个好主意，这样你就可以根据需要添加更多日志。我们的第一个 `logdbs` 将是 50MB，以留出一些增长空间。我们在 `rootdbs` 中六个逻辑日志，想要添加 20 个，所以我们将创建 26 个。

```
rebel:root # onspaces -c -d logdbs -p /opt/data/logdbs -o 0 -s 50000
```

正在验证物理磁盘空间，请稍候 ...

空间添加成功。

> **警告** 需要对 Root DBSpace 进行层 0 归档。

```
rebel:root # ontape -s -L 0
```

到磁带设备 '/dev/null/' 的归档已完成。

# 第 4 章 • 在 Linux 上安装 Informix

通过运行 `onmode -sy` 命令确保引擎处于单用户模式：

```
rebel:root # onmode -sy
```

执行零级备份以清理任何未处理的日志条目。

```
rebel:root # ontape -s -L 0
```

归档到带设备 '/dev/null' 已完成。

```
Program over.
rebel:root # onstat -ld
```

Informix Dynamic Server 版本 7.30.UC10 -- 在线 -- 运行 00:19:33 -- 8888 Kbytes

| 地址 | 数量 | 标志 | fchunk | nchunks | 标志 | 所有者 | 名称 |
|---|---|---|---|---|---|---|---|
| 1011e13c | 1 | 1 | | 1 | 1 | N | informix | rootdbs |
| 1011e508 | 2 | 1 | | 2 | 1 | N | informix | physdbs |
