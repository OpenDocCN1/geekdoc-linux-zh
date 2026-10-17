
类似的指令也可用于`/proc/sys`目录中文件相关的其他设置。查看`/proc/sys/net/ipv4`目录中的`icmp_*`指令。你们中有些人可能认识到，互联网控制消息协议（ICMP）最常与`ping`命令相关联。事实上，`ping`命令是对回显的请求。因此`icmp_echo_ignore_all`和`icmp_echo_ignore_broadcasts`与直接的`ping`命令以及与广播地址相关的`ping`命令有关。

换句话说，如果你将以下指令添加到`/etc/sysctl.conf`文件中：

```
net.ipv4.icmp_echo_ignore_all = 1
net.ipv4.icmp_echo_ignore_broadcasts = 1
```

本地系统将不会响应直接的`ping`命令，也不会响应`ping`向网络广播地址发出的请求。

### /etc/sysctl.conf 文件中的设置

`/etc/sysctl.conf`文件中的设置只是可以配置内容的一小部分。可以合理假设 RHEL 6 在该文件中包含这些选项是有原因的，并且这些设置最有可能在 RHCE 考试中涉及。你已经检查了 IPv4 转发的第一个指令。下一个指令如果处于活动状态，则可确保从外部网络传入的数据包确实来自外部：

```
net.ipv4.conf.default.rp_filter = 1
```

以下指令通常处于禁用状态，以防止外部网络上的黑客通过第三方路由数据。这种路由是攻击中常见的策略，因为它可以帮助掩盖攻击者的身份。

```
net.ipv4.conf.default.accept_source_route = 0
```

也称为内核 magic sysrq 键，开发人员可能出于开发目的启用此指令。通常，你应保留以下设置：

```
kernel.sysrq = 0
```

如果 Linux 内核崩溃，此选项会将 PID 号包含在内核转储文件中以帮助识别罪魁祸首：

```
kernel.core_uses_pid = 1
```

黑客用来使系统过载的另一种标准方法是 SYN 数据包泛滥。这类似于所谓的“死亡 ping”。以下设置对其使用进行监管：

```
net.ipv4.tcp_syncookies = 1
```

桥是交换机的旧称，它可以调节单个网络内的流量。以下指令会禁用在这些桥上使用所注明的`iptables`、`ip6tables`和`arptables`命令。

```
net.bridge.bridge-nf-call-iptables = 0
net.bridge.bridge-nf-call-ip6tables = 0
net.bridge.bridge-nf-call-arptables = 0
```

此类桥与物理主机系统上的虚拟化相关；它们不适用于基于 KVM 的虚拟机中。

## 练习 12-2

### 禁用对 ping 命令的响应

在本练习中，你将使用内核参数来禁用对`ping`命令的响应。虽然本练习可以在任意两个连接的系统上运行，但本练习假设你将配置`server1.example.com`系统并从`tester1.example.com`系统测试结果。

- 1. 在`server1.example.com`系统上，使用以下命令查看与`ping`消息响应相关的当前设置：
  
  ```
  # cat /proc/sys/net/ipv4/icmp_echo_ignore_all
  ```
- 2. 假设输出为`0`，尝试`ping localhost`命令。会发生什么？不要忘记按 CTRL-C 退出输出流。如果输出为`1`，请跳至步骤 5。
- 3. 从`tester1.example.com`等远程系统确认结果。在某些情况下，你可能无法物理访问该系统，因此请使用适当的`ssh`命令连接。从远程系统，尝试`ping server1.example.com`或`ping 192.168.122.50`命令。
- 4. 返回`server1.example.com`系统。使用以下命令更改步骤 1 中描述的内核设置：
  
  ```
  # echo "1" > /proc/sys/net/ipv4/icmp_echo_ignore_all
  ```
  
  确认方法为重复步骤 1 中的命令。再次尝试`ping localhost`命令。会发生什么？
- 5. 将`icmp_echo_ignore_all`选项恢复为原始的`0`设置。

## 认证目标 12.03

### 创建 RPM 包

如果你从未创建过 RPM，RHCE 目标“构建一个打包单个文件的简单 RPM”可能看起来是一个巨大的挑战。在一些相对较新的工具的帮助下，这比看起来容易。

