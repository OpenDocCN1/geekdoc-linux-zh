
# Docker 容器：使用 Kubernetes、Flannel、Cockpit 和 Atomic 进行构建与部署 (Negus Live Linux 系列)

> 一如既往，我将本书献给我的妻子 Sheree。

—Christopher Negus

（注：后续章节内容在原文中存在大量重复，根据“一定不要重复输出原文”的指令，此处仅展示已翻译的结构框架，如需完整翻译所有重复部分请告知。）

重启容器 ................................................................................ 113

向容器发送信号 ................................................................................ 114

暂停和恢复容器 ........................................................................ 115

等待容器的退出码 ....................................................................... 116

重命名容器 ....................................................................................... 117

创建容器 ....................................................................................... 117

总结 ....................................................................................................................... 118

## 第9章 配置容器存储 ................................................... 121

管理容器存储 ................................................................................... 122

使用宿主机的卷 ................................................................................ 122

数据卷容器 ....................................................................................... 123

对绑定挂载进行写保护 ............................................................................ 124

挂载设备 ............................................................................... 125

挂载套接字 .............................................................................. 125

Docker 主机的存储策略 .......................................................... 127

为 Docker 主机附加外部存储 ................................................... 128

总结 ....................................................................................................................... 130

## 第10章 配置容器网络 ............................................... 133

向其他容器暴露端口 ...................................................................... 134

在宿主机外映射端口 ................................................................................ 136

从链接的容器映射端口 ................................................................... 136

连接不同主机上的容器 ........................................................................ 138

`docker0` 桥接的替代方案 ................................................................ 139

更改容器的网络模式 ................................................... 140

检查网络选项 ....................................................................... 140

更改 Docker 网络桥接 ........................................................................ 142

总结 ....................................................................................................................... 143

## 第11章 清理容器 ........................................................ 145

为镜像和容器清理空间 ................................................... 146

删除镜像 ....................................................................................................... 146

删除单个镜像 ....................................................................... 147

删除多个镜像 ...................................................................... 148

删除容器 ................................................................................ 150

删除单个容器 ....................................................................... 150

删除多个容器 ...................................................... 152

清理并保存容器 ................................................................. . . . . . 153

清理并保存 Fedora 容器 ................................................. . . . . . 154

## 第12章 构建 Docker 镜像 ................................................................... 157

在 Dockerfile 中设置执行执行命令 ................................................................................ 161

使用 `ENTRYPOINT` 指令 ......................................................................................................... 162

从 Dockerfile 向镜像添加文件 ................................................................................................ 164



# 第三部分

# 在云环境中运行容器

## 第13章 使用超级特权容器 (Super Privileged Containers)

- 在 Atomic 主机中使用超级特权容器
- 理解超级特权容器
- 向宿主机开放权限
- 访问宿主机进程表
- 访问宿主机网络接口
- 访问宿主机进程间通信
- 访问宿主机文件系统
- 准备使用超级特权容器
- 使用 `atomic` 命令
- 使用 `atomic` 安装 SPC 镜像
- 使用 `atomic` 获取 SPC 镜像信息
- 使用 `atomic` 运行 SPC 镜像
- 使用原子操作停止并重启 SPC
- 更新 SPC 镜像
- 卸载 SPC 镜像
- 尝试某些 SPC
- 运行 RHEL 工具 SPC
- 运行日志 (`rsyslog`) SPC
- 运行系统监控 (`sadc`) SPC
- 总结

## 第 14 章 使用 Cockpit 在云端管理容器

- 了解 Cockpit
- 从 Cockpit 开始
- 向 Cockpit 添加服务器
- 在 Cockpit 中处理容器工作
- 向 Cockpit 添加容器镜像
- 从 Cockpit 运行镜像
- 在 Cockpit 中处理网络接口
- 在 Cockpit 中配置存储
- 在 Cockpit 中执行其他管理任务
- 在 Cockpit 中管理管理员账户

- 在 `Dockerfile` 中分配环境变量
- 使用其他 `docker build` 命令选项
- 清理镜像
- 保持容器简单
- 总结



在 `Cockpit` 中打开终端 ................................................................ 209

总结 .......................................................................................................... 210

## 第四部分 管理多个容器 ................................................... 211

### 第 15 章 使用 Kubernetes 编排容器 ........................ 213

了解 Kubernetes .......................................................... 214

从 Kubernetes 开始 ......................................................... 216

设置全合一 Kubernetes 配置 ................................... 218

安装并启动 Kubernetes ................................ 218

在 Kubernetes 中启动 Pod ........................................ 220

使用 Kubernetes 进行工作 .......................................................... 223

总结 .......................................................................................................... 224

### 第 16 章 创建 Kubernetes 集群 ................................... 225

了解 Kubernetes 高级特性 ................... 226

设置 Kubernetes 集群 ....................................... 226

第 1 步：安装 Linux ................................................................... 227

第 2 步：设置 Kubernetes 主节点 ....................................... 227

第 3 步：设置 Kubernetes 节点 . . . . . . . . . . . . . . . . 230

第 4 步：使用 Flannel 设置网络 . . . . . . . . . . . . . . . . 231

在 Kubernetes 集群中启动 Pods . . . . . . . . . . . . . . . . . 233

删除副本控制器、服务和 Pods . . . . . . . . . . . . . . . . 237

总结 . . . . . . . . . . . . . . . . . . . . . . . 238

## 第五部分 开发容器 . . . . . . . . . . . . . . . . . . 239

### 第 17 章 开发 Docker 容器 . . . . . . . . . . . . . . . . . . 241

容器开发准备. . . . . . . . . . . . . . . . . . . 241

为红帽系统选择容器开发环境. . . . . . . . . . . . . . . . . . 242

来自 Docker 的容器开发环境 . . . . . . . . . . 246

使用良好的开发实践 . . . . . . . . . . . . . . . . . . 247

为构建收集或排除文件. . . . . . . . . . . . . . . . . . 248

利用分层优势. . . . . . . . . . . . . . . . . . . . . . . . . 249

在构建中管理软件包 . . . . . . . . . . . . . . . . . . . 250

学习更多关于构建容器的知识. . . . . . . . . . 251

总结 . . . . . . . . . . . . . . . . . . . . . . . . . . . 252

### 第 18 章 探索示例 Dockerfile 文件 . . . . . . . . . . 253

检查官方 Docker 镜像的 Dockerfile. . . . . . . . . . . 254

查看 CentOS Dockerfile. . . . . . . . . . . . . . . . . . . . . . 254

查看 Busybox Dockerfile. . . . . . . . . . . . . . . . . . . . . . . . 257

检查开源项目的 Dockerfile . . . . . 258

查看 WordPress Dockerfile. . . . . . . . . . . . . . . . . . . . . . . 258

查看 MySQL Dockerfile. . . . . . . . . . . . . . . . . . . . . . . 260

检查用于桌面和个人使用的 Dockerfile . . . . 263

查看 Chrome Dockerfile. . . . . . . . . . . . . . . . . . . . . . . 263

查看 Firefox Dockerfile. . . . . . . . . . . . . . . . . . . . . . . 267

总结 . . . . . . . . . . . . . . . . . . . . . 270

索引.. . . . . . . . . . . . . . . . . . . . . . 273

# 前言

Docker 是一种容器化技术，处于构建、打包和部署应用程序的核心。它潜力影响计算的各个方面，从应用开发过程到在大数据中心中的部署和扩展。

尽管 Docker 非常受欢迎，但它仍然是一个相对新的项目，许多人并不真正清楚它意味着什么。如果你是其中之一，本书将帮助你迈出第一步，同时让你开眼界看到容器化未来为你承诺的巨大潜力。

# 前言

`命令行 shell`：Docker 提供了图形化界面供用户操作。然而，本书中的大多数 Docker 示例均来自 Linux 命令行 shell。熟悉如何在 Linux shell 中进行操作，将使你使用 Docker 的工作效率变得高得多。

`软件包`：Docker 本身是一种将软件打包并作为捆绑应用程序进行交付的机制。然而，为了构建容器镜像，大多数 Docker 基础镜像都配置为允许你从其基于的特定 Linux 发行版安装软件包。

