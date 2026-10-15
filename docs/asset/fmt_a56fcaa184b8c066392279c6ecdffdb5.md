
创建此文件后，你必须使用以下命令重启 xinetd：

```
$ sudo /etc/init.d/xinetd restart
```

## 在 Firefox 中处理 svg URL

在 Firefox 中尝试访问以 svg 开头的 URL 将显示一个对话框，提示“Firefox 不知道如何处理此地址”。如果你能够在 Firefox 中处理这些 URL，你需要创建一个小型脚本来调用你喜欢的 Subversion 客户端。例如，我使用以下脚本：

```
#!/bin/bash

/usr/bin/svnner "$1"
```

在将此保存到文件中并赋予执行权限后，我通过以下方式修改了 Firefox：

- 在 Firefox 地址栏中输入 `config`，并按回键。
- 在偏好窗口中右键点击并选择“新建字符串”，
- 输入 `network.protocol-handler.app.svg` 作为字符串名称，
- 将脚本的完整路径作为字符串的值。

## 从 Subversion 存储库检出文件

现在你已经配置了一个（或两个）Subversion 服务器，你可以从任何可以到达服务器的机器访问示例存储库。获取 hello 项目的示例检出命令如下：

- `svn file:///var/svn/hello`：这是获取 hello 项目的标准命令。你只能从 Subversion 存储库所在的机器使用它。
- `svn http://192.168.6.90/svn/hello`：此命令使用 HTTP 协议获取 hello 项目，只有在 Subversion 存储库所在的主机上运行了 Web 服务器时，它才能工作，参见“配置 Apache2 以支持 Subversion”部分。
- `svn sv://192.168.6.90/svn/hello`：此命令使用 SVN 协议获取 hello 项目，只有在 Subversion 存储库所在的主机上运行了 Subversion 服务器时，它才能工作，参见“配置 svner 服务器”部分。

执行这些命令将在你的当前目录下创建一个名为 `hello` 的目录，并在该目录中填充 `hello.c` 文件。恭喜——你正在使用 Subversion！

# 在 Ubuntu 和 Kubuntu 上进行软件开发

## 向 Subversion 仓库提交更改

一旦你检出 Subversion 仓库的文件并对其进行了修改，你就会想要将它们提交回最初所在的仓库——这为你的源代码的最新、最全版本提供了一个唯一的真实位置，而且能够对其进行更改正是源代码控制的根本意义所在。

Subversion 让提交修改后的文件变得非常简单，因为它会自动跟踪版本信息以及检出文件最初所在的仓库。如果你对任何从 Subversion 检出的目录进行详细列出 `-al`，你将看到一个名为 `svn` 的目录，它就存储了这些信息。

由于 Subversion 为你维护了这些信息，要将文件提交回 Subversion，你所做的只是使用 `svn ci`（提交）命令。下面的示例展示了提交 `hello` 文件的新、改进版本的过程，并显示了 svn 命令提交操作的输出：

```
$ svn ci hello.c -m "Added commit"

Sending hello.c

Transmitting file data .

Committed revision 7.
```
