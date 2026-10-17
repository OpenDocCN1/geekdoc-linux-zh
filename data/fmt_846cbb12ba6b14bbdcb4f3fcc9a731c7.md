
# `gpg --import RPM_GPG_KEY`

```
```

然后你可以可以使用类似命令验证完整性和真实性：

```bash
# rpm --checksig pkg-0.0.rpm
```

如果你不想使用 GPG，可以使用此命令仅检查完整性：

```bash
# rpm --nogpg pkg-0.0.rpm
```

## 添加和删除组件

RPM 使得在系统中添加和删除软件包变得简单。它包含一个关于添加、升级和删除软件包的正确方法，使得只需运行单个命令即可完成添加和删除。

## 第 4 章：基础配置与管理

此错误表示 Penguin 包安装失败，因为它需要版本 7.1 或更高版本的 Iceberg 包。你必须找到并安装 Iceberg 包以及 Iceberg 可能需要的任何其他包。

最后，RPM 会检查是否有任何配置文件会被此包的安装所覆盖。RPM 会尝试对冲突处理做出智能决策。如果 RPM 用新包中的文件替换了现有的配置文件，屏幕上将显示警告。

```
# rpm -i penguin-3.26.i386.rpm
warning: /etc/someconfig saved as /etc/someconfig.rpmsave
```

由你来查看这两个文件，并决定是否以及需要进行哪些修改。

### 升级模式

`-u` 选项用于升级现有软件包。例如，如果已经安装了 3.25 版本的 Penguin 工具，执行命令：

```
# rpm -u penguin-3.26.i386.rpm
```

将把旧版本的软件包替换为新版本。事实上，RPM 升级模式的特性之一是，旧软件包甚至不需要存在。在这种情况下，`-u` 的作用与 `-i` 相同。

### 模式

`-e` 命令从系统中删除软件包。与安装模式一样，RPM 在允许你删除软件包之前会进行一些清理工作。首先，它执行依赖性检查，以确保没有其他正在删除的软件包依赖于它。如果你修改了任何配置文件，RPM 会创建该文件的副本，在末尾添加 `.rpmsave`，然后删除原始文件。最后，在从系统和 RPM 数据库中删除所有文件后，它会在数据库中移除包名。

注意：请务必小心你从系统中删除哪些软件包。与大多数 Linux 工具一样，RPM 假设自己是全知的，并且会静默地让你“自毁”。删除 `passwd` 或 `kernel` 包将是灾难性的。

### 添加更新、安全修复和其他项目

Red Hat Linux 在不断更新。当发现漏洞或安全问题时，它们会被发布在 Red Hat 的 Errata 页面，地址为：http://www.redhat.com/support/docs/errata.html。你应该定期检查此页面以确保你的系统是最新状态。

### 练习 4-5

#### 从 Red Hat Errata 页面更新

每当你检查错误列表页面时，都可以遵循以下良好的检查清单：

- 1. 访问 http://www.redhat.com/support/docs/errata.html。选择 Red Hat Linux General Errata 链接。
- 2. 滚动到 Overview 部分。浏览列表，选择列出的每个包。
- 3. 如果你的系统中加载了受影响的包，考虑使用推荐的替换包进行升级。
- 4. 在替换受影响的包之前，考虑其影响。你可能需要将系统切换到单用户模式或进行重启。
- 5. 执行升级时，注意配置文件的警告。如果你的本地配置文件被新文件替换，你可能需要更改新的配置文件以反映你当前的设置。
- 6. 彻底测试新包。确保你已正确配置。
- 7. 如果某个包列在错误列表中但未安装在你的系统中，可能没有理由现在将其安装到你的系统中。仔细阅读该包的详细错误条目，仅在需要时才安装。

Red Hat 现在包含了一个 RH Network Software Manager 服务，你可以配置它来检查修订后的包、新包、错误列表和其他信息。你可以通过在 www.redhat.com/network/ 注册获得该服务的免费预览订阅；之后将收取服务费用。

### 验证一个或多个软件包