例如，对于 Ubuntu 基础镜像，你应该了解如何使用 `apt-get` 等工具安装 Deb 软件包。对于 Fedora、Red Hat Enterprise 或 CentOS 镜像，`yum`、`dnf` 和 `rpm` 命令会非常有用。当你使用这些基础镜像构建你自己的 Docker 容器时，这些镜像通常会被设置为从在线软件仓库获取你请求的软件包。了解如何在所选的 Linux 发行版中获取和安装软件包，对于你成功使用 Docker 至关重要。

`文件所有权与权限`：Linux 系统以及容器内的每个文件都由特定的用户和组所有，并具有某些允许访问这些文件的权限。有时，你希望从宿主机向容器内部授予文件和目录（文件夹）的访问权限。其中一些可能是特殊文件，例如应用程序运行所需的设备或套接字。进程也会以特定用户的身份运行。理解这些权限的工作原理对于确保容器正常运行至关重要。

我只提到了有效操作 Docker 容器时需要的几个较明显的特性。在你继续探索如何充分利用以及自己创建 Docker 容器时，你还会遇到许多与其他 Linux 相关的特性。

如果你不熟悉 Linux，我强烈建议你参加一个课程或买一本至少提供 Linux 基础知识的书，以帮助你上手 Docker 容器。我个人的建议是读一本由本书编写的《Linux 圣经》（Linux Bible）第九版（http://www.wiley.com/WileyCDA/WileyTitle/productCd-111899878.html）。它不仅能专门帮助你构建 Docker 容器所需的技能，还能帮助你在开发 Docker 容器镜像时通用的在 Linux 环境中工作。

# 本书内容

本书旨在供初接触 Docker 容器的人士从头到尾阅读。之后，它可以作为参考资料，提醒你与 Docker 容器相关的各种选项和功能。本书分为五个部分。

# 第一部分：容器入门



# 第一部分：入门知识

在第一部分，你将学习开始使用 Docker 容器所需的知识。第 1 章“使用 Docker 容器化应用程序”描述了什么是容器以及它们与未容器化的应用程序有什么区别。在第 2 章“设置容器运行时环境”中，你将学习如何在 Fedora 和 Ubuntu 等不同的通用 Linux 系统上安装 Docker，以及如何在 CoreOS 和 Project Atomic 等专门面向容器的 Linux 系统上安装 Docker。在第 3 章“设置私有仓库”中，我们通过向你展示如何配置一个私有的 Docker 仓库来存放你的 Docker 镜像，完成了一次基础设置。

# 第二部分：操作单个容器

此部分的大部分内容涉及使用 `docker` 命令直接操作单个容器。在第 4 章“运行容器镜像”中，我将向你展示如何运行第一个容器镜像。为了帮助你查找并获取镜像，第 5 章“查找、拉取、保存和加载容器镜像”描述了如何从 Docker 仓库搜索容器镜像，然后拉取所需的镜像、将其保存为文件并加载到另一个 Docker 系统中。

在第 6 章“标记镜像”中，你将学习如何为镜像打标签，以便更好地识别镜像包含的内容，并利用这些信息将镜像推送到仓库。在第 7 章“调查容器”中，我将向你展示如何查看 Docker 容器或镜像内部，了解该容器或镜像的工作细节。在第 8 章“启动、停止和重启容器”中，你将学习如何停止、启动和重启容器。

在第 9 章“配置容器存储”中，你将学习如何配置存储，主要通过将宿主机的目录挂载到容器内部。要学习如何为容器配置网络，第 10 章“配置容器网络”描述了如何配置 Docker 服务通常使用的（或不使用的）默认网络，以及每个运行容器的人如何为单个容器设置网络接口。

Docker 会缓存大量数据以便重复使用。在第 11 章“清理容器”中，我将向你展示如何清理创建或运行 Docker 镜像时留下的缓存。在第 12 章“构建 Docker 镜像”中，你将学习如何构建自己的 Docker 容器，包括如何构建构建和运行高效的容器。

# 第三部分：在云环境中运行

在第 13 章“使用超级权限容器”中，我描述了如何运行所谓的超级权限容器（SPCs）。为了说明 SPCs 的工作原理，我将向你展示如何在 RHEL Atomic 系统上获取几个执行不同管理任务的镜像。在第 14 章“使用 Cockpit 在云端管理容器”中，我描述了如何使用 Cockpit 网页版容器管理工具在你的云或本地环境中跨多个主机管理容器。

# 第四部分：管理多个容器

在这一部分，我将进入编排领域。在第 15 章“使用 Kubernetes 编排容器”中，我描述了如何在一个系统上使用 Kubernetes 主节点和节点服务来尝试 Kubernetes。在第 16 章“创建 Kubernetes 集群”中，我将跨越一体机系统，描述如何设置一个集群。有了该集群，你就可以可以在节点的 Pod 上部署应用程序。

# 第五部分：开发容器

在短段时间内，已经出现了一些提高容器构建效率的技术。在第 17 章“开发容器”中，我描述了一些开发容器的技巧。最后，在第 18 章“探索 Dockerfile”中，我向你展示我见过的各种 Dockerfile，以说明人们是如何克服构建容器障碍的。

所以，如果你现在准备好了，就开始阅读吧。希望你喜欢这本书！

# 致谢

在制作本书期间，我获得的帮助是超凡的。在我的日常工作中，我有幸能与 Red Hat 的人员直接合作，他们将 Docker、Kubernetes 和 Atomic 等项目的优秀工作扩展并集成到适用于大多数企业环境的操作系统中。因此，来说，我要感谢 Red Hat Enterprise Linux Atomic、OpenShift 以及 Linux 团队的开发者、测试人员和其他作者，他们每天告诉我如何让 Linux 容器企业化。

对于对本书有直接影响的人，我想点名 Red Hat 的几个人。首先，William Henry 为本书撰写了关于存储和网络的两个章节。我很幸运他能编写这些关键章节。除了他的工作外，William 对 Docker 相关项目做出了重大贡献。事实上，William 编写了 Docker 软件自带的几十页命令说明。让他参与并帮助本书的发展是非常贵的。

Red Hat 的另一位重要贡献者是 Scott Collier。Scott 对 Docker 知识的公开贡献包括设置 Docker 和 Kubernetes 的博客，以及通过 Fedora Cloud 共享许多示例 Dockerfile。对于这本书，Scott 慷慨投入时间，帮助我梳理书中贯穿的技术和示例。

由于我是在工作时间之外编写这本书的（这也是为什么它比我预想的要长），因此我经常在晚上和周末与出版社（Pearson）互动。所以，感谢编辑 Chris Zahn 和 Elaine Wiley 审核我的内容，偶尔在周日晚上回复并进行压缩。

最后，我想感谢我的家人。当一个人在写书时，几乎必然要在某段时间内忽略家庭。我为你们所有人感到非常自豪。尽管我经常埋头写作，我的儿子 Seth 却在《歌舞高中会》中完美地模仿了扎克·埃弗隆，他在学校剧剧中担任主角，同时还参加了高中的足球队。我的儿子 Caleb 找到了自己的定位，在缅因州的他那块小有机农场安顿了下来。而我的妻子 Sheree 一直通过她的健身和斯巴特人跑步让年轻一代感到惊叹。你们的爱和支持是我继续前进的动力。

## 关于作者

Chris 于 2008 年加入红帽，担任 RHCE 讲师。为了这一角色，他成为了红帽认证讲师 `RHCI` 和红帽认证考官 `RHX`。2014 年，Chris 成为红帽认证架构师 `RHCA`，获得了虚拟化管理、部署与系统管理、集群与存储管理以及服务器加固认证。2011 年，Chris 从 Linux 讲师职位转回成为红帽的全职作家，并一直工作至今。

在职业生涯早期，Chris 曾在 UNIX 实验室和 AT&T 贝尔实验室与生产 UNIX 操作系统的组织工作。在此期间，Chris 编写了第一份官方 UNIX System V 桌面系统手册，并合写了《UNIX 桌面指南》。在八年时间里，Chris 与 UNIX 系统的开发者紧密合作，涵盖了从 UNIX System V Release 2.0 到 Release 4.2 的版本。

## 设置私有 Docker Registry

本章：

- 在 Fedora 或 Ubuntu 中创建私有 Docker 仓库
- 使用 `docker-registry` 软件包
- 使用 `registry` 容器镜像
- 了解 Docker 镜像命名空间

