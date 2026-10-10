
所有对 OpenStack 的更改在合并之前必须通过持续集成系统中的所有测试，因此由 DevStack 拉取的开发者代码已经在默认的 DevStack 环境中自动测试过了。OpenStack 生态系统中的几家公司也将 DevStack 用作其质量保证系统的一部分。

## DevStack 要求

要开始使用 DevStack，你需要一台可用至少 4GB 内存的虚拟机（VM）或备用系统，但请注意，DevStack 在 6-8GB 内存下运行效果更佳。为了获得最佳性能，你还需要使用支持硬件虚拟化的 64 位 CPU。

你有多种基础操作系统选择，因为 Ubuntu LTS、Fedora 和 RHEL/CentOS 目前均维持对 DevStack 的支持，而其他几种发行版则对特定版本提供半维护状态的支持。

最后，如果你使用虚拟机并希望使用本章后续描述基于 Web 的 Horizon 仪表盘，你需要安装所选基础操作系统的桌面版本，或者从另一台机器提供对该机器 `80` 端口的访问权限。这样你就可以在 `localhost` 上使用 web 浏览器，或者安装使用桥接接口的服务器版本，以便从外部访问服务器。如果你使用的是物理硬件，请确保该系统可以通过网络访问。

## 部署 DevStack

既然你已经具备了运行 DevStack 所需的资源，就需要做一些配置决定了。

DevStack 设计为开箱即用，无需更改配置，只需执行一系列简单命令，其中最后一条命令会花费一些时间：

```bash
$ sudo apt-get install git
$ git clone https://git.openstack.org/openstack-dev/devstack.git
$ cd devstack
$ . /stack.sh
```

前几步会要求你输入每个组件的一串密码。你需要记录这些密码的输入内容。获取密码后，它会花费一些时间来修改你的软件源和网络，然后下载 DevStack 中使用的 OpenStack 组件的最新开发版本及其依赖项。脚本还会在开始阶段的某些点暂停，询问你服务密码（有关如何使用包含这些变量的 `local.conf` 文件的提示，请参阅本章稍后的“自定义 DevStack”部分）。

DevStack 项目提供了一份带注释的 `stack.sh` 脚本版本，供你在默认安装进行时查阅；你可以在 `devstack` 目录中本地查看，或在线访问 `http://docs.openstack.org/developer/devstack/stack.sh.html`。

## 常见故障

如果权限不正确，你在运行 DevStack 时将会遇到问题。以下是一些建议：

- 不要在使用上述列出的任何命令时使用 `root` 或 `sudo`。
- 虽然你不应该以 `root` 或 `sudo` 身份运行命令，但你用于运行 `stack.sh` 的用户必须具有 `sudo` 权限，最好是无密码的。
- 在运行 `stack.sh` 时，确认 `devstack/` 目录由你试图用来运行它的用户所有。
- 如果你希望创建一个专门用于运行 DevStack 的 “stack” 用户，你可以使用随 DevStack 提供的 `tools/create-stack-user.sh` 脚本。此脚本需要从具有 `sudo` 权限的账户使用 `sudo` 运行。

网络是许多故障的根本原因。以下是一些最常见的问题：

- 你的本地网络与 DevStack 内部网络（`10.0.0.1/24`）的默认设置冲突。
- 虚拟机或物理系统无法访问互联网。运行 `stack.sh` 需要互联网访问。这可能表现为从域名解析错误到操作系统存储库超时的各种问题。

有时 DevStack 会损坏。如前所述，DevStack 拉取的是 OpenStack 的开发版本。尽管在代码合并之前进行了大量的测试，但有时 DevStack 的当前日期状态不允许进行部署。如果你 struggles 运行纯 DevStack，请参阅本章稍后关于 DevStack "stable" 的详细信息。

一旦安装成功完成，在返回你的命令提示符之前，它应以类似以下内容结束：