虽然考试期间你无法访问互联网，但你可以下载源 RPM 来帮助备考。源 RPM 安装后会设置子目录结构。位置取决于用户。如果源 RPM 由用户`michael`安装（是的，普通用户现在可以加载源代码），则源 RPM 子目录可以在`/home/michael/rpmbuild`目录中找到。

> 在生产环境中，以 root 管理用户身份安装和编译源 RPM 存在风险。源 RPM 中的错误很容易危及生产系统。

从源 RPM（SRPM）解压的源代码可以作为你将创建的源代码的模型。RHEL 6 现在提供了工具来帮助设置 spec 文件。然后可以使用该 spec 文件构建实际的二进制 RPM，以便其他人将其用于在自己的系统上安装单个文件。

### 源 RPM

在 Red Hat 系统上，当 GNU 通用公共许可证（GPL）提及源代码时，它指的是源 RPM。事实上，Red Hat 部分通过在其公共服务器`ftp.redhat.com`上发布源 RPM 来遵守此类开源许可证。源代码包括由开发人员创建的程序和文件。然后可以将源代码构建为用于安装 RHEL 6 以及安装完成后额外软件的二进制包。

在本节中，你将下载并安装与 vsFTP 服务器关联的源代码 RPM。一种方法是使用第 2 章中描述的`lftp`命令。要使用该命令连接到 Red Hat FTP 服务器，请运行以下命令：

```
$ lftp ftp.redhat.com
```

该命令匿名连接到 Red Hat 公共 FTP 服务器并启动`lftp ftp.redhat.com>`提示符。要连接到包含 RHEL 6 服务器源代码包的目录，请从所述提示符运行以下命令：

```
lftp ftp.redhat.com> cd /redhat/linux/enterprise/6Server/en/os/SRPMS
```

在`lftp`提示符下，命令补全功能可用；换句话说，如果你在输入`cd`命令后不确定有哪些目录可用，只需按一次或两次 TAB 键即可。

在所述目录中，你可以使用以下命令下载 vsFTP 服务器的源代码（版本号会随更新而变化）：

```
get vsftpd-2.2.2-6.el6.src.rpm
```

然后你可以运行`quit`命令退出`lftp`提示符并返回到常规命令行界面。源代码 SRPM 现在应该可用

在本地目录中。即使作为普通用户，你也可以使用`rpm`命令解包该 SRPM。例如，以下从我的普通账户运行的命令将源代码解包到`/home/michael/rpmbuild`子目录中：

```
$ rpm -ivh vsftpd-*.src.rpm
```

命令不会安装 vsFTP 服务器，就像使用常规 RPM 包那样。它将 SRPM 解包到特定的子目录中。

## RPM 源的目录结构

SRPMs 安装时会被解包。此类软件包的源代码会被加载到`rpmbuild/SPECS`和`rpmbuild/SOURCES`子目录中。顾名思义，源代码位于`SOURCES`子目录中。图 12-1 说明了从 vsFTP 源代码解包的文件列表。

所列目录中的大部分文件都是补丁，即源代码的更新。一些文件是配置文件，将由二进制包加载到`/etc/vsftpd`目录中。实际的源代码被压缩在 gzip 压缩的 tar 归档中，格式为`.tar.gz`。请注意版本号包含在源-

![](img/9139201cfcaf4292284a0eed074928e5_686_0.png)

![](img/9139201cfcaf4292284a0eed074928e5_687_0.png)

代码归档中。此类归档可以使用`tar`命令的帮助创建和解包。

## 源代码也可以使用 bzip2 算法进行压缩。

要创建 RPM，你需要在同一个`rpmbuild/SOURCES`子目录中设置类似的归档。配置完成后，你还必须创建一个`.spec`文件，存储在`rpmbuild/SPECS`子目录中。然后你就可以使用`rpmbuild`命令编译该软件包。

## 安装并分析 rpmbuild 命令

`rpmbuild`命令用于根据`.spec`文件配置的源代码构建二进制 RPM。由于该命令默认不可用，你必须从`rpm-build`软件包安装它。你还应该安装`rpmdevtools`软件包，稍后会很有用。为了加快进程，使用管理权限使用`yum`命令安装所有这些软件包更为高效，使用第 7 章中描述的程序。

```