Docker 的基础之一是能够请求使用现有的容器镜像，如果该镜像尚未于你的系统中，则从某处获取并下载到你的系统中。默认情况下，“某处”是 Docker Hub 仓库 `https://hub.docker.com`。然而，有其他方法可以配置其他拉取 Docker 镜像的位置。这些位置被称为仓库（registries）。

通过建立自己的私有仓库，你可以将私有镜像留给自己。你还可以通过在本地推送和拉取镜像来节省时间，而不是将它们发布到互联网上。

设置私有仓库非常简单。它需要获取服务（通过安装软件包或使用 `registry` Docker 容器镜像）、启动服务，并确保相应的端口已开放以便服务可以访问。使用仓库比设置仓库需要更多的解释，特别是考虑到 Docker 每天都会添加新功能，这些功能正在改变 Docker 使用和搜索仓库以查找镜像的方式。

特别是，Docker 使用镜像命名空间的方式正在变得更具适应性。如果你的位置与互联网断开连接，无法访问 Docker Hub，目前正在开发的功能将允许你使用不同的默认仓库。同样，新功能允许你将仓库添加到搜索顺序中，这就像你可以让网络浏览器查看不同的 DNS 服务器一样。

本章描述了如何在多个不同的 Linux 系统上设置私有 Docker 仓库。第一个示例只是为了帮助你快速运行一个 Docker 仓库以开始测试或学习如何使用仓库。之后，我将描述一些让 Docker 仓库更适用于生产环境的技术。

在章的后半部分，我将告诉该如何调整你的本地 Docker 服务使用 Docker 仓库，包括如何将 Docker.io 替换为默认仓库，并将所有其他仓库添加到搜索路径中。

> 注意
>
> 使用此 Docker 并不要求配备本地仓库。然而，当你在这书中构建、保存和复用镜像时，你可能会发现一种存储镜像（尤其是私有镜像）的方法，而无需将它们推送到公共的 Docker Hub 仓库。尽管如此，如果你想在跳到设置 Docker 仓库之前学习更多关于容器的知识，现在可以跳过本章。

### 获取并启动私有 Docker 仓库

你可以通过多种不同的方式在 Linux 系统上运行 Docker 仓库，以存储你自己的 Docker 镜像。对于包含 `docker-registry` 软件包的 Linux 发行版（如 Fedora 和红帽企业 Linux），你可以安装该软件包并启动服务。对于其他发行版，你可以运行来自 Docker.io 的官方 `registry` 容器镜像来提供服务。



请查看本章对应你正在使用的 Linux 系统的章节，了解如何在系统上安装和运行 Docker 仓库。对于 Fedora，我演示了如何使用 `docker-registry` 软件包，而对于 Ubuntu，我展示了如何使用 `registry` 容器。

以下是关于设置 Docker 仓库你应该了解的几点通用知识：

- 安装在任何处：像大多数服务器一样，Docker 仓库不需要安装在客户端系统上（即你运行 `docker` 命令的地方）。你可以将其安装在客户端可以通过网络访问的任何 Linux 系统上。这样，多个 Docker 客户端就可以访问你的 Docker 仓库了。

- 开放端口：如果你的 Docker 仓库不在客户端，你必须确保 TCP 端口 `5000` 没有被运行 Docker 仓库的机器防火墙拦截。

- 提供空间：如果你向仓库推送了大量镜像，空间可能会很快填满。对于 `docker-registry` 软件包，存储的镜像包含在 `/var/lib/docker-registry` 目录下。确保在该目录中配置了足够的空间以满足你的需求，或者如果你愿意，也可以配置不同的目录。

# 第 3 章 设置私有 Docker 仓库

## 在 Fedora 中设置 Docker 仓库

按照这些指令在 Fedora 系统上安装并启动 Docker 仓库。目前，此程序通过 `docker-registry` RPM 包创建一个版本1 的 Docker 仓库。虽然此程序在 Fedora 上经过了测试，相同的基本步骤也适用于以下 Linux 发行版：

- Fedora 22 或更高版本
- 红帽企业 Linux 7 或更高版本
- CentOS 7 或更高版本

`docker-registry` 软件包不适用于 Atomic、RHEL 和 CentOS 发行版。因此，你需要使用 `registry` 容器来设置 Ubuntu。

> 注意
>
> 在接下来的过程中，你将使用 `docker-registry` 包来标识你打算存储的镜像。要更深入地了解标记，请参考第 6 章，“标记镜像”。

### 1. 安装 docker-registry

当你在 Fedora 上安装 `docker-registry` 时，它还会拉取十几个依赖包。要安装这些包，请输入以下：

```bash
# yum install docker-registry
...
Transaction Summary ===================
Install 1 Package (+15 Dependent)
Total download size: 6.8 M
Installed size: 39 M
Is this ok [y/N]: y
```

### 2. 列出 docker-registry

使用 `rpm` 命令列出 `docker-registry` 包的内容。该包中有近200个文件（大部分是 Python 代码）。此命令仅显示文档和配置文件：

```bash
# rpm -ql docker-registry | grep -E "(/etc) \|(/usr/share) \|(systemd)"
/etc/sysconfig/docker-registry.yml
/usr/lib/systemd/system/docker-registry.service
/usr/share/doc/docker-registry/
/usr/share/doc/docker-registry/AUTHORS
/usr/share/doc/docker-registry/CHANGELOG.md
/usr/share/doc/docker-registry/LICENSE
/usr/share/doc/docker-registry/README.md
```

### 3. 打开防火墙

如果你的 Fedora 运行着拦截入连接的防火墙，你可能需要开放 TCP 端口 `5000` 以访问仓库服务。假设你在 Fedora 中使用防火墙服务，运行这些命令在防火墙上开放端口（立即且永久），并查看端口已开放：

```bash
# firewall-cmd --zone=public --add-port=5000/tcp
# firewall-cmd --zone=public --add-port=5000/tcp --permanent
# firewall-cmd --zone=public --list-ports
```

### 4. 启动 docker-registry 服务

如果你想对 Docker 仓库进行任何特殊配置，请在启动服务之前参考后续章节。对于简单的 `docker-registry` 安装，你可以如下启动服务并开始使用（状态显示 `docker-registry` 服务已激活并启用）：

```bash
# systemctl start docker-registry
# systemctl enable docker-registry
```

Created symlink from /etc/systemd/system/multi-user.target.wants/docker-registry.service to /usr/lib/systemd/system/docker-registry.service.

```bash
# systemctl status docker-registry
```

`docker-registry.service - Registry server for Docker`

Loaded: loaded (/usr/lib/systemd/system/docker-registry.service; vendor preset;)

Active: active (running) since Mon 2015-05-25 12:02:14 EDT; 42s ago

主进程 PID: 5728 (gunicorn)

CGroup: /system.slice/docker-registry.service

  -└-5728 /usr/bin/python /usr/bin/gunicorn --access-logfile

      --requests 100 --graceful-timeout 3600-t 36...

### 5. 获取镜像

用于测试 Docker 的常用镜像是 Docker Hub Registry 提供的 `hello-world` 镜像。按照如下方式运行该镜像（这会将镜像拉取到本地系统并运行）：

```bash
# docker run --name myhello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from docker.io/hello-world
91c95931e552: Download complete
a82819747be10: Download complete
Hello from Docker.
docker.io/hello-world:latest: The image you are pulling has been verified.
```

### 6. 允许访问仓库

Fedora 和 Red Hat Linux 中的 `docker` 客户端要求从仓库获取证书，或者将该仓库识别为不安全。在本示例中，你可以通过编辑 `/etc/sysconfig/docker` 文件并在该文件中创建以下行将仓库识别为不安全：

```bash
ADD_REGISTRY='--add-registry localhost:5000'
INSECURE_REGISTRY='--insecure-registry localhost:5000'
```

之后，重启本地 Docker 服务：

```bash
systemctl restart docker
```

### 7. 标记镜像

使用 `docker tag` 给镜像命名，你可以使用该名称将镜像推送到本地系统的 Docker 仓库：

```bash
# docker tag hello-world localhost:5000/hello-me:latest
```

### 8. 推送镜像

要将 `hello-world` 推送到本地 Docker 仓库，输入以下内容：

```bash
# docker push localhost:5000/hello-me:latest
```

推送引用的是仓库 `[localhost:5000/hello-me]` (1 个标签)

