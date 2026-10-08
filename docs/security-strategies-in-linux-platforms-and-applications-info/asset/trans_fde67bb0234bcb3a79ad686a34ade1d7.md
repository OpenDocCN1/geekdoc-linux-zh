

# 第 13 章 测试与报告

例如，标准的 Tripwire 配置会报告 `/proc/` 和 `/dev/` 目录下的文件变化。当前的 Linux 系统在每次系统重启时，都会更改这些目录中许多文件的内容或访问时间。如果系统通过 DHCP 获取网络地址信息，当前的 Linux 系统还可能会更改 `/etc/` 目录下的文件。可以使用以下命令更新 Tripwire 策略：

```bash
# tripwire --update
```

然后，得益于 `/etc/cron.daily/` 目录下的 tripwire 脚本，标准的 Tripwire 包被配置为每天对本地系统进行检查。

# 使用高级入侵检测环境 (AIDE) 进行测试

与 Tripwire 类似，AIDE 支持对已安装和配置的文件进行定期检查。AIDE 已在第 12 章中讨论过。本节将根据 `aide.conf` 配置文件的信息，进一步深入介绍 AIDE 的工作原理。Ubuntu 和 Red Hat 系统的配置可能有所不同。当然，细节可能会发生变化，特别是当某个系统的开发人员认为另一种方法更好时。

无论何种情况，AIDE 规则都如表 13-3 所示通过属性进行定义。一些开发者认为 AIDE 优于 Tripwire。事实上，AIDE 包可以从 Ubuntu 主仓库和 Red Hat Enterprise Linux (RHEL) 存储库获取。这两种发行版至少在某些方面都支持 AIDE 的安装。

# Ubuntu AIDE

当安装在 Ubuntu 系统上时，AIDE 的配置位于 `/etc/aide/` 目录下的文件中。此外，通过 `/etc/default/aide` 文件，单个服务的配置选项被定义在 `/etc/aide/aide.conf.d/` 目录下的文件中。虽然基础数据库文件相似，但 AIDE 的版本在 `/etc/aide/aide.conf` 文件中包含了带有默认代码组合的指令。

例如，以下指令建议 AIDE 可以对每个文件使用多种校验和。每个选项都列在表 13-3 中。

```bash
Checksums = md5+sha1+md5160+haval+ gost+crc32
tiger-whirlpool
```

`OwnerMode` 指令用于计算所有配置文件的权限、用户所有者和组：

```bash
OwnerMode = p+u+g
```

`Size` 指令应用于文件，通过固定大小可以帮助判断文件的大小和块数是否发生了变化：

```bash
Size = s+b
```

`aide.conf` 文件中的其他指令描述了应用于 `/etc/aide/aide.conf.d/` 目录下文件的额外指令。

# 表 13-3 AIDE 规则代码。

| 代码 | 描述 |
|---|---|
| p | 权限：读、写、执行 |
| i | Inode：卷或分区上的标记位置 |
| n | 链接数 |
| u | 用户 |
| g | 组组 |
| s | 大小 |
| b | 块数 |
| m | 修改时间；所有权或权限上次更改的时间 |
| a | 访问时间；文件最后一次被读取或访问的时间 |
| c | 更改时间；文件最后一次更改的时间 |
| S | 预期大小会变化的文件标签，例如日志文件 |
| acl | 访问控制列表 (ACL) 标签 |
| selinux | 安全增强 Linux (Security Enhanced Linux) 上文 |
| attr | 扩展文件属性 |
| md5 | 消息摘要 5 (MD5) 校验 |
| sha | 安全哈希算法 (SHA) 版本 1 哈希函数；也可能指 256 位哈希函数的 sha256 |
| rmd160 | 基于消息摘要 4 (MD4) 哈希的 Java 校验算法的哈希函数；rmd 缩写是指代 RACE Integrity Primitives Evaluation Message Digest |
| haval | 输出长度可变的加密哈希函数 |
| gost | 原本在苏联苏联开发的加密哈希函数 |
| crc32 | 基于循环冗余校验 (CRC) 的加密哈希函数 |
| whirlpool | 另一种加密哈希函数 |

# 第 13 章 测试与报告

## Red Hat AIDE

相比之下，Red Hat 的 AIDE 配置大部分自包含在 `/etc/aide.conf` 文件中。定义的指令有所不同，且在某些方面是累积的。这里的 R 指令定义了如表 13-3 所示的代码组。

```bash
R: p+i+n+u+g+s+m+c+acl+selinux+xattrs+md5
```

该组被插入此处 `NORMAL` 指令的值中，该指令包含了两个校验哈希函数。

```bash
NORMAL = R-rmd160+sha256
```

后续指令实际上创建了一个等同于 R 代码组的 DIR 指令

```bash
DIR = p+i+n+u+g+acl+selinux+xattrs
```

某些文件只需要检查访问控制，如此处定义的 PERMS 指令所示。该指令本质上是对普通权限访问权限、所有权、ACL 和 SELinux 上文的检查：

```bash
PERMS = p+i+n+u+g+acl+selinux
```

图 13-6 显示的 `/etc/aide.conf` 摘了对关键目录的默认检查。几个文件前面带有 `!` 字符（称为“bang”），表示排除。换句话说，在此配置中，`/usr/src/` ... (省略)

