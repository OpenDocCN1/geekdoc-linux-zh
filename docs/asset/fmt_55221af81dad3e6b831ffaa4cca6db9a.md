
# 修改 AIDE 报告的输出

现在，AIDE 报告将运行并将 STDOUT 重定向到名为 `/var/log/aide/aidereport-<date>.txt` 的文件

例如，对于 2014 年 3 月 12 日的报告，文件名将是 `/var/log/aide/aidereport-03122014.txt`

使用像这样的重定向配置后，当 AIDE 通过其正常的 cron 任务运行时，你将不再收到电子邮件。相反，只有当 AIDE cron 任务发生错误时，你才会收到电子邮件。由于你不再接收邮件，你可能会忍不住忽略监控职责并让所有 AIDE 报告堆积。然而，你仍然应该通过查看 AIDE 报告中的异常情况进行监控，并根据情况进行清理。

# 获取更详细的输出

AIDE 报告可以配置额外的详细程度。当你排查规则匹配问题时，为 AIDE 添加详细信息非常有价值。例如，当你设置 `verbose-configuration` 选项时，你将能够看到 AIDE 如何构建要检查的文件列表。如果你看到意外的结果，或者文件由于神秘原因被包含或排除，在配置中添加此项或将其作为命令行选项添加将会有帮助。

添加详细信息的配置选项如下：
`verbose=<N>`

在这种情况下，`<N>` 是一个正整数，最大值为 255。在实践中，超过 200 的数字会为大多数检查提供额外的调试输出。因此，要添加最大的详细级别，你将使用此配置设置：
`verbose=255`

使用此配置，你将在 AIDE 运行期间看到一些额外的输出：

```
Handling / with s "/bin" with node "/"

Handling / with s "/sbin" with node "/"

Handling / with s "/etc" with node "/"

Handling / with s "/lib" with node "/"

Handling /usr with s "/usr/lib" with node "/usr"

tree: "/"

2    ^/bin

3    ^/sbin

4    ^/etc

5    ^/lib

tree: "/usr"

6    ^/usr/lib
```

`AIDE, version 0.15.1 AIDE database.` 看起来不错！

# 第 14 章 文件系统完整性

输出要详细得多（正如你预期的那样），并包含了 AIDE 程序内部调用的函数，以及 AIDE 在检查文件时正在检查文件的详细信息。当你试图排查 AIDE 配置问题时，使用这种输出可能是无价之宝。

# 在 AIDE 中定义宏

宏在 AIDE 中用于定义常用对象，以及在整个 AIDE 配置文件中作为变量的对象。你可能会使用 AIDE 宏来定义在配置内部使用的顶级目录。然后，你将在选择行中使用此宏，它将作为变量在 във选择行中被替换。你还可以使用宏根据某些标准来设置变量。宏随后可以在 AIDE 配置文件中的控制结构（代码的决策块）中使用，以根据决策控制结构来更改 AIDE 的配置。

宏使用以下语法定义：

```
@@define <definition>
```

宏也可以使用以下语法取消定义：

```
@@undef <macro>
```

宏在 AIDE 配置中通过以下语法使用：

```
@@(<macro>)
```

以简单方式使用宏的一个示例是创建一个宏：

```
@@define BASEDIR /usr/src
```

此宏稍后可以在可以在配置中使用：

```
$(BASEDIR)/
```

如果你在不同主机之间有不同的目录结构，并且你希望在它们之间只使用一个 AIDE 配置文件，这可能对你有帮助。以下是这些这些用途的示例。第一个示例检查名为 `SOURCE` 的宏是否已定义，如果没有，则定义它：

```
@@ifndef SOURCE

@@define SOURCE /usr/src

@@endif
```

第二个示例查看运行 AIDE 的计算机的主机名，并根据检查结果设置宏。这是第二个示例：

```
@@ifhost cwa

@@define LOCALBINDIR /usr/local/sbin

@@endif
```

最后，这是一个使用 else 语句的示例：

```
@@ifhost cwa

@@define LOCALBINDIR /usr/local/sbin

@@else

@@define LOCALBINDIR /usr/local/sbin

@@endif
```

无论使用哪种控制结构，都必须使用此语句关闭：

```
@@endif