...

Pushing tag for rev `[91c95931e552]` on

```bash
(http://localhost:5000/v1/repositories/hello-me/tags/latest)
```

### 9. 拉取镜像

为了确保你能从仓库中检索镜像，在第二个终端中，从系统中删除该镜像，然后尝试从你的仓库中检索它：



```bash
# docker rm myhello
# docker rm hello-world localhost:5000/hello-me:latest
# docker pull localhost:5000/hello-me:latest
pulling repository localhost:5000/hello-me
91c95931e552: Download complete
a821974b7be10: Download complete
# docker images
```

| REPOSITORY | TAG | IMAGE ID | CREATED | VIRTUAL | SIZE |
| :--- | :--- | :--- | :--- | :--- | :--- |
| localhost:5000/hello-me | latest | 91c95931e552 | 5 周前 | | 910 B |

在刚刚显示的示例中，镜像已成功从本地仓库进行了推送和拉取。此时，你有以下选择：

- 如果你想了解更多关于 Docker 仓库的工作原理并可能修改其行为，请跳到本章后半部分的“配置私有 Docker 仓库”章节。
- 如果你准备好开始使用 Docker 容器，请跳到第 4 章“运行容器镜像”。

下一节将描述如何在 Ubuntu 中设置 Docker 仓库。

## 在 Ubuntu 中设置 Docker 仓库

与其通过软件包安装 Docker 仓库，你也可以从 Docker Hub Registry 下载仓库容器并使用它提供 Docker 仓库服务。这是尝试 Docker 仓库的一种快速方便的方法，尽管默认仓库在生产环境中的扩展性较差，且配置更为复杂。

> 注意
>
> 有多个版本的仓库可用。在本示例中，我使用了 `registry:latest`，它会产生一个版本 1 的 Docker 仓库镜像。当你尝试这样做时，可能已经有了稳定的版本 2。我建议你参考此处获取运行版本 2 Docker 仓库的信息：https://docs.docker.com/registry/

尽管此过程在 Ubuntu 14.04 上测试过，但相同的基本过程应该适用于任何运行 Docker 服务的 Linux 系统。

要在此开始，请按照第 2 章“设置容器运行时环境”中的描述安装 Docker，并启动 Docker 服务。我建议你打开两个终端窗口（shell）来执行此操作。打开一个你计划运行仓库服务的终端，这样你可以在启动和测试时观察其进度。另一个终端则可以在其中推送和拉取镜像。

- 获取仓库镜像：按照如下方式运行 `docker pull` 命令，从 Docker Hub Registry 拉取仓库镜像（关于 `docker pull` 的描述请参见第 5 章“查找、推送、保存和加载容器镜像”）：

```bash
$ docker pull registry:latest
Pulling repository registry
204704ce3137: Download complete
e9e06b6e14c: Download complete
```

- 运行仓库镜像：为了尝试 Docker 仓库，请在前台运行该镜像，你可以观察容器镜像运行时产生的消息（关于 `docker run` 的描述请参阅第 4 章）。此命令启动了最新的仓库镜像，暴露了端口以便外部客户端使用，并在第一个终端中运行：

```bash
$ docker run -p 5000:5000 registry:latest
[2015-05-25 21:33:35] [INFO] Starting gevent
[2015-05-25 21:33:35] [INFO] Listening at: http://0.0.0.0:5000
[2015-05-25 21:33:35] [INFO] Using worker
```

- `b 0.0.0.0:5000`：将工作进程绑定到系统上所有 IP 地址 `0.0.0.0` 的 5000 端口。这允许 Docker 客户端通过系统上的任何外部网络接口，通过 TCP 端口 5000 访问到 Docker 注册仓库。
- `w 4`：将工作进程的数量设置为 4（在原始的 gunicorn 进程之上）。
- `docker-registry.wsgi:application`：使用 Docker 注册仓库 wsgi 应用程序运行进程。

要更改 `docker-registry` 服务的行为，你可以编辑 `/etc/sysconfig/docker-registry` 文件。以下是该文件在 Fedora 中的默认设置方式：

```
# 注册仓库配置文件（file）
DOCKER_REGISTRY_CONFIG=/etc/docker-registry.yml
```

```
# 使用来自 DOCKER_REGISTRY_CONFIG 的配置
SETTINGS_FLAVOR=local
```

```
# 绑定到注册仓库的地址
REGISTRY_ADDRESS=0.0.0.0
```

```
# 绑定到注册仓库的端口
REGISTRY_PORT=5000
```

```
# 处理连接的工作进程数量
GUNICORN_WORKERS=4
```

在 `docker-registry` 文件中，你可以执行此类操作，让 Docker 注册仓库仅监听某个特定的 IP 地址（默认情况下，`REGISTRY_ADDRESS=0.0.0.0` 监听所有地址）。你也可以将服务的端口更改为 TCP 端口 5000 以外的端口，或者将 `gunicorn` 工作进程的数量设置为非 4 的数字。

`/etc/docker-registry.yml` 文件被设置为 Docker 注册仓库的配置文件。`SETTINGS_FLAVOR=local` 告诉配置包含常用变量，并设置 `/var/lib/docker-registry` 目录用于本地存储。在 `/etc/sysconfig/docker-registry` 文件，你可以设置以下常用变量：

- `LOGLEVEL`：默认日志级别设置为 `info`。它也可以设置为 `debug`、`notice`、`warning`、`err`、`error`、`crit`、`alert`、`emerg` 或 `panic`。
- `DEBUG`：设置为 `true` 或 `false` 以开启或关闭调试。
- `STANDALONE`：如果设置为 `true`（默认值），注册仓库将作为独立注册仓库运行，不查询 Docker 索引。

### 第 3 章 搭建私有 Docker 注册仓库

- `INDEX_ENDPOINT`：如果本地仓库未设置为独立模式运行（默认值），则索引端被设置为 `https://index.docker.io`。
- `STORAGE_REDIRECT`：默认禁用此项功能。
- `DISABLE_TOKEN_AUTH`：如果服务不是独立模式，则启用此变量以允许令牌认证（token authentication）。
- `PRIVILEGED_KEY`：默认未设置特殊密钥。
- `SEARCH_BACKEND`：默认没有搜索后端。
- `SQLALCHEMY_INDEX_DATABASE`：默认 SQLite 后端数据库设置为：`sqlite:///tmp/docker-registry.db`。

如果你想使用除 `local` 以外的配置变体（flavor），请查看 `/etc/docker-registry.yml` 文件。设置不同的变体用于 Ceph Gateway 配置、Google Cloud Storage 配置、OpenStack Swift Storage 等。

你可以设置的其他变量可以被 gunicorn 进程获取，包括以下内容。请注意，其中一些值会出现在 gunicorn 命令行中：

- `GUNICORN_GRACEFUL_TIMEOUT`：设置优雅重启工作进程的超时时间（秒）。
- `GUNICORN_SILENT_TIMEOUT`：设置重启静默工作进程的超时时间（秒）。
- `GUNICORN_USER`：以此处设置的用户运行 gunicorn 进程，而不是以 root 权限运行。
- `GUNICORN_GROUP`：以此处设置的组运行 gunicorn 进程，而不是以 root 权限运行。
- `GUNICORN_ACCESS_LOG_FILE`：设置访问日志的路径。
- `GUNICORN_ERROR_LOG_FILE`：设置错误日志的路径。
- `GUNICORN_TIMEOUT`：设置 gunicorn 的请求超时时间。
- `GUNICORN_WORKERS`：设置 gunicorn 工作进程的数量。
- `GUNICORN_BIND`：设置 gunicorn 绑定的地址和端口。
- `GUNICORN_PYTHONPATH`：设置 gunicorn 的 Python 路径。



`GUNICORN_OPTIONS`：传递给 `gunicorn` 的额外选项。

以下是翻译的内容：

- `b 0.0.0.0:5000`：将工作进程绑定到系统上所有 IP 地址 (`0.0.0.0`) 的 5000 端口。这允许 Docker 客户端通过系统上的任何外部网络接口，通过 TCP 端口 5000 访问到 Docker 注册仓库。
- `w 4`：将工作进程的数量设置为 4（在原始的 `gunicorn` 进程之上）。
- `docker-registry.wsgi:application`：使用 Docker 注册仓库 wsgi 应用程序运行进程。