```
=========================
DevStack Components Timed
=========================

run_process - 46 secs
apt-get-update - 12 secs
pip_install - 377 secs
restart_apache_server - 9 secs
wait_for_service - 13 secs
git_timed - 248 secs
apt-get - 250 secs

This is your host IP address: 192.168.122.216
This is your host IPv6 address: ::1
Horizon is now available at http://192.168.122.216/dashboard
Keystone is serving at http://192.168.122.216:5000/
The default users are: admin and demo
The password is: 13245
2016-04-20 21:51:40.175 | stack.sh completed in 1486 seconds.
```

第一个链接是 Horizon，它是 OpenStack 的基于 web 的仪表盘。这是一个非常有价值的起点，因为它提供了部署的图形概览，并支持用户和管理员登录。

第二个链接指向 Keystone 的 API 端点，任何需要通过 API 操纵 OpenStack 的服务（如 Nova、compute 和命令行客户端）都需要与其进行身份验证。这通常在执行针对 DevStack 的命令时需要放入环境变量或配置文件中。

> **警告**
>
> 你重启了吗？由于 DevStack 并非设计为持久安装，当重启系统时，它不会自动恢复你的部署。
>
> 你需要再次运行 `./. . . . .stack.sh` 和 `.stack.sh` 以创建新的 DevStack 环境。不幸的是，这将重新开始全新安装，你的任何实例、卷或其他内容都不会保留。

## 仪表盘：作为用户登录

我们将首先介绍 Horizon 界面。导航到之前给出的 URL，首先你可以作为普通用户登录。默认情况下，你会拥有一个名为 “demo” 的用户用于此目的，其密码为安装时指定的密码。登录后，你将看到面向用户的仪表盘视图（见图 2.1）。

![](img/8684900d708748f86bb043faa5589f9e_54_0.png)

图 2.1 Horizon 仪表盘（用户视图）

> **提示**
>
> 加载 Horizon 登录界面有困难？有时首次启动时速度较慢，因此请等待几秒钟后重试。

作为用户，你可以探索可用的选项，但作为第一个任务，你可以尝试启动一个实例。

首先，你需要设置将传递给任何你启动的实例的用户凭据。为此，你需要选择计算部分左侧菜单中的访问与安全。你看到的第一个屏幕是安全组，它控制实例上可访问的端口，包括入站和出站。你需要选择如图 2.2 所示的密钥对选项卡。在此屏幕上，你可以上传系统中已有的现有公共 SSH 密钥，或者创建密钥对。如果你选择通过界面创建密钥对，它将下载相关的 `.pem` 文件，然后你将在实例启动后使用该文件通过 SSH 客户端登录实例。

下一步是通过 Horizon 仪表盘创建你的第一个实例。你可以通过选择左侧菜单中的实例并点击启动实例按钮来执行此操作。这将弹出如图 2.3 所示的对话框，引导你输入第一个实例所需的所有信息。

![](img/8684900d708748f86bb043faa5589f9e_55_0.png)

![](img/8684900d708748f86bb043faa5589f9e_55_1.png)

在“详细信息”界面中，对话框选项包括以下内容：

- **实例名称**：这将是在 OpenStack 中引用该实例的名称。之后可以在 Horizon 界面中使用此名称来引用实例，但请注意，这些名称并不唯一，因此如果你之后希望访问该实例，最好通过 UUID 来引用它。
  
  在此演示中，你可以使用任何你想要的名称。

- **可用区**：由于这是一个 DevStack 安装，唯一可用的可用区（AZ）是默认的—nova。如果你使用的是公共 OpenStack 云或分布式云，你将拥有更多选项。

- **数量**：定义你希望启动多少台此类实例。
  
  目前，我们只需要一台。

填写完这些部分后，点击“下一步”进入“源”界面。

- **实例启动源**：源是灵活的，允许你使用已上传到 OpenStack 的预定义镜像、现有卷或快照，或者上传你自己的镜像。根据你选择的内容，对话框会发生变化，以进一步描述启动源。
  
  1. 在“选择启动源”下拉菜单中，应选择“镜像”。如果没有选择，请进行选中。
  2. DevStack 附带了一个非常基础的关注于云环境的 Linux 镜像，称为 CirrOS。点击对话框中“可用”部分最右侧的加号，将其移动到“已分配”区域。

