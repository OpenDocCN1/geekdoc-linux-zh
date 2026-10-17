
`chkconfig`需要在实际`init`脚本中添加额外的注释行，以告诉它服务应该在哪些运行级别下启动，以及在运行级别初始化期间，服务相对何时应该启动。`init`脚本按特定顺序处理，以确保依赖于其他服务的在所依赖的服务之后启动。这些取自`http` `init`脚本的行如下：

```bash
# chkconfig: 345 8 15
# description: Apache 是一个世界维网服务器。它被用于提供
# HTML 文件和 CGI。
```

第一行是`chkconfig`的标记，它告诉工具给定脚本应适用于运行级别`3`、`4`和`5`，启动顺序为`8`，停止顺序为`15`。

> 什么是健康检查器？
> 
> 解决问题的工具

# 使用 chkconfig 列出服务

要获取哪些服务在哪个运行级别启动的列表，请使用`chkconfig --list`命令。可选，你可以添加一个名称作为额外参数，`chkconfig`将仅列出该服务的信息。以下是输出：

```bash
[user@host ~]$ /sbin/chkconfig --list httpd
httpd 0:off 1:off 2:off 3:on 4:on 5:on
```

在这种情况下，`chkconfig`报告`httpd`在运行级别`3`、`4`、`5`上启动。

## 使用 chkconfig 服务

要从某个运行级别移除服务，请使用以下命令：

`chkconfig --level <runlevel> <servicename> off`

`runlevel`是你想修改的运行级别，`servicename`是服务的名称。`on`和`off`分别启用和禁用服务。例如，要关闭运行级别`3`的`httpd`，你需要执行以下命令：`chkconfig --level 3 httpd off`

此命令仅从特定的运行级别移除服务，这是最常见的操作。你可以列出多个运行级别，例如，可以在命令行输入`345`来更改多个运行级别的设置。如果你需要完全删除服务，将使用以下命令：`chkconfig --del httpd`

此命令的效果是从所有`rc.d`目录目录移除`httpd`。它不会从`/etc/rc.d/init.d`目录中删除服务的脚本，只是删除了指向该文件的符号链接。

## 使用 chkconfig 添加服务

要在特定运行级别上添加服务，请使用以下命令：

`chkconfig --level <runlevel> <servicename> on`

将`httpd`添加回运行级别`3`，使用以下命令：`chkconfig --level 3 httpd on`

要根据`chkconfig`给出的建议向所有运行级别添加新服务，请使用以下命令：`chkconfig --add <servicename>`

`chkconfig`会一次性在正确的目录中设置服务的所有链接。

## 重置服务信息

玩玩服务是有益的，只要你有`/etc/rc.d`目录树的备份，并且有一种重新进入系统进行恢复的方法。然而，这种激进的操作通常是不必要的。相反，你可以通过以下命令将服务的启动优先级和其他信息恢复到建议的设置。

# 第五部分 系统管理

## 第 29 章 管理应用程序

它非常先进，甚至可以将`FTP`或`HTTP` `URL`作为包名。某些安装选项如表 29.1 所示。

| 选项 | 描述 |
| :--- | :--- |
| `-v` | 输出`rpm`正在执行的操作 |
| `-h` 或 `--hash` | 在安装包时打印 50 个哈希标记或井号 `#` |
| `--percent` | 在从包中提取文件时打印百分比 |
| `--test` | 运行软件包安装过程，但不安装任何内容；主要用于检测冲突 |
| `--excludedocs` | 防止安装被标记为文档如`man`页面的文件 |
| `--includedocs` | 强制安装标记为文档的文件；这是默认设置 |
| `--nodeps` | 在安装包之前不进行依赖关系检查 |
| `--replacefiles` | 允许用正在安装的包中的文件替换已安装的文件 |
| `--replacepkgs` | 允许用正在安装的包替换已安装的包 |
| `--oldpackage` | 允许用旧版本替换已安装的包版本包 |
| `--Force` | 强制安装包 |

在给`rpm`提供选项时，无论何种模式，所有的单字母选项称为短选项都可以合并写一个块中：