要更改 `docker-registry` 服务的行为，你可以编辑 `/etc/sysconfig/docker-registry` 文件。以下是该文件在 Fedora 中的默认设置方式：

```
# 注册仓库配置文件（file）
DOCKER_REGISTRY_CONFIG=/etc/docker-registry.yml
```

```
# 使用来自 DOCKER_REGISTRY_CONFIG 的配置
SETTINGS_FLAVOR=local
```

```
# 绑定到注册仓库的地址
REGISTRY_ADDRESS=0.0.0.0
```

```
# 绑定到注册仓库的端口
REGISTRY_PORT=5000
```

```
# 处理连接的工作进程数量
GUNICORN_WORKERS=4
```

在 `docker-registry` 文件中，你可以执行此类操作，让 Docker 注册仓库仅监听某个特定的 IP 地址（默认情况下，`REGISTRY_ADDRESS=0.0.0.0` 监听所有地址）。你也可以将服务的端口更改为 TCP 端口 5000 以外的端口，或者将 `gunicorn` 工作进程的数量设置为非 4 的数字。

`/etc/docker-registry.yml` 文件被设置为 Docker 注册仓库的配置文件。`SETTINGS_FLAVOR=local` 告诉配置包含常用变量，并设置 `/var/lib/docker-registry` 目录用于本地存储。在 `/etc/sysconfig/docker-registry` 文件，你可以设置以下常用变量：

- `LOGLEVEL`：默认日志级别设置为 `info`。它也可以设置为 `debug`、`notice`、`warning`、`err`、`error`、`crit`、`alert`、`emerg` 或 `panic`。
- `DEBUG`：设置为 `true` 或 `false` 以开启或关闭调试。
- `STANDALONE`：如果设置为 `true`（默认值），注册仓库将作为独立注册仓库运行，不查询 Docker 索引。

## 第 3 章 搭建私有 Docker 注册仓库

- `INDEX_ENDPOINT`：如果本地仓库未设置为独立模式运行（默认值），则索引端被设置为 `https://index.docker.io`。
- `STORAGE_REDIRECT`：默认禁用此项功能。
- `DISABLE_TOKEN_AUTH`：如果服务不是独立模式，则启用此变量以允许令牌认证（token authentication）。
- `PRIVILEGED_KEY`：默认未设置特殊密钥。
- `SEARCH_BACKEND`：默认没有搜索后端。
- `SQLALCHEMY_INDEX_DATABASE`：默认 SQLite 后端数据库设置为：`sqlite:///tmp/docker-registry.db`。

如果你想使用除 `local` 以外的配置变体（flavor），请查看 `/etc/docker-registry.yml` 文件。设置不同的变体用于 Ceph Gateway 配置、Google Cloud Storage 配置、OpenStack Swift Storage 等。

你可以设置的其他变量可以被 `gunicorn` 进程获取，包括以下内容。请注意，其中一些值会出现在 `gunicorn` 命令行中：

- `GUNICORN_GRACEFUL_TIMEOUT`：设置优雅重启工作进程的超时时间（秒）。
- `GUNICORN_SILENT_TIMEOUT`：设置重启静默工作进程的超时时间（秒）。
- `GUNICORN_USER`：以此处设置的用户运行 `gunicorn` 进程，而不是以 root 权限运行。
- `GUNICORN_GROUP`：以此处设置的组运行 `gunicorn` 进程，而不是以 root 权限运行。
- `GUNICORN_ACCESS_LOG_FILE`：设置访问日志的路径。
- `GUNICORN_ERROR_LOG_FILE`：设置错误日志的路径。
- `GUNICORN_TIMEOUT`：设置 `gunicorn` 的请求超时时间。
- `GUNICORN_WORKERS`：设置 `gunicorn` 工作进程的数量。
- `GUNICORN_BIND`：设置 `gunicorn` 绑定的地址和端口。
- `GUNICORN_PYTHONPATH`：设置 `gunicorn` 的 Python 路径。
- `GUNICORN_OPTIONS`：传递给 `gunicorn` 的额外选项。

Docker Hub Registry。通过这种方式，只有此特定 docker 安装的用户会在你明确包含的注册仓库中搜索镜像。

`INSECURE_REGISTRY='--insecure-registry'` 变量不会显式地允许或拒绝某个仓库。这是一种特定情况：用户想使用本地 Docker 客户端从提供 HTTPS 通信的仓库拉取镜像，但客户端没有该仓库的证书来验证其真实性。取消注释该变量并在行中添加不安全仓库的名称，可以允许 `docker` 命令在没有完全授权的情况下从该仓库拉取镜像。

```
INSECURE_REGISTRY='--insecure-registry myreg.example.com'
```

再次，此功能以及上述描述的其他功能并不是上游 Docker 项目的一部分。但如果你你的安装需要这些功能，可以通过目前存在于 Fedora、RHEL、CentOS 和相关 Atomic 项目中的功能，更改 Docker 默认访问注册仓库的方式。

# 摘要

设置私有 Docker 仓库可以让你能够在不使用公共 Docker Hub Registry 的情况下推送和拉取镜像。本章描述了为自己设置 Docker 仓库的不同方法。

对于提供了 `docker-registry` 包的 Linux 发行版（如 Fedora 和 Red Hat Enterprise Linux），你可以安装该包并使用 `systemctl` 命令启动 `docker-registry` 服务。作为替代方案，任何运行 Docker 服务的系统都可以拉取并运行来自 Docker Hub Registry 的仓库镜像，从而提供私有的 Docker 仓库。

除了如何设置你自己的 Docker 仓库外，本章还描述了 Docker 镜像命名空间的工作原理，并以 Docker Hub Registry 为中心。对该模型的建议修改已经在 Fedora 和其他 Red Hat 赞助的操作系统中实现，并在 Docker 社区中讨论。这些修改使用户能够更改 Docker 服务在搜索和拉取请求时设置哪些仓库。

## 符号

`--net` options, 140-142

## A

- `ADD` 指令, Dockerfile, 164-165
- `ADD_REGISTRY` 变量, 47
- 管理员命令, 在容器内运行, 57-58
- 管理员账户, 管理, Cockpit, 208-209
- 一体一体化 Kubernetes, 217
- 配置, 218-224
- Amazon Web Services, 开启 OpenShift, 243
- Ansible, 开启 OpenShift, 243
- 应用镜像, 检查, 90-92
- 应用, 容器化
- 益处, 4-7
- 挑战性, 7
- 减损, 4-5
- 目标, 10
- 参数, 原子化命令, 179
- 原子化命令, 180-185
- 参数, 181

## Atomic Host

- 配置, 29-30
- Fedora, 30-32
- SPCs (超特权容器), 176-180
- 主机文件系统访问, 179-180
- 主机网络接口访问, 178-179
- 主机进程表访问, 177-178
- IPC 访问, 179
- 开启权限到, 177
- `atomic run` 命令, 183-184
- 属性, 容器, 检查, 99-100

## B

- 基础镜像, 127
- 检查, 89-90
- `bash` shell, 启动交互式, 54-56



# 索引

- 绑定挂载, 写保护, 124-125
- 阻塞注册仓库属性, 47
- 更改, 容器, 检查, 106
- 字符游戏, 56-57
- 更改, 142-143
- `docker0`, 替代方案, 139-142
- 构建容器, 169
- 缓存管理, 170-171
- 为 Red Hat 选择环境, 242-243
- 清理镜像, 169
- 排除文件, 248-249
- 收集文件, 248-249
- 保持目录精小, 169-170
- 层, 249-250
- 软件包包, 250-251
- 资源, 251
- 运行 OpenShift, 243-246
- 设置, 241-247
- 简单性, 170
- Chrome Dockerfiles, 查看, 263-266
- CI (持续集成) Docker, 125
- 清理容器, 153
- Fedora, 154
- Ubuntu, 153-154
- 镜像, 169
- 云端管理, 容器, 193-194, 198-204
- 向 Cockpit 添加服务器, 199-200
- 云原生计算基金会 (CNCF), 214
- 集群, Kubernetes, 217, 225
- 配置, 226-233
- 在...中启动 pod, 233-237
- `CMD` 指令, Dockerfile, 161-162
- CNCF (云原生计算基金会), 214
- 构建镜像, 80, 157-158, 168-169
- `docker build` 命令, 158-181
- Dockerfile, 161
- Cockpit, 194-195, 210
- 添加容器镜像, 199-200
- 配置存储, 207-208
- Containers 标签, 196
- 管理员, 208-209
- 云端容器管理, 193-194, 198-204
- Journal 标签, 196
- Networking 标签, 196
- 网络接口, 204
- 开启终端, 209
- 从...运行镜像, 201-204
- Busybox Dockerfiles, 查看, 257-258
- 缓存, 170-171
- CDK (容器开发包), 242-243
- CentOS Dockerfiles, 30
- 添加 systemd 服务, 256-257
- Atomic, 30
- 查看, 254-257
- 证书, RHEL 包, 47
- Storage 标签, 196