再次点击“下一步”以选择你的口味（Flavor）。Flavor 描述了将分配给实例的资源，包括 CPU 数量、内存量和磁盘空间。与“源”界面一样，点击你想要选择的 flavor 右侧的加号。由于我在使用 DevStack 时通常面临资源限制，我通常会选择 `m1.nano`。

既然你已经设置了 SSH 密钥，现在你需要点击左侧菜单中的“密钥对”。与之前的两个界面一样，你会看到之前创建的密钥，并可以点击加号将其添加到“已分配”中。完成这一步后，你现在终于可以点击“启动实例”按钮了。

实例的构建状态将在 Horizon 中显示。使用 CirrOS 时启动应该很快，在看到分配本地 IP 后不久，你就可以使用你创建或已使用的 SSH 密钥通过 `ssh` 登录。使用默认网络配置，这是一个仅限本地的 IP。你需要从 DevStack 主机进行 `ssh` 登录，例如：

```bash
$ ssh -i .sh/elizabeth.pem cirr0s@10.0.0.2
The authenticity of host '10.0.0.2 (10.0.0.2)' can't be established.
RSA key fingerprint is 4e5:173:48:0f55:e5:20:89:11:7:e3:83:d447:5v:66.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '10.0.0.2' (RSA) to the list of known hosts.
$
```

单个 `$` 符号表示你已登录到 CirrOS 镜像。你可以使用以下命令确认：

```bash
$ cat /etc/cirros/version
0.3.4
```

如果你之前没有设置 SSH 密钥或在使用密钥时遇到问题，你仍然可以使用密码 “cubswin” 登录：

```bash
$ ssh cirros@10.0.0.2
10.0.0.3's password:
$ 
```

如果你在实例中四处查看，你会发现这是一个相当简单的 Linux 安装。那里可能没有太多可做的事情。你可以随时注销。

现在，回到 Horizon 界面，如果你在左侧菜单中导航回“概览”，你将看到你的新实例出现在摘要中。

> **提示**
>
> 通过 Horizon 界面修改实例对于学习和较小规模的部署组织来说很实用，但 OpenStack 的真正威力来自于其 API 和基于命令行界面（CLI）的工具。有关使用 OpenStack CLI 从命令行操作实例的首次讨论，请参阅第 4 章“你的第一个 OpenStack”。

## 仪表板：以管理员身份登录

现在你知道 Horizon 仪表板用户端的样子了，我们将探索管理端。你将使用与演示账户相同的 URL 进行登录，但这次你将运行 `stack.sh` 时定义的管理员密码以 `admin` 身份登录。你很可能会看到图 2.4 中所示的内容。

在这个 Horizon 视图中，你将拥有“身份项目”屏幕，但你还会有一个“管理”菜单部分，使你能够查看和更改关于你的 DevStack 安装的若干事项。

> **提示**
>
> OpenStack 的默认管理屏幕随时间发生了变化，因此你也可能会像使用演示用户那样最终停留在“项目”屏幕上。为了导航到我们在这里确定的默认屏幕，请在左侧菜单中点击“身份”，然后点击“项目”。

这个菜单有两个部分涉及“系统”和“身份”。以下是你需要注意的“系统”面板中关键部分的示例：

- **实例**：查看系统中由不同用户运行的所有实例。你还可以在此屏幕上编辑和操作它们。
- **口味（Flavors）**：更改提供的口味以满足你的运营要求，删除和添加新的口味。
- **系统信息**：查看你的 DevStack 实例中当前启用的内容概览。

接下来，你需要探索“身份”面板，它包含以下内容：

- **项目**：OpenStack 云中的一个组织单位，可以在具有不同权限的用户之间共享。默认情况下，每个用户都有一个仅属于他们的项目。
- **用户**：允许你操作系统中存在的用户。请注意，其中一些用户是系统用户（如控制 Glance 和 Nova 的用户），对于 OpenStack 的运行是必需的。不应删除这些系统用户。还要注意，在运行 DevStack 时更改密码需要小心，因为其中一些是硬编码在配置文件中的。
- **组**：分配给特定项目或域的一组用户。
- **角色**：你可以分配给特定项目或域的一组已定义的可执行操作。

你可以在第 6 章“私有计算云”中学习更多关于使用 Horizon 的内容。

