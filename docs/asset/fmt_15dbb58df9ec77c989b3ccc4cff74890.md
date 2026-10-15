
其他操作有不同的语法。例如，`copy`操作允许你设置文件属性，如源和目的路径、所有者、组和权限。

```
copy:
  /usr/repo/files/group dest=/etc/group owner=root group=sys mode=644
```

不同的操作可以进一步细分为`editfiles`，用于对文件进行原地编辑。这种`editfiles`的用法注释掉了文件中的 finger 服务。

```
editfiles:
  CommentLinesMatching = "*finger*"
```

## 使用类

每个操作都可以进一步细分为类（classes），这些类是由 cfengine 设置的布尔变量（真或假）。类代表 cfengine 的各种状态，包括运行它的主机和当前时间。类甚至可以在完成操作后动态创建。操作仅在它们列出的类被定义时才调用，这使得根据主机名、日期甚至上一个操作的完成情况做出不同的更改变得简单。

cfengine 提供了一组默认类来表示主机名和时间等内容。这些类包括：

| Class | Description |
| :--- | :--- |
| any | 此类始终被定义，列在其下的任何操作将始终执行。 |
| hostname | 此类以当前运行 cfengine 的主机名命名。 |
| platform | 此类以运行 cfengine 的平台名命名（如 sun4、linux）。 |
| YrXXXX | 当前年份（例如 Yr2002）。 |
| Month | 以当前月份命名 |
| Day | 以星期几命名 |
| DayXX | 月份中的日期（例如 Day26） |
| HrXX | 24 小时制中的小时（例如 Hr20） |
| MinXX | cfengine 启动时的分钟 |
| MinXX_XX | cfengine 启动时小时内的 5 分钟间隔（例如，12:07 将产生一个名为 Min12_5 的类） |

定义自己的类非常简单；只需在`classes`操作下定义每个类，就像在`control`操作中定义变量一样。以下是定义如下 Web 服务器机器类的方法：

- classes:
  webservers = ( grumpy dopey sneezezy doc )

要将操作限制到特定类，只需在类名前前面加上两个冒号。列表 12.1 显示了一个典型的 cfengine 配置文件，它将 `/etc/group` 复制到所有服务器并处理 httpd。当 Web 服务器上的 httpd.conf 更新时，Apache 会重启。它还注释了 `/etc/inetd.conf` 中以 "finger" 开头的行。

### 列表 12.1 一个简单的 cfengine 配置文件

```
# simple cfengine.conf

# 定义类

classes:

  webservers = ( grumpy dopey sneezezy doc )

# 定义我们的操作顺序

control:

  actionsequence = ( copy editfiles shellcommands )

# 复制文件

copy:

  any:

    # 将 /etc/group 复制到所有服务器

    /usr/repo/files/group dest=/etc/group o=root group=sys mode=644

  webservers:

    # 向 Web 服务器复制 Apache 配置

    /usr/repo/files/httpd.conf dest=/usr/local/apache/conf/httpd.conf \
    o=root group=root mode=644 define=restart_httpd

# 编辑配置文件

editfiles:

  CommentLinesMatching = "^finger"
```

# UNIX 系统管理入门教程

### 列表 12.1 续

```
# 运行命令

shellcommands:

restart_httpd:

    /usr/local/apache/bin/apachectl restart
```

你可以通过使用复合类（compound classes）为配置添加更多灵活性。复合类支持逻辑与（AND）和或（OR）类，因此你可以根据多个类的值来执行操作，而不仅仅是一个类。逻辑与用 "&" 表示，而逻辑或用 "|" 表示。逻辑与不是通过在类名前面加 "1" 来表示的。使用列表 12.2 中的 `cfengine.conf` 在周一将 Apache 配置文件复制到 Web 服务器，你可以将配置更改为如下所示：

```
copy:
    webservers.Monday:
        # 加入 Web 服务器的 Apache 配置
        /usr/repo/files/httpd.conf dest=/usr/local/apache/httpd.conf owner group=root mode=644 define=restart_httpd
```

此时应该显而易见 cfengine 是有多强大了。你可以复制文件、特定的行、重启进程等任何你想要的操作——这一切通过一个配置文件即可。

# 自动化临时空间管理

Unix 提供了几个默认的临时文件存储位置，最常见的是 `/tmp` 和 `/var/tmp`。你可以提供其他临时存储位置。用户、应用程序和操作系统都会使用这些空间，因此保持临时存储位置整洁至关重要。后续章节中讨论的工具使定期清理成为系统维护的简单部分。

# 使用 find 进行临时空间管理

清理临时存储目录的一种历史悠方法是使用 `find` 命令。`find` 是一个极其复杂的命令，许多初学者（甚至是一些高级用户）都会被它的语法所困扰。这里提供的示例仅使用了它的少数几个选项。

大多数站点选择通过删除在指定时间内（例如两周）未被修改的文件来管理临时存储。有时时间范围还不够——如果某些服务器运行着长时间进程，并在 `/tmp` 中存储持久性信息怎么办？幸运的是，`find` 可以达到你所需的精确度。一种可行的方法是指示 `find` 只删除用户拥有的文件，而不是管理员账户的文件。例如，如果大多数服务器以 root 身份运行，你可以告诉 `find` 忽略这些文件。以下 `find` 命令将删除超过两周且不属于 root 的文件：

```
# find /tmp /var/tmp -mtime +14 ! -user root rm -f {} \
```
