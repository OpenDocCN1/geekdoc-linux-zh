

![](img/8684900d708748f86bb043faa5589f9e_60_0.png)

既然你已经熟悉了系统中运行的内容，那么你也可以开始使用 OpenStack 命令行客户端来启动实例、查看实例状态等。首先，你需要通过 source devstack 目录中的 openrc 文件来加载凭证。以下是几个简单的入门命令：

```
$ source ~/devstack/openrc
$ openstack flavor list
$ openstack server list --all-projects
```

你将在后续章节中了解更多关于 OpenStack Client 命令的内容，并在附录 E“OpenStack Client (OSC)”中找到基本参考。

## DevStack 选项

本章的前一节介绍了如何在没有任何自定义的情况下启动 DevStack。然而，为了测试 OpenStack 开发版本的各个方面，建议进行自定义设置。

### DevStack “稳定版”

DevStack 中一个鲜为人知的功能是可以使用 DevStack 脚本启动 OpenStack 的稳定版本。开发人员和 OpenStack 持续集成堆栈大量使用此功能来测试升级。不过，它也可以帮助新手体验特定已发布的 OpenStack 版本，而不仅仅是开发版本。如果你在运行 master 分支的 DevStack 版本时遇到问题，使用这个稳定版本来入门 OpenStack 也很有价值。

> **注意**
>
> 尽管这会安装 OpenStack 的稳定版本，但这仍然不是在生产环境中运行 OpenStack 的可维护或推荐方式。你应该继续使用稍后可以重新安装的虚拟机或备用系统，并学习适当的分离和高可用性流程以维护生产系统。

使用 DevStack 运行 OpenStack 稳定版本的步骤是之前提到的三个步骤的略微修改版，增加了一步切换到克隆的 git 仓库中受支持的稳定分支之一：

```
$ git clone git://git.openstack.org/openstack-dev/devstack.git
$ cd devstack
$ git checkout stable/mitaka
$ ./stack.sh
```

> **提示**
>
> 想要列出 DevStack 中可用的稳定分支以供选择吗？在 devstack 目录下，输入：
>
> `git branch -a`
>
> OpenStack 版本是按字母顺序排列的，因此分支列表中的最后一项将是最新的稳定版本。

与运行标准 DevStack 一样，这需要一些时间来下载依赖项并设置环境。它不会从开发版本拉取，而是从请求的稳定环境拉取。

本章前面演示的以用户和管理员身份登录的步骤也可以在这个稳定版本上完成，但你会拥有一个已发布的版本，它更像是在你的发行版中附带的版本。

## 自定义 DevStack

你可以进行许多自定义设置，以调整你的 DevStack 环境，实现从预置密码和网络到启用附加服务等各种功能。

> **提示**
>
> 如果你想要进行自定义设置，建议不要使用 DevStack 的某个稳定分支。开发版本一直在添加新选项，并且处于积极维护和测试中，而稳定版本更新的可能性较小。

更改是在主 devstack 目录中的 `local.conf` 文件中进行的。你可以在 `samples/local.conf` 中找到一个示例配置文件。

至少，建议编写一个 `local.conf` 以匹配你的环境并使脚本非交互式运行。这将包括为 admin 用户以及数据库、队列服务器等服务设置默认密码以及网络配置。

通过阅读你所运行的 DevStack 版本的文档来了解更多关于最小配置的信息，该文档存储在源代码 `doc/source` 目录中的 `configuration.rst` 中。最新的开发版本在线可用，地址为：[http://docs.openstack.org/developer/devstack/configuration.html#minimal-configuration](http://docs.openstack.org/developer/devstack/configuration.html#minimal-configuration)。

除了这些基本的环境变量，还有几个值得注意的变量：

- 更改 DevStack 目录：

  ```
  DEST=/opt/stack (默认值，更改为你希望使用的路径)
  ```

- 启用日志记录：

  ```
  LOGFILE=$DEST/logs/stack.sh.log
  ```

你还可以调整日志存储的天数（默认 7 天）以及与日志去向相关的设置（它们的专用日志或统一的 syslog）。

启用其他服务是在自定义 DevStack 时你可以做的更强大的事情之一。通过在此开发环境中启用其他服务，你可以测试最新功能，或者部署一个组件更接近你未来实际部署样式的 DevStack。例如，如果你想专注于存储，你可能希望启用 Swift，即 OpenStack 的对象存储组件。启用附加服务通常是通过在 `local.conf` 文件中定义变量来实现的。DevStack 开发版本中支持的服务会随着新服务加入 OpenStack 生态系统而定期变化。除了前面提到的随附文档外，要了解可用服务以及默认服务在 DevStack 中如何工作以及被调用，你可以浏览 DevStack 源代码中的 `lib/` 目录下的文件。这些库包含大量文档，其中包含注释以及部署它们所需的导出和函数。

你可以设置一个使用多主机的 DevStack 安装，就像我们稍后以更可维护的方式安装 OpenStack 时那样。然而，这种配置支持较差，DevStack 开发者警告说它仅在非常基本的配置下经过测试。

如前所述，你可以阅读注释详尽的 `stack.sh` 脚本，了解更多可以通过环境变量或 `local.conf` 脚本进行的自定义设置。

## 总结

我们现在已经介绍了 DevStack 的一些最基本用途，并让你开始在一个真实的、非生产环境的 OpenStack 安装中运行。通过这些，你能够开始熟悉前台守护进程的界面和基本导航，从而窥见几个服务的内部结构。然后，我们回顾了一些扩展 DevStack 以运行 OpenStack 稳定版本并启用某些默认未启用的其他 OpenStack 服务的方法。

# 3 网络

> *如果这颗星球上有魔法，那就包含在水中。*
>
> Loren Eiseley

在我们深入部署场景之前，停下来讨论一下网络是很重要的。网络是配置 OpenStack 时主要考虑的因素。它将影响你所做的硬件和环境选择，并自然地在这本书中为你和部署场景做出的选择中扮演重要角色。

OpenStack 中的网络也是一个复杂的主题，同样会让试图部署 OpenStack 的系统管理员和网络管理员陷入困境。此外，你所在环境（例如数据中心）中的物理网络和设备将决定你可以使用 OpenStack 支持的网络工具做什么。

## 关键概念

关于 OpenStack 网络，你应该知道的第 一件事是没有标准的部署方案。组织的需求、它们必须工作的环境以及使用的硬件会有很大的不同。本章概述的概念是泛化的，并非所有部署都遵循相同的规则。这里的目的是让你在对 OpenStack 进行自部署时可能遇到的情况有一个初步了解，从而有一个理解其工作原理的起点。

## 操作平面

使用通用网络中找到的相同术语来考虑 OpenStack 环境中整个流量流是有用的。具体来说，网络工程将流量流概念化为发生在管理平面、控制平面或数据平面之一。OpenStack 有非常类似的网络类型划分，但这些网络有时会被合并。为了简单起见，我们的部署场景将使用单个私有网络用于控制、管理和数据流量，但我们仍然应该解释每个平面。

### 管理平面

管理员需要一种方式来维护、更新和查询他们的服务器和网络元素，这通常是通过管理平面完成的。