![](img/8684900d708748f86bb043faa5589f9e_58_0.png)

## 在命令行上与主机交互

既然你已经探索了部分界面，你可以附加到命令行上的屏幕会话，开始探索在前景中以守护进程模式运行的特定进程。

要附加到屏幕，你发出标准的屏幕重新附加命令：

```bash
screen -r
```

初始屏幕会话应该看起来像图 2.5。

由于 DevStack 默认不创建日志文件，所有关于正在运行的服务的信息都分散在 `screen` 进程中的几十个 child screens（子屏幕）中。其中一个有趣的 `screen` 是名为 `n-api` 的屏幕，它显示了 `nova-api` 守护程序的输出。你还可以浏览你刚才在 Horizon 仪表板中进行的调用。

## 导航 Screen

DevStack 使用一种名为 `screen` 的工具来管理在前景中运行的守护进程。以下命令将帮助你导航此 `screen` 会话，以便你可以与守护进程交互并查看它们的运行情况。

连接到正在运行的 `screen` 会话：

```bash
screen -r
```

一旦你进入 `screen` 会话，以下键组合将列出所有正在运行的 child screens：

```bash
ctrl + a + "
```

然后，你可以使用向上和向下箭头在 screens 之间导航。稍后，如果你希望去特定的 `screen` 并且知道其编号，可以使用以下命令：

```bash
ctrl + a + `
```

这将显示一个提示，你可以在其中输入你要去的 `screen` 编号。

如果你只是想概览所有 screens 中显示的内容，你可以使用以下命令逐一导航：

```bash
ctrl + a + n
ctrl + a + p
```

这些将分别带你到下一个和上一个 `screen`。

最后，要从这个 `screen` 会话脱离并返回终端，输入以下内容：

```bash
ctrl + a + d
```

![](img/8684900d708748f86bb043faa5589f9e_60_0.png)

既然你已经熟悉了系统中运行的内容，那么你也可以开始使用 OpenStack 命令行客户端来启动实例、查看实例状态等。首先，你需要通过 `source` `devstack` 目录中的 `openrc` 文件来加载凭证。以下是几个简单的入门命令：

```bash
$ source ~/devstack/openrc
$ openstack flavor list
$ openstack server list --all-projects
```

你将在后续章节中了解更多关于 OpenStack Client 命令的内容，并在附录 E“OpenStack Client (OSC)”中找到基本参考。

## DevStack 选项

本章的前一节介绍了如何在没有任何自定义的情况下启动 DevStack。然而，为了测试 OpenStack 开发版本的各个方面，建议进行自定义设置。

## DevStack “稳定版”

DevStack 中一个鲜为人知的功能是可以使用 DevStack 脚本启动 OpenStack 的稳定版本。开发人员和 OpenStack 持续集成堆栈大量使用此功能来测试升级。不过，它也可以帮助新手体验特定已发布的 OpenStack 版本，而不仅仅是开发版本。如果你在运行 `master` 分支的 DevStack 版本时遇到问题，使用这个稳定版本来入门 OpenStack 也很有价值。

> **注意**
>
> 尽管这会安装 OpenStack 的稳定版本，但这仍然不是在生产环境中运行 OpenStack 的可维护或推荐方式。你应该继续使用稍后可以重新安装的虚拟机或备用系统，并学习适当的分离和高可用性流程以维护生产系统。

使用 DevStack 运行 OpenStack 稳定版本的步骤是之前提到的三个步骤的略微修改版，增加了一步切换到克隆的 `git` 仓库中受支持的稳定分支之一：

```bash
$ git clone git://git.openstack.org/openstack-dev/devstack.git
$ cd devstack
$ git checkout stable/mitaka
$ ./stack.sh
```

> **提示**
>
> 想要列出 DevStack 中可用的稳定分支以供选择吗？在 `devstack` 目录下，输入：
>
> ```bash
> git branch -a
> ```
>
> OpenStack 版本是按字母顺序排列的，因此分支列表中的最后一项将是最新的稳定版本。

与运行标准 DevStack 一样，这需要一些时间来下载依赖项并设置环境。它不会从开发版本拉取，而是从请求的稳定环境拉取。
