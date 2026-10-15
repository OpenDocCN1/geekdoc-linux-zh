
> **注意**：你看到的错误只是 `quota check` 命令告诉你配额文件尚未包含数据，但它会用正确的信息更新它们。

### 8. 使用以下命令编辑该用户的配额设置：

- `edquota -u quotaboy`

### 9. 你会在 vi 中看到用户的配额信息，因此可以编辑数值，如下所示：

```
Disk quotas for user quotaboy (uid 500):
Filesystem blocks soft hard inodes soft hard
/dev/sdb5 0 0 0 0 0 0
```

### 10. 将 quotaboy 的块配额设置为匹配以下内容：

```
Filesystem blocks soft hard inodes soft hard
/dev/sdb5 0 5000 6000 0 0 0
```

### 11. 保存并退出文件；它将被配额系统正确加载。

> **警告**：在配置其配额期间，不应有任何用户访问 `/data` 文件系统。如果可能，请使用 `service network stop` 命令关闭网络，或者通过 `touch` 命令创建 `/etc/nologin` 文件来禁用登录。

### 12. 以 quotaboy 身份登录，或使用 `su -` 命令切换为 quotaboy：

- `su - quotaboy`

### 13. 作为 quotaboy 在 /data 目录中创建一个新文件：

- `touch /data/file1.quotaboy`

### 14. 退出 quotaboy 用户，并以 root 用户身份再次运行 `quotacheck` 命令：

- `quotacheck -avug`
  - `quotacheck: Scanning /dev/sdb5 [/data] done`
  - `quotacheck: Checked X directories and XXX files`

> **注意**：有时你需要运行几次 `quotacheck` 命令才能让用户显示在配额输出中。使用 `repquota -a` 命令可以显示所有用户的配额和状态。

### 15. 作为 root 用户，检查 quotaboy 是否列出了配额：

- `quota quotaboy`
  - `Filesystem blocks quota limit grace files quota limit grace`
  - `/dev/sdb5 0 5000 6000 1 0 0`

### 16. 为 /data 文件系统启用配额系统：

- `quotaon /data`

### 17. 以 quotaboy 身份登录或 `su` 切换到他的账户：

```
su - quotaboy
```

### 18. 运行 `quota` 命令查看 quotaboy 当前的使用情况：

```
quota
Disk quotas for user quotaboy (uid 501):
Filesystem blocks quota limit grace files quota limit grace
/dev/sdb5    0   5000  6000      0     0   0   0
```

### 19. 作为 quotaboy 用户，将 /etc 目录中的所有常规文件复制到 /data 目录：

```
cp /etc/* /data
```

### 20. 运行 `quota` 命令查看已使用和空闲的块数量：

```
Disk quotas for user quotaboy (uid 502):
Filesystem blocks quota limit grace files quota limit grace
/dev/sdb5    2524  5000  6000      152    0   0   0
```

### 21. 通过复制整个 /etc/ 树到 /data 目录来填满你的配额，注意观察关于磁盘配额超限的多个错误：

```
cp -r /etc /data
```

### 22. 务必清理测试系统中的混乱，并反复尝试，直到你熟悉配额的配置为止。

为了确保当用户位于系统上时配额始终处于开启状态，请将 `quotaon` 和 `quotacheck` 命令添加到脚本中，并让 `/etc/rc.d/rc.sysinit` 或类似的脚本在文件系统挂载后调用它们。

## 硬限制和软限制

剖析 `edquota -u quotaboy` 编辑器会话非常重要，因为其中有几项内容可能会出现在考试中。让我们看看输出的每个部分：

```
Filesystem blocks soft hard inodes soft hard
/dev/sdb5    0     0   0     0   0   0
```

各部分的描述如下：

- `Filesystem`（文件系统）——这是用户拥有配额的文件系统。
- `blocks`（块）——这是用户在当前文件系统中目前使用的块数。
- `soft`（软限制）——这是软限制，在宽限期内可以被超过。
- `hard`（硬限制）——这是硬限制，不可以被超过。
- `inodes`（索引节点）——这是目前正在使用的索引节点数量。
- `soft`（软限制）——如果设置，这是你想为其设置软限制的索引节点数量（如果你不知道该用什么值，就不要使用它）。
- `hard`（硬限制）——这是索引节点的硬限制，如果达到此限制，用户将无法创建更多文件。

可编辑的字段是块和索引节点的软限制和硬限制设置。编辑其他任何值都没有作用。

## 设置宽限期

使用 `edquota -t` 来设置用户的宽限期；它的配置单位可以是天、小时、分钟或秒。如果你配置了一个小于一天的宽限期，那你真是个相当严厉的系统管理员。其语法如下：

```
edquota -t
```

要在对用户执行软限制之前建立宽限期，请使用以下命令，其中时间单位可以是天、小时、分钟或秒：

```
FileSystem Block grace period Inode grace period
/dev/sdb5 7days 7days
```

## 获取配额信息

作为普通用户运行 `quota` 命令以获取该用户的配额信息（如前一个练习所示）。如果该用户没有配额，输出将说明没有配额。

root 用户有能力获取所有用户的配额统计数据，如下所示：

```
repquota -a
*** Report for user quotas on device /dev/sdb5
Block grace time: 7days; Inode grace time: 7days

 User used soft hard grace used soft hard grace
 root -- 32844 0 0 5 0 0
 snuffy -- 0 0 0 1 0 0
 quotaboy +- 6000 5000 6000 6days 1464 0 0
```

## 文件属性

许多系统管理员认为 Linux 文件系统上的文件没有任何特殊或隐藏属性，但实际上有一些属性可以帮助简化工作并加快系统速度，如果它们还能增强安全性那就更好了。

文件对象的特殊属性通过 `chattr` 命令设置，并通过 `lsattr` 命令查看。这些属性包括：

- `A`——修改时不更新访问时间。
- `a`——仅允许追加写入。
- `c`——压缩；文件从其自然状态进行压缩。
- `d`——不转储；当执行 `dump` 命令时，排除设置了此属性的文件。
- `i`——不可变；无法对文件进行更改，它不能被修改。
- `s`——安全删除；删除时内容会被清零。
- `u`——不可删除；除非重置该属性，否则文件不能被删除。
- `S`——执行同步更新。

选项的三个限定符是 `+`，用于添加或设置选项；`-`，用于移除选项；以及后跟多个选项的 `=`。使用 `=` 运算符会用新属性覆盖当前属性。

作为一个设置有用属性的例子，让我们假设你有一个用户，她行为不端，但她要么不使用 bash shell 来实施她的恶行，要么在事后擦除了 `.bash_history` 文件中的条目。

你可以使用以下命令将该用户的 `.bash_history` 文件设置为仅允许追加：

```
chattr +a /home/baduser/.bash_history
```

我在一家公司工作过，那里曾利用此功能来发现一位篡改重要数据库以谋取私利的管理员。仅允许追加的选项甚至不允许用户删除违规文件。用户无法覆盖该文件，除了尽可能多地输入命令，希望能将定罪的那些行挤出 1000 行长度的历史缓冲区之外，几乎无事可做。