```
# rpm -i -v kernel-2.2.12-20.i386.rpm
```

此命令等同于以下：

```
# rpm -ivh kernel-2.2.12-20.i386.rpm
```

所有以`--`开头的选项称为长选项必须单独给出。

现在我们来看几个安装`rpm`包的示例。第一个示例是从以下包`defrag-0.73-5.i386.rpm`安装`defrag`一个文件系统碎片整理器：

### 安装 rpm 包

1. `rpm`软件包通常遵循标准的命名规范：`name-version-release.rpm`
   `name`是包名，`version`是包的版本，`release`是包的发布级别，`arch`是包对应的硬件架构，而`rpm`是默认扩展名。这种命名方案非常方便，因为仅通过查看名称就可以确定特定包的一些基本信息。
2. 在此示例中，版本`0.73`、发布`5`的`defrag`包被安装在`i386`架构的计算机上。
3. 使用`cd`切换到包含`RPM`的相应目录，或者找到可以下载包的`URL`，使用`rpm`命令的`i`、`v`和`n`选项安装`defrag`，后面跟着`defrag` `rpm`文件的名和`URL`，如下：

```
# rpm -ivh http://contrib.redhat.com/contrib/libc6/i386/defrag-0.73-5.i386.rpm
```

在安装包时，输出将如下：

`defrag`

```
#################
```

安装完成后，将显示 50 个哈希标记。

在这个示例中，我使用井号`#`来表示`root`提示符，因为`root`可以为整个系统正确安装包。如果你尝试用`root`以外的用户身份安装此包，将生成类似下面的错误：

```
failed to open /var/lib/rpm/packages.rpm
error: cannot open /var/lib/rpm/packages.rpm
```

偶尔，安装的文件会与之前安装的包的文件发生冲突。如果你安装了`defrag`版本`0.65`，将生成以下消息：

```
/sbin/edefrag conflicts with file from defrag-0.65-5
error: defrag-0.73-5.i386.rpm cannot be installed
```

如果你仍然想安装这些文件，可以在命令中添加`--replacefiles`选项。

另一种类型的冲突有时被称为依赖关系冲突。这发生在安装某个包时，需要某些包才能正常运行的情况。例如，你可能尝试安装以下包：

```
# rpm -ivh quicktest-1.5.2-1.i386.rpm
```

你可以得到以下依赖关系：

```
failed dependencies:
kernel >= 2.2.12 is needed by quicktest-1.5.2-1
quicktest = 1.5.1 is needed by xquicktest-1.0.1-1
```

# 第五部分 系统管理

## 第 27 章 管理守护进程

### 列表 27.1 继续

```
39:
40:    exit 1
41: esac
42:
43:    exit 0
```

在系统中将另一个程序设置为守护进程的最简单方法是将现有脚本复制到新文件中，并根据你的需要编辑该文件。列表 27.1 所示脚本中特定于`httpd`的行是`3–7`、`18–21`、`24–28`和`33`行。这些行在脚本执行时提供反馈，或实际启动程序。

第`25`行和`28`行是`Apache`特有的，因为`Apache`将其进程`ID`编号存储在`/var/run/httpd`下的一个文件中。注意，这里没有删除`/var/run`中`PID`文件的行。如果你的程序名为`mydaemon`，第`24–28`行看起来像这样：

```
24:    echo -n "Shutting down mydaemon :"
25:    kill mydaemon
26:    echo mydaemon
27:    rm -f /var/run/mydaemon
28:    ;;
```

## init 脚本清单

使用此清单可以确保你和系统管理员都拥有必要的功能。

- 确保脚本处理`/var/lock/subsys`中的锁文件和`/var/run`中的`PID`文件；包含了`status`命令行参数和`kill`函数。
- 支持`start`和`stop`命令行参数。如果你的进程依赖于另一个进程的运行，确保你的进程具有较大的数字。
- 确保脚本提供了适当的反馈，向用户说明正在发生什么。如果守护进程正在启动需要时间的连接，请特别注意这一点。