## C

- `docker` 镜像, 12, 53, 147, 154-155
- `docker import`, 12, 154-155
- `docker info`, 11
- `docker inspect`, 11, 87-103, 107
- `docker kill`, 12, 114-115, 118
- `docker load`, 12, 65, 77
- `docker login`, 12
- `docker logs`, 12, 106-107
- `docker pause`, 10, 115-118
- `docker port`, 11
- `docker ps`, 53, 110, 116-117, 150, 155
- `docker ps -a`, 53
- 在容器内运行管理员, 57-58
- 分配名称, 80-81
- `systemctl`, 38
- 仓库名称, 83-86
- `yum filter`, 23
- 代码,退出, 等待, 116
- `atomic`, 180-185
- 参数, 181
- `atomic run`, 183-184
- `curl`, 110-111, 222
- `docker`, 8, 11-12, 15, 20-21
- `docker attach`, 11, 100-105
- `docker build`, 12, 79, 157, 158-161, 167-251
- `docker commit`, 77
- `docker cp`, 107
- `docker create`, 12, 117-119
- `docker events`, 12
- `docker exec`, 11, 105-107
- `docker help`, 11
- `docker history`, 11, 127
- `docker pull`, 12, 65, 73-77, 127
- `docker pull -a`, 66
- `docker pull rhel`, 71
- `docker pull ubuntu`, 66
- `docker push`, 12
- `docker rename`, 12, 117
- `docker restart`, 12, 113-114, 119
- `docker rm`, 12, 51, 150-152
- `docker rmi`, 12, 51, 146-149, 155
- `docker run`, 10, 51-56, 59, 63-65, 73, 117-118, 122, 131, 136, 150
- `docker save`, 12, 65-77
- `docker search`, 65-69, 72-73, 77, 88
- `docker search rhel`, 71
- `docker start`, 10-12, 53, 109-112, 151
- `docker start container`, 53
- `docker stop`, 10-12, 109-112, 118
- `docker stop container`, 53
- `docker tag`, 12, 79-80
- `docker top`, 12, 103-104, 107
- `docker unpause`, 10-12, 115
- `docker version`, 11
- `docker wait`, 11, 119
- `ifconfig`, 141
- `journalctl`, 72, 125
- `kill`, 114
- `kubectl`, 216, 222, 237
- `kubectl create`, 220
- `kubectl delete`, 237
- `kubectl get`, 238
- `logger`, 125
- `mysql_safe`, 222
- `ps`, 54, 102
- `python`, 88, 94, 102
- System 标签, 194
- Tools 标签, 197
- 版本, 194

# 索引

- 暴露端口到, 134-135
- 文件系统, 6
- 检查, 88, 103, 107
- 属性, 99-100
- 更改, 106
- 配置, 94-99
- CPU 限制, 101-102
- 内存, 101-102
- 进程, 103-104
- 进程输出, 106
- 运行, 92-103
- SELinux 上文, 102-103
- 终端会话, 100
- 内内核, 6
- 运行服务时限制资源, 62-63
- 链接, 165
- 从...映射端口, 136-137
- LXC (Linux Containers), 133
- 为...腾出空间, 146
- 在云中管理, 193-194, 198-204
- 宿主机外部映射, 136-139
- 挂载设备, 125
- 挂载套接, 125-126
- 暂停和恢复, 115
- pods, 216-218
- 删除, 237-238
- 跨多个节点部署, 216
- 主节点, 216
- 节点, 216
- 复制控制器, 216
- 资源文件, 217
- 服务, 216
- 启动, 220-223
- 在集群中启动, 233-237
- 使用, 223-224
- 堆叠, 63
- 运行, 63-64
- 进程, 6
- 注册表, 配置, 46
- 移除, 12, 150
- 个别, 150-152
- 多个, 152
- 重命名, 117
- 启动, 113-114
- 运行, 11
- 在...中运行管理命令, 57-58
- `sadc`, 189-191
- 示例镜像, 14
- 保存, 153
- Fedora, 154
- Ubuntu, 153-154
- 向...发送信号, 114-115
- 服务交互, 104-105
- SpCs, 175-177, 185-186, 191
- Atomic Host, 176-180
- 准备使用, 180-185
- 运行日志 (rsyslog), 187-188
- 运行 rhel-tools, 186-187
- 运行系统监控器 (`sadc`), 189-191
- 启动, 93-94, 109
- 离线, 110-111
- 交互式, 112
- ...中的新进程, 105
- 停止, 109
- 离线, 110-111
- 交互式, 112
- 存储镜像, 146-147
- 宿主机, 121 个别, 147-148



- 管理, 121-126 多个, 148-149

- 宿主机策略, 127-130 Kubernetes pods, 237-238

- 特权, 63 离线容器, 启动和停止卷, 110-111

- 宿主机, 122-123 正在容器

- 管理, 121 为 Red Hat 选择环境, 等待退出码, 116 242-243

- 绑定挂载的写保护, 排除文件, 248-249

- 124-125 收集文件, 248-249

- 容器特定的 Linux, 18 层, 249-250

- 配置, 29-34 软件包管理,

- 容器标签页 (Cockpit), 196 资源, 250-251

- 持续集成 (CI) Docker, 125 运行 OpenShift, 243-246

- 从容器复制文件, 107 设置, 241-247

- CoreOS, 32-34 设备, 6

- 挂载, 125

- 可修复镜像, 157

- CPU 限制, 容器, 检查, Devops 模型, Kubernetes, 215

- 101-102 目录, 小型, 169-170

- 创建 Kubernetes 集群 `DISABLE_TOKEN_AUTH` 变量, 217 (`docker-registry` 文件), 45

- `curl` 命令, 110-111, 382 磁盘空间占用, 容器镜像, 51

## D

- 数据卷容器, 123-124 DNS (域名系统), 46

- Debian, 配置, 28 Docker, 3-4, 13 `docker0` bridge 

- DEBUG 变量 (`docker-registry` 文件), 44 替代方案, 139-142

- 删除 docker 攻击命令, 11, 100 容器, 150

- 个别, 150-152

- 多个, 152

- 153, 158-161, 168-171, 251

- `docker` 命令, 8, 11-12, 15, 20-21

- 补全, 11

- Docker Compose, 247

- `docker cp` 命令, 12 从容器复制文件, 107

- `docker diff` 命令, 检查, 106

- `docker exec` 命令, 11, 107 在容器中启动新进程, 105

- Dockerfiles 参考, 251, 254, 270-271

- ADD 指令, 164-165 环境变量, 166

- 分配标签, 167-168

- 构建镜像, 157-158 设置到环境, 161-165

- CMD 指令, 161-162

- ENV 指令, 166

- EXPOSE 指令, 165-166

- LABEL 指令, 167-168

- RUN 指令, 163-164

- Busybox, 257-258

- Chrome, 266

- Firefox, 267-269

- MySQL, 260-263

- WordPress, 258-260

- `docker help` 命令, 11

- `docker history` 命令, 搜索镜像, 69-70

- Docker Hub 注册表, 7-12 在 Fedora 中, 37-40 在 Ubuntu 中, 40-42 私有注册表, 43-45 容器, 46

- `docker search` 命令, 66-69 命名空间, 46-48

- `docker images` 命令, 12, 53, 147, 154-155

- `docker info` 命令, 11, 87, 107

- `docker inspect` 命令, 11-12, 87, 107 检查容器, 88, 103 运行, 92-103

- 检查镜像, 88-89 应用, 90-92 历史, 92

- dockeratic, 247

- `docker kill` 命令, 12, 114-115, 118

