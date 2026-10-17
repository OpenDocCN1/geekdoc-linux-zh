
如果你的系统中没有这些资源，很可能原因是未加载`howto-5.2-2.src.rpm`（Red Hat 5.2）或`howto-6.0-4.src.rpm`（Red Hat 6.0）软件包（有关 RPM 软件包的更多信息，请参阅第 26 页 *Red Hat 软件包管理器*）。如果你不能或不想加载这些或其他文档软件包，一些优秀的网络资源可供使用。有关大多数 Linux 组件的最新文档可在`http://metalab.unc.edu/LDP/`找到，而特定于 Red Hat 发行版的文档可在`http://www.redhat.com/support/`找到。

## 启动脚本

内核启动序列的最后一步（由 LILO 或其他启动加载器调用）是启动进程`/sbin/init`。`init`进程读取配置文件`/etc/inittab`，该文件告知`init`应启动哪些进程以及达到哪个运行级别。系统的运行级别描述了基于正在运行的进程的系统状态。运行级别用包含 0 到 9 的整数以及`s`或`S`（单用户模式的同义词）表示。默认情况下，未配置运行级别 7、8 和 9。针对特定运行级别启动和/或停止的进程由`/etc/inittab`文件中的指令以及`/etc/rc.d/rcN.d`目录中的启动脚本决定，其中`N`可以是 0 到 9 之间的任意整数。因此，正是这些启动脚本（通常称为启动/停止或启动/终止脚本）定义了运行级别。

你可以通过执行`init N`来更改运行级别，其中`N`是 0 到 9 之间的任意整数，或者是`s`或`S`。如果运行级别未定义，`init`将直接退出。你可以通过执行`/sbin/runlevel`命令来确定系统当前的运行级别。

有关`init`和`runlevel`的更多信息可在`init(8)`和`runlevel(8)`手册页中获取。有关此主题的更完整细节，请查阅以下书籍：

- Hein, Jochen, *Linux Companion for System Administrators*，Harlow, England, Addison Wesley Longman Limited, 1999.

- Komarski, Mark F., and Cary Collett, *Linux System Administrator’s Handbook*，Upper Saddle River, New Jersey, Prentice Hall PTR, 1998.

或其他类似资源。

我们将在本书的不同部分提到启动脚本。在这里，我们将简要描述启动脚本的结构、常见用法以及操作。

默认情况下，除了`/etc/rc.d/rc.local`之外的所有启动脚本都位于目录`/etc/rc.d/init.d`中。前面提到的`/etc/rc.d/rcN.d`目录中的脚本是指向`/etc/rc.d/init.d`中条目的符号链接（有关符号链接的信息请参阅`ln(1)`手册页）。`/etc/rc.d/init.d`中的每个脚本可以接受多个参数，但至少会接受两个参数：`start`和`stop`。当以`start`参数执行脚本时，该脚本控制的进程将启动。当给出`stop`参数时，进程将终止。

例如，控制`/usr/sbin/lpd`守护程序的脚本`/etc/rc.d/init.d/lpd`由示例 3-4 中显示的脚本通过符号链接引用。示例 3-4 中的脚本通常仅通过`init`调用。当由`init`调用时，名称以`K`开头的脚本将导致以`stop`参数调用`/etc/rc.d/init.d/lpd`，而以`S`开头的脚本将导致以`start`参数调用`/etc/rc.d/init.d/lpd`。数字 60 用于确定相对于同一目录中其他脚本（`lpd`脚本所在的目录）的调用顺序。

### 示例 3-4 指向 `/usr/sbin/lpd` 的符号链接

```
/etc/rc.d/rc0.d/K60lpd
/etc/rc.d/rc1.d/K60lpd
/etc/rc.d/rc2.d/S60lpd
/etc/rc.d/rc3.d/S60lpd
/etc/rc.d/rc4.d/S60lpd
/etc/rc.d/rc5.d/S60lpd
/etc/rc.d/rc6.d/K60lpd
```

