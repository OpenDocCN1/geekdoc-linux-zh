

## 安装 AIDE

AIDE 是一款文件系统完整性检查工具，提供了此类程序所具备的众多功能。有关 AIDE 的更多信息（包括下载链接）请访问 [http://www.cs.tu.tz.fi/~rammer/aide.html](http://www.cs.tu.tz.fi/~rammer/aide.html) 和 [http://sourceforge.net/projects/aide](http://sourceforge.net/projects/aide)。

下载完成后，AIDE 需要编译。不过，在尝试编译 AIDE 之前，您可能还需要安装一些前置依赖项。如果是这种情况，AIDE 的 configure 脚本会告知您这些前置依赖项，您需要在继续编译 AIDE 之前先下载并编译这些依赖项。一个常见的前置依赖项是 mhash 库。您可以从 [http://sourceforge.net/projects/mhash/](http://sourceforge.net/projects/mhash/) 下载 mhash 库。

mhash 库应以静态方式编译，以便与 AIDE 配合使用。请按照解包和编译软件包的标准步骤操作：

```
tar -zxvf mhash-<NNNN>.tar.gz
cd mhash-<NNNN>
```

我建议为 configure 脚本使用以下编译选项：

```
./configure --prefix=/usr --enable-static=yes
```

配置完 mhash 后，使用以下命令进行编译和安装：

```
make
make install
```

编译 AIDE 与其他软件的编译过程类似，例如在 Linux 中操作如下：

```
tar -zxvf aide-<NNNN>.tar.gz
cd aide-<NNNN>
./configure
make
make install
```

## 配置 AIDE

与许多其他 Linux 应用程序一样，AIDE 通过配置文件来运行。该配置文件基于文本，包含程序运行时用于确定其行为特征的信息。首次运行 AIDE 时，您将创建并初始化一个数据库，用于后续的文件系统完整性检查。然后手动检查该数据库以确保其合理性，并运行更新流程，从此以后用于查找文件系统中发生的变化。

### 创建 AIDE 配置文件

安装 AIDE 后，您想要做的第一件事就是创建一个配置文件。与 Linux 中的大多数其他软件不同，AIDE 不包含默认的配置文件，您无法基于它构建自定义版本。在 `<AIDE-source>/doc/` 目录中有一个示例配置文件，但其中明确说明不应将其用作系统范围的配置文件。因此，您必须自己创建一个。别担心，我会帮助您。

AIDE 配置文件通常名为 aide.conf，位于 /etc/ 目录下。AIDE 配置文件中的注释以井号（#）开头。AIDE 配置文件中的行分为三类：配置行、宏行和选择行。AIDE 配置文件的核心是选择行，用于确定监控文件系统中的哪些对象。配置行在确定 AIDE 如何运行方面也很重要，而宏行在创建高级配置时也很重要。AIDE 使用一系列 `parameter=value` 指令来指示对给定对象执行何种类型的检查。表 12.1 列出了这些指令。

#### 表 12.1：AIDE 配置指令

| 指令 | 描述 |
| :--- | :--- |
| p | 权限 |
| i | inode |
| n | 链接数 |
| u | 用户 |
| g | 组 |
| s | 大小 |
| b | 块数 |
| m | Mtime |
| a | Atime |
| c | Ctime |
| S | 检查增长的大小 |
| md5 | md5 校验和 |
| sha1 | sha1 校验和 |
| rmd160 | rmd160 校验和 |
| tiger | tiger 校验和 |
| R | p+i+n+u+g+s+m+c+md5 |
| L | p+i+n+u+g |
| E | 空组 |
| > | 增长日志文件 p+u+g+i+n+S |
| haval | haval 校验和 |
| gost | gost 校验和 |
| crc32 | crc32 校验和 |

AIDE 还允许管理员创建包含默认组的自定义组。这样做可以节省时间并提高配置文件的可读性。您可以使用自定义组来组合其他常用检查组。例如，创建一个名为 MyGroup 的组，包含常用类型的检查，只需这样简单操作：

```
MyGroup p+i+n+u+md5
```

无论这些分组是默认的还是自定义的，都用于确定将在给定选择上执行的检查类型。您还使用配置文件中的选择行来配置要检查的文件和目录。选择行由要检查的对象和要执行的检查类型组成。对象可以是文件、目录、正则表达式，或者更常见的是文件与某些正则表达式语法的组合。我将在后面的章节中简要介绍正则表达式，但现在我将展示选择过程的简单示例。

以下选择行将检查 /etc 目录中的所有内容，具体查看链接数、拥有特定文件的用户、拥有特定文件的组以及文件的大小：

```
/etc n+u+g+s
```

这些属性之一的意外变更可能表明有人篡改了系统。下一个示例使用名为 MyGroup 的自定义组作为 /bin 目录中文件的检查项：

```
/bin MyGroup
```

可以使用感叹号（!）忽略或跳过某些对象，如下例所示，这将使 AIDE 忽略 /var/log 中的所有内容：

```
!/var/log/.*
```

忽略经常变化的对象可以大幅减少 AIDE 报告中出现的无关行数。但是，您应谨慎行事，以免忽略过多；否则，您可能错过重要的文件系统变更。

配置文件中的规则行使用正则表达式来实现强大的匹配功能。如果您不熟悉正则表达式背后的奥秘，请不要担心；在这里我会尽量简单易懂。

在 AIDE 中匹配文件的一个主要顾虑是，您不能给攻击者留下绕过文件完整性检查器的空间。如果您没有完全限定文件名来指定，这种情况就可能发生。例如，如果您想跳过检查 /var/log/ 目录中的一个文件，因为它会变化，您可能会使用这种（看似正确的）语法：

```
!/var/log/maillog
```

然而，由于发生的正则表达式匹配，攻击者可以创建这样一个文件：

```
/var/log/maillog.crack
```

由于您已经排除了 /var/log/maillog，AIDE 将不会检查任何以 /var/log/maillog 开头的文件。为了解决这个问题，您在文件末尾添加一个美元符号（$）。在正则表达式语法中，$ 表示行尾。因此，通过更改要排除的文件的语法并添加 $，您使用了针对该文件系统检查最精确的匹配：

```
!/var/log/maillog$
```

默认情况下，AIDE 将在 /usr/local/etc/ 中创建一个基于文件的数据库，名为 aide.db.new。然后手动将该文件移动到 /usr/local/etc/aide.db 以供未来检查使用。因此，在配置文件的背景下，确实没有真正必要改变这种行为；但是，您当然可以使用配置选项更改该文件的路径和名称：

```
database=file:<filename>
database_out=file:<filename>
```

AIDE 还可以使用 SQL 数据库服务器（如 PostgreSQL）来存储数据库内容，尽管该配置超出了本书的范围。

### AIDE 配置文件示例

至少，您需要告诉 AIDE 要检查文件系统的哪些部分以及用于这些检查的规则。您还可以向配置中添加许多其他内容来改变 AIDE 的执行方式。为了本节的目的，我将展示一个非常基本的配置文件，并附带说明您应根据 Linux 安装的需要对其进行补充。

打开文件 `/usr/local/etc/aide.conf`。如果该文件不存在，请创建它。在文件中放置以下行：

- /bin R
- /sbin R
- /etc R+a
- /lib R
- /usr/lib R

### 初始化 AIDE 数据库

在手边拥有一个快速且基本的配置文件后，是时候初始化 AIDE 数据库了。这个过程所需时间各不相同，取决于您要检查的文件数量以及计算机可用的资源量。初始化 AIDE 数据库很简单，只需运行以下命令：

```
/usr/local/bin/aide --init
```

AIDE 现在将根据您在配置文件中选择的标准初始化数据库。完成后，您将看到类似此消息：

```
AIDE, version 0.10

AIDE database initialized.
```

下一步是将新创建的数据库重命名（移动）为 `aide.db`，使其成为默认或主数据库：

```
mv /usr/local/etc/aide.db.new /usr/local/etc/aide.db
```

现在，您应该能够运行数据库检查以验证一切正常：

```
/usr/local/bin/aide --check
```

如果一切顺利，您将看到如下类似的输出：

```
AIDE, version 0.10

All files match AIDE database. Looks okay!
```

初始化 AIDE 数据库后，您应立即将数据库复制到磁盘，最好是 CD-R 之类的只读介质，或者安全地将其复制到另一台计算机上。如果您将 AIDE 数据库留在计算机上，攻击者可能能够简单地修改 AIDE 数据库，在用自己的文件替换系统文件后掩盖她的踪迹！从此时起，每次更新 AIDE 数据库时，您都应始终将生成的数据库文件复制到安全介质上。