- `docker load` 命令, 12, 65, 77

- `docker login` 命令, 12

- `docker logout` 命令, 12

- `docker logs` 命令, 12, 106

- docker Machine, 247

- docker Official Images, 251

- `docker pause` 命令, 10, 115-118

- `docker port` 命令, 46-47

- `docker ps -a` 命令, 53

- `docker ps` 命令, 53, 110, 116-117, 150, 155

- `docker pull -a ubuntu` 命令, 63

- `docker pull` 命令, 12, 65, 73-77, 127

- `docker pull rhel` 命令, 71

- `docker pull Ubuntu` 命令, 62

- `docker push` 命令, 12 注册表, 13

- `docker-registry` 包, 配置, 43-45

- `docker rename` 命令, 12, 117

- `docker restart` 命令, 12, 113-114, 119

- `docker rm` 命令, 12, 51, 150-152

- `docker rmi` 命令, 12, 51, 146-149, 155

- `docker run` 命令, 10-12, 51-56, 59, 63-65, 73, 117-118, 121, 131, 136, 150, 159

- `docker save` 命令, 12, 65, 76-77

- `docker search` 命令, 65-69, 72-73, 77, 88

- `docker search rhel` 命令, 71

- `docker start` 命令, 10-12, 53, 109, 151 离线容器, 110-111 交互式容器, 112

- `docker start container` 命令, 53

- `docker stop` 命令, 10-12, 109, 118 离线容器, 110-111 交互式容器, 112

- `docker stop` 命令, 53

- `docker tag` 命令, 12, 79-80

- `docker top` 命令, 107 子命令, 12

- `docker unpause` 命令, 10-12, 115

- `docker version` 命令, 11

- `wait` 命令, 116, 119

- `wait` 命令, 下载, 22

## E

- `ENTRYPOINT` 指令, Dockerfile, 161-163

- `ENV` 指令, Dockerfile, 166 环境变量, 分配到 Dockerfile, 166

- 退出码, 容器, 等待, 116

- `EXPOSE` 指令, Dockerfile, 165-166 暴露端口, 134 从镜像 Dockerfile, 165-166

- 外部存储, 挂载到宿主机, 128-129 Kubernetes 网络, 231-233

## F

- Flannel, 设置

- GitHub, 253

- Google Chrome Dockerfiles, 查看, 263-266

- unicorn 进程, 43-265

## H

- 历史, 镜像, 检查, 92 宿主机进程, 访问, 177-178 不同的连接, 138-139

- Atomic SPCs (超级特权容器), 176-180 文件系统, 访问, 179-180 网络接口, 访问, 178-179 权限, 13 容器, 122-123

- Atomic Host 配置, 21-24 Atomic Host, 30-32 清理和保存, 154

- 设置 Docker 注册表, 37-40

- 164-165 从容器复制, 107

- 文件系统, 容器, 6

- Dockerfiles, 查看, 267-269

## I

- `ifconfig` 命令, 141

- 添加到 Cockpit, 201 命名为, 80-81

- 挂载用户到, 83-85

- 基础, 127 构建, 80, 157-168-169

- `docker build` 命令, 158-161 Dockerfile, 161-165

- 清理, 169

- 磁盘空间占用, 51

- 运行容器化服务, 59

- 运行容器化 Web 服务器, 59-61

- 交互式运行, 54-57

- 可修复, 157

- Docker 镜像命名空间, 46-48

- 在 Dockerfile 内部导出端口, 165-166

- 导入, 81

- 检查, 88-89 应用, 90-92 基础, 89-90 历史, 92

- 层, 127

- 列出, 12

- 加载, 77

- 为...腾出空间, 146

- 修改, 12

- 标签, 添加标签, 79-80

- 可移植, 157

- 从注册表拉取, 73-76

- rails, 68

- 注册表名称和端口, 80

- 移除, 12, 146-147 个别, 147-148 多个, 148-149



# 索引

- 可重现, 157
- 容器化服务, 59
- 容器化 Web 服务器, 59-61
- 从 Cockpit, 201-204 保存, 76-77
- 搜索, 66, 70-73
- Docker Hub, 69-70
- `docker search` 命令, 66-69
- SPCs (超级特权容器) 使用 `atomic` 命令安装, 182
- 使用 `atomic` 命令获取信息, 182-183
- 运行, 183-184 启动和停止, 184
- 卸载, 185
- 日期, 184

## 管理工具
- 管理工具, 7
- 可更新的, 158
- 用户名, 80
- 可验证的, 158
- 版本名称, 79
- 版本号, 79
- wordpress, 90-91
- 导入镜像, 81
- Red Hat Enterprise Linux, 25
- Ubuntu, 19
- 与容器内部交互, 104-105
- 交互式容器，启动和停止, 112
- 接口，网络，Cockpit, 204-206
- IPC (进程间通信), 6
- 访问, 179
- `INDEX_ENDPOINT` 变量 (`docker-registry` 文件), 45
- 个体

## J-K
- + 容器, 150-152
- 镜像，删除, 147-148
- `info` 参数 (`删除 (atomic` 命令), 148
- 检查容器, 88, 103, 105
- 属性, 99-100
- 更改, 106
- 配置, 94-99
- CPU 限制, 101-102
- 内存, 101-102
- 进程, 103-104
- 进程输出, 106
- 运行, 92-103
- SELinux 上文, 102-103
- 启动, 93-94
- 终端会, 106
- 镜像, 88-89
- 应用, 90-92
- 基础, 89-90
- 历史
- + `journalctl` 命令, 72, 125
- Journal 标签页 (Cockpit), 196
- 内核, 6
- `kill` 命令, 114
- Kitematic, 247
- `kubectl` 命令, 216, 222, 239
- `kubectl create` 命令, 220
- `kubectl delete` 命令, 235
- `kubectl get` 命令, 238
- Kubernetes, 8, 213-216, 224
- 高级功能, 226
- 一体化, 217
- 配置, 218-224
- 集群, 217, 225
- 配置, 226-233
- 在...中启动 pod, 233-237
- 创建服务集, 215
- 数据中心稳定, 215
- Devops 模型, 215
- 通用主机计算机, 215
- 安装, 218-219
- master 节点，设置, 227-229
- 网络，设置, 231-233
- `install` 参数 (`atomic` 命令), 181
- 安装
- Fedora, 22
- Kubernetes, 218-219
- Linux, 227

# 索引 295
- 节点, 226
- 安装, 227
- 设置, 230-231
- 主要发行版, 10
- pods, 216-218
- LinuxDockeriles, 253
- 删除, 237-238
- 列出镜像, 12
- 跨多个节点部署, 216
- 加载镜像, 77
- master, 216
- `logger` 命令, 125
- 节点, 216
- 日志，rsyslog 容器, 187-188
- 副本计数器, 217
- `LOGLEVEL` 变量 (`docker-registry` 文件), 44
- 资源文件, 216
- LVM (逻辑卷管理器),
- 启动, 220-223
- 使用...扩展存储, 129-130
- 在集群中启动, 233-237
- LXC (Linux 容器), 133
- 使用, 233-224

## M
- 副本计数器，删除, 237-238
- Mac OS X, 17
- 服务，删除, 237-238
- 配置, 28
- 启动, 220

## L
- 管理容器存储, 122-126
- `LABEL` 指令, Dockerfile, 167-168
- 主机策略, 127-130
- 端口映射, 134
- 标签，在 Dockerfile 中分配, 167-168
- 外部主机, 136-139
- 层层
- master, Kubernetes,设置, 227-229
- 开发容器, 249-250
- 镜像, 127
- 内存，容器，检查, 101-102
- 链接容器, 165
- Microsoft Windows, 17
- 从...映射端口, 136-137
- 配置, 28
- Linux, 17
- 挂载
- 选择版本, 250
- 设备, 125
- 套接字, 125-126
- Fedora, 21-24
- RHEL, 25-27
- Ubuntu, 18-21
- 容器，删除, 152
- 镜像，删除, 148-149
- 容器特定的, 18
- 配置, 29-34
- MySQL Dockerfiles，查看, 260-263
- `mysqld_saf` 命令, 222

# 索引

## N
- + 命名
  - 为镜像分配仓库, 83-86
  - 分配用户名, 83-85