由于由`init`调用的所有启动脚本都是指向`/etc/rc.d/init.d`中脚本的符号链接，因此当我们需要进行更改时，只需修改`/etc/rc.d/init.d`中的那些脚本即可。每当你要添加启动脚本时，请将脚本放入`/etc/rc.d/init.d`，然后在各种`/etc/rc.d/rc*`目录（将 N 替换为适当的数字）中创建相应的`s*`和`k*`符号链接。要禁用功能，例如`sendmail`，你可以删除或重命名指向`sendmail`启动脚本`/etc/rc.d/init.d/sendmail`的符号链接。

这一结构的一个例外是`/etc/rc.d/rc.local`。默认情况下，该文件通过`/etc/rc.d/rc2.d`、`/etc/rc.d/rc3.d`和`/etc/rc.d/rc5.d`中的`s99local`被符号链接引用。它是系统进入运行级别 2、3 或 5 时调用的最后一个脚本。

如果这是你第一次接触运行级别，花点时间阅读本部分注明的参考资料是值得的。

## RED HAT 软件包管理器

Red Hat 软件包管理器 (RPM) 是管理你 Linux 系统上软件包的软件。软件包是一组相关的文件，通常提供软件的功能组件（我们说“通常”是因为有时一个软件包依赖于其他软件包）。RPM 允许你添加、删除、构建、查询和验证软件包。RPM 的文档非常广泛，主要资源列在第 28 页 *RPM 资源*中。

在本节中，我们将讨论几个 RPM 命令，我们将在本书的不同部分重新提及这些命令。

### 使用 RPM 验证软件包

RPM 允许你验证已安装的软件包和文件。它可以检查每个文件的大小 (`S`)、权限或模式 (`M`)、MD5 哈希值 (`5`—有关 MD5 的更多信息，请参阅第 44 页的哈希函数和数字签名)、主次版本号 (`D`)、符号链接内容 (`L`)、所有者 (`U`)、组 (`G`) 和修改时间 (`T`)。它还会告诉你文件是否为配置文件 (`c`)。它将这些检查与包含在 RPM 数据库（`/var/lib/rpm`中一组文件）中最初安装的配置进行对比。可以使用`-v`选项验证文件和软件包。例如，我们可以使用以下命令验证`/etc/exports`以及包含`/etc/exports`的软件包中的所有文件：

```
$ rpm -Vf /etc/exports
S.5....Tc /etc/exports
S.5....Tc /etc/hosts.allow
S.5....Tc /etc/hosts.deny
S.5....Tc /etc/printcap
S.5....Tc /etc/services
S.5....Tc /etc/exports
$
```

请注意，`-e`选项指定参数是一个文件。输出结果反映了验证失败的事实。每个文件的大小、MD5 哈希值和修改时间都与原始值不同。这无关紧要，因为这些文件都是配置文件（注意“`c`”），且很可能发生变化。

如果验证通过，则没有输出。例如：

```
# rpm -Vf /sbin/iconfig
#
```

这表明`/sbin/iconfig`以及包含`/sbin/iconfig`的软件包中的所有其他文件自安装以来均未更改。

您也可以将已安装的软件包与 CD 进行验证。例如，将 Red Hat 发行版 CD 插入您的光盘驱动器并执行以下操作：

```
# mount /mnt/cdrom
# rpm -Vp /mnt/cdrom/RedHat/RPMS/bash-1.14.7-13.i386.rpm
#
```

这将验证您系统中加载的软件包`bash-1.14.7-13`是否与 CD 上找到的软件包一致。

此功能可以帮助您通过验证软件包的完整性来提高安全性。有关更多详细信息，请参阅第 28 页“RPM 资源”章节中的 [Maximum RPM](http://www.redhat.com/knowledgebase/zhtml/linuxdocs.html)。

### 使用 RPM 检查 PGP 签名

一些 RPM 软件包将包含 PGP 签名（PGP 在第 45 页的“PGP 概述”中有介绍）。如果您获取了这样的 RPM，您可以使用`-k`标志验证签名。例如，我们验证一个 Secure Shell (SSH) RPM 的签名。

```
# rpm -K ssh-1_2_26-ius_i386.rpm
ssh-1_2_26-ius_i386.rpm: size pgp md5 OK
#
```

请注意，MD5 哈希值也会被验证。如果我们希望获得更详细的输出，可以添加`-v`选项，如下所示：