验证已安装的软件包会将该包的信息与系统中 RPM 数据库的信息或原始包的信息进行比较。验证会对包中的每个文件的尺寸、MD5 校验和、类型、所有者和组进行检查。以下是一些验证示例：

- 验证所有包
  `# rpm --verify -a`
- 验证某个 RPM 包内的所有文件
  `# rpm --verify -p fileutils-4.0-1.i386.rpm`
- 验证属于特定包的文件
  `# rpm --verify --file /bin/ls`

如果你正在验证文件或包

```
# rpm --verify --file /bin/vi......G.bin/vi
```

表 4-7 列出了错误代码及其含义。

### 查看安装的包

如果没有 RPM，你需要搜索文件系统来确定某个软件包是否已安装。RPM 可以让你轻松找出安装了哪些包以及关于这些包的信息。

### 查询模式

RPM 的优势之一是，理想情况下系统中的每个软件包或应用程序都得到了记录。使用 RPM 的查询模式，可以确定系统中安装了哪些包，或者某个文件属于哪个包。

#### 表 4-7 错误代码

| 错误代码 | 含义 |
|---|---|
| 5 | MD5 校验和 |
| S | 文件尺寸 |
| L | 符号链接 |
| T | 文件修改时间 |
| D | 设备 |
| U | 用户 |
| G | 组 |
| M | 模式 |

如果你想找到属于某个特定包的文件，这非常有帮助。查询模式还可以用于在安装 RPM 包之前识别其中包含哪些文件。这让你在文件实际写入系统之前查看它们。`-q` 选项用于查询软件包。单独 `-q` 会给你指定包的版本。如果你想查看系统中哪个版本的 `tin`，请执行以下命令：

```
# rpm -q tin
tin-1.4.4-2
```

如果你想查看哪个已安装包拥有某个文件，使用 `-f`。这里我们要查看哪个包拥有 `/etc/passwd`。

```
# rpm -q -f /etc/passwd
setup-2.3.4-1
```

同样，如果你想生成某个特定包的文件列表，使用 `-l` 选项。

```
# rpm -q -l tin
/etc/X11/app/Internet/tin.desktop
/usr/bin/rtin
/usr/bin/tin
/usr/share/doc/tin-1.4.4
/usr/share/doc/tin-1.4.4/README
/usr/share/doc/tin-1.4.4/doc
/usr/share/doc/tin-1.4.4/doc/CHANGES
/usr/share/doc/tin-1.4.4/doc/CHANGES.old
/usr/share/doc/tin-1.4.4/doc/DEBUG_REFS
/usr/share/doc/tin-1.4.4/doc/INSTALL
/usr/share/doc/tin-1.4.4/doc/TODO
/usr/share/doc/tin-1.4.4/doc/WHATSNEW
/usr/share/doc/tin-1.4.4/doc/auth.txt
/usr/share/doc/tin-1.4.4/doc/good-netkeeping-seal
/usr/share/doc/tin-1.4.4/doc/internals.txt
/usr/share/doc/tin-1.4.4/doc/iso2asc
/usr/share/doc/tin-1.4.4/doc/pgp.txt
/usr/share/doc/tin-1.4.4/doc/rcvars.txt
/usr/share/doc/tin-1.4.4/doc/reading-mail.txt
/usr/share/doc/tin-1.4.4/doc/tin.1
/usr/share/doc/tin-1.4.4/doc/tin defaults
/usr/share/doc/tin-1.4.4/doc/umlaute
/usr/share/doc/tin-1.4.4/doc/umlafts
/usr/share/man/man1/tin.gz
```

`-q` 最常见的修饰之一是 `-a`，它查询所有软件包。默认的工作站系统安装了超过 350 个包。以下是截断输出：

```
# rpm -a
chkconfig-1.2.16-1
sed-3.02-8
psmisc-19-4
XFree86-libs-4.0.1-1
glib-1.2.8-4
wmconfig-0.9.9-3
fig-3.2.3c-3
toolwait-1.2-5
```

如需获取关于软件包的更多信息，使用 `-i`（信息）修饰符。

```
# rpm -i passwd
Name                : passwd              Relocations: (not relocable)
```