- 镜像，为其添加标签, 79-80
- 命名空间，Docker 镜像, 46-48
- 镜像命名, 80-81
- 网络, 13
  - 使用 Flannel 为 Kubernetes 设置网络, 231-233
- 网络标签页 (Cockpit), 196
- 网络接口, 6
  - Cockpit, 204–206
- 网络模式，容器，更改, 140
- 节点, Kubernetes, 226
  - 设置, 230–231
- + Linux, 17
  - 配置, 18-21
  - 容器特定的, 18, 29-34
- Mac OS X, 17
  - 配置, 28
- Microsoft Windows, 17
  - 配置, 28
- RHEL (Red Hat Enterprise Linux), 175
  - Atomic, 30, 128
  - 配置, 25-27
  - 容器开发, 242-243
- SUSE, 配置, 28
  - 下载, 25
  - 安装, 25
- OS X, 17
  - 配置, 28
  - 输出, 106
- + 官方仓库 (Docker Hub), 69
- OpenShift, 241-242
- 开源 Dockerfiles，查看
- 开源项目, Dockerfiles, 253
- 操作系统
  - CentOS, 配置, 28
  - CoreOS, 配置, 32-34
  - Debian, 配置, 28
  - Fedora, 配置, 21-24
- + 暂停容器, 115-116
- pods, Kubernetes, 216-218
  - 删除, 237-238
  - 跨多个节点部署, 216
  - master, 216
  - 节点, 216
  - 副本计数器, 216
  - 资源文件, 217
  - 服务, 216
  - 启动, 220-223
  - 在集群中启动, 233-237
  - 使用, 223-224

## Q-R
- + 可迁移镜像, 157
- 暴露, 134
- 从 Dockerfile 内部, 165-166
- 到其他容器, 134-135
- 映射, 134
- 外部主机, 136-139
- 私有注册库，配置, 35-37, 43-46
- `docker-registry` 软件包, 43-45
- 注册库容器, 46
- 特权容器, 63
- 权限, 63-64
- 打开到主机, 177
- 检查, 103-104
- 输出输出, 106
- 启动新的, 105
- gunicorn, 43-45
- `ps` 命令, 54, 102
- 从注册库拉镜像, 73-76
- 确认, 47
- `python` 命令, 88, 94
- + rails 镜像, 68
- Red Hat Enterprise Linux. 查看 RHEL (Red Hat Enterprise Linux)
- 注册库, 65
- 在 Fedora 中配置, 37-40
- 在 Ubuntu 中配置, 40-42
- 私有注册库，配置, 35-37, 43-46
- 私有的，配置, 35-37, 43-46
- 镜像搜索, 66-69
- 拉取镜像, 73-76
- 删除容器, 150
- 个体, 150-152
- 多个, 152
- 镜像, 146-147



# 索引 288

- 多个, 148-149
- Kubernetes 副本计数器, 237-238
- Kubernetes 副本计数器, 237-238
- 仓库, 65
- 镜像分配名称, 83-86
- 可复的镜像, 157
- 容器, 189-191
- 在容器中运行时限制资源, 62-63
- 重启容器, 113-114
- 容器, 153
- RHEL (Red Hat Enterprise Linux), 175
- Ubuntu, 153-154
- 镜像, 76-77
- 下载, 25
- 安装, 25
- 属性, 46
- `SEARCH_BACKEND` 变量 (`docker-registry` 文件), 45
- `rhel-tools` 容器，SPCs, 186-187
- `pm -ql` 命令, 23
- 搜索镜像, 66, 70-73
- Docker Hub, 69-70
- `rsyslog` 容器, 187-188
- `run` 参数 (`atomic` 命令), 181
- `docker search` 命令, 66-69
- Search Registry (Docker Hub), 69
- `RUN` 指令, Dockerfile, 163-164
- 密钥, RHEL docker 软件包, 27
- Security Enhanced Linux (SELinux), 122-123
- 容器中的管理命令, 57-58
- 交互式容器镜像, 54-56
- SELinux 上文，容器，检查, 102-103
- SELinux (Security Enhanced Linux), 122-123
- 管理命令, 57-58
- 基于字符的游戏, 56-57
- 容器化服务, 59
- 容器化 Web 服务器, 59-61
- 容器, 11
- 服务器，加入 Cockpit, 199-200
- 服务
  - 检查, 92-103
  - 与容器交互, 104-105
  - Kubernetes，删除, 237-238
- Services 标签页 (Cockpit), 196
- shell, bash，交互式启动, 54-56
- SIGHUP 信号, 115
- SIGINT 信号, 115
- SIGKILL 信号, 114-115
- 发送到容器的信号, 114-115
- SIGTERM 信号, 115
- 存储, 13, 130-131
- 套接字，挂载, 125-126
- 将外部挂载到主机, 128-129
- SPCs (超特权), 175-177, 185-186
- 配置, Cockpit, 207-209
- Atomic Host, 176
- 容器, 121
- 主机文件系统访问, 179-180
- 主机网络访问, 178
- `STORAGE_REDIRECT` 变量 (`docker-registry` 文件), 45
- IPC 访问, 179
- 打开权限, 177
- 使用准备, 180
- Storage 标签页 (Cockpit), 197
- SPCs (超特权)。查看 SPCs (超特权)
- `atomic` 命令, 180-185
- 运行日志 (`rsyslog`), 187-188
- 运行 `rhel-tools`, 186-187
- 运行系统监控 (`sade`), 189-191
- SUSE, 配置, 28
- `systemctl` 命令, 38
- systemd 服务，添加到 CentOS Dockerfile, 256-257
- System 标签页 (Cockpit), 194

# 索引

- 安装, 19
- 设置 Docker 注册表, 40–42
- 卸载参数（原子命令）, 181
- 安装 SPC 镜像, 185
- 合并文件系统, 249
- 恢复容器运行, 115-116
- 可更新的镜像, 158
- 更新参数（原子命令）, 181
- 更新 SPC 镜像, 184
- 用户名，附加到镜像, 83-85
- Chrome Dockerfile, 263-266
- Firefox Dockerfile, 267-269
- MySQL Dockerfile, 260-263
- WordPress Dockerfile, 258-266
- vimfile, 27
- 虚拟机 (VMs), 5
- 卷 (volumes)
  - 数据卷容器, 123-124
  - 宿主机, 122-123

## W-Z

- 等待退出代码，容器, 116
- Web 服务器，容器化，运行, 59-61
- Windows, 17
  - 配置, 28
- WordPress Dockerfile，查看, 258-260
- `wordpress` 镜像, 90-91
- 写保护绑定挂载, 124-125
- `yum filter` 命令, 251

## V

- 变量
  - `ADD_REGISTRY`, 47
  - 在 Dockerfile 中赋值, 166
- 可验证的镜像, 158
- 版本名称，镜像, 79
- 版本号，镜像, 79
- 查看
  - Busybox Dockerfile, 257-258
  - CentOS Dockerfile, 254-257

# Docker 容器

作为内容更新计划（Content Update Program）的一部分，以下是获取免费版 Docker Containers Web 版的说明：

如果您是从 informit.com 购买的书籍，可以在您的账户页的“数字购买”（Digital Purchases）标签页下找到免费的 Web 版。

如果您是在 InformIT 以外的零售商购买的书籍或尚未注册您的副本，请按照以下步骤操作：

1. 前往 `informit.com/register`。
2. 登录或创建新账户。
3. 输入 ISBN：`9780134136561`。
4. 回答问题作为购买证明。
5. 点击账户页上的“数字购买”（Digital Purchases）标签页以访问您的免费 Web 版。

# 更多关于内容更新计划……

随着 Docker 技术的演进，InformIT 将定期更新 Docker Containers Web 版。

注册用户将在每次 Docker Containers Web 版更新时收到一封电子邮件通知，告知更改。邮件提醒将发送至您用于 informit.com 账户的电子邮箱地址。

当书籍的新版本出版时，该书的 Web 版将不再添加进一步更新。但是，您将继续拥有访问带有后续更新的当前 Web 版。

Web 版可在使用现代移动浏览器的平板电脑上使用。只需登录您的 informit.com 账户，并从“数字购买”标签页访问 Web 版即可。

有关内容更新计划的更多信息，请访问 `informit.com/CUP` 或发送电子邮件至 `informit@custhelp.com` 联系我们的客户服务部门。
