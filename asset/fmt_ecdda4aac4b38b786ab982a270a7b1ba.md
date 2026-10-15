
```bash
#!/bin/bash

# 生成 vmdk 的简单脚本

# 用法：./create_mdk.sh <image>

# 版权 security.com

if [ $# -ne 1 ]; then

  echo "Usage: ./create_mdk.sh <image>"

  exit 1

fi

FILENAME=$1

LOOPDEVICE=""

HEADS=""

CYLINDERS=""

TOTALSEORS=""

# 扫描回环设备

for i in `seq 0 9`; do

  losetup /dev/loop$i 2>/dev/null

  if [ $? -eq 0 ]; then

    LOOPDEVICE=/dev/loop$i

    break

  fi

done

if [ "$LOOPDEVICE" = "" ]; then

  echo "没有回环设备"

  exit 1

fi

# 读取几何结构

TOTALSEORS=$(fdisk -l $LOOPDEVICE 2>/dev/null | awk '{print $1}')

TRACKSEORS=$(fdisk -l $LOOPDEVICE 2>/dev/null | awk '{print $2}')

CYLINDERS=$(fdisk -l $LOOPDEVICE 2>/dev/null | awk '{print $3}')

HEADS=$(fdisk -l $LOOPDEVICE 2>/dev/null | awk '{print $4}')

# 检查值

if [ "$TOTALSEORS" -eq 0 ]; then

  echo "无法设置虚拟机"

  exit 1

fi

if [ "$TRACKSEORS" -eq 0 ]; then

  echo "扇区值无效"

  exit 1

fi

if [ "$CYLINDERS" -eq 0 ]; then

  echo "柱区值无效"

  exit 1

fi

if [ "$HEADS" -eq 0 ]; then

  echo "头数值无效"

  exit 1

fi

# 构建 vmdk

echo "正在写入 $FILENAME.mdk..."

cat << VMDK_EOF > $FILENAME.mdk

#磁盘描述符

version=1

CID=7680558

parentCID=ffffffff

parentID=ffffffff

createType="monolithicFlat"

# 范围描述

RW $TOTALSEORS FLAT "$FILENAME" 0

#磁盘数据

#DDB

ddb.adapterType = "ide"

ddb.geometry.sectors = "$TRACKSEORS"

ddb.geometry.heads = "$HEADS"

ddb.geometry.cylinders = "$CYLINDERS"

ddb.virtualHWVersion = "4"

ddb.toolsVersion = "0"

VMDK_EOF

echo "完成!"

```

虚拟机是检查受损系统、测试新工具或在无风险的情况下检查网络数据的完美环境。

# 离线分析（案例 4）

当你检查受损网络时，检查所有可能的日志数据可能是很有用的，以便寻找奇怪的记录、关联不同来源的日志、检查可疑活动等。

| 清单 | 说明 |
|---|---|
| 检查镜像分区表。 | 使用回环设备：`losetup /dev/[firstloopdevice] [image_file]` |

# 附录 B：Linux 取证与数据恢复

| 检查清单 | 说明 |
|--- | :--- |
| 使用 `fdisk`, `sfdisk` 或 `parted` 查看分区表结构。 | 记得检查镜像以查看扇区中的结果。 |
| 以只读模式挂载镜像。 | `Mount -o ro,nodev,user,noexec,notime,of_fset=[first_partition_cylinder*512] [image.file][mount_point]` |

## 电子证据的处理

有时，仅仅从机器上获取取证证据是不够的。如果证据需要在法律事务中使用，那么你必须对获取这些定罪证据的方式极其谨慎，而不仅仅是关注能否获取它们。这就是拥有电子证据的含义。

电子证据是一种工具，它正逐渐成为我们生活的一部分，并在诉讼中变得日益重要。可以肯定，传统证据正在从支持性文件向虚拟环境迁移，其管理流程和可采性标准较于传统证据发生了变化。

我们假设电子证据是证明利用新技术实施犯罪的适当介质，并将其定义为从电子设备或数字介质中获得的、用于证明行为真实性的任何信息。由于这一程序性工具的重要性，在法庭审查电子证据的可采性是打击技术犯罪的基本手段。

## 立法法规

电子证据的使用已成为解决使用电子设备实施犯罪的必要要素。法律依据涵盖了电子证据的应用到法律体系中存在的、类比适用法规的解释性原则，这些原则允许你利用法律规定来规范特定情况或立法空白。由于缺乏针对此类证据的特定规范，这些法规的类比适用原则在分析关于电子证据材料的立法时具有非常特殊的关联性。这一解释性概念为呈现此类证据的案件提供了法律解决方案。

## 电子证据的定义

不同的法律文本中没有对电子证据进行直接且明确的引用，也没有特定的排他性定义。然而，一些规定包含了以某种方式引用电子证据的条款。没有任何国家在其法律法典中规定电子证据的特定定义。在所有立法中，对传统证据的引用或或具体，涵盖了部分属于电子证据的内容。

## 传统证据与电子证据的等效性

法律表明电子证据等同于传统证据。它将电子证据视为与传统证据相同，更具体地说，属于文件证据。在考虑电子证据的监管时，文件证据的监管发挥着重要作用。

## 电子证据的优缺点

你可以从不同的角度解读使用电子证据带来的优点和不便。这在涉及“可靠性”时表现。一些人认为，电子证据的客观性和精确性使其更加可靠，因此倾向于使用它；另一些人则认为，缺乏验证电子证据真实性的手段使其更加脆弱，因此比传统证据更不可靠，认为其使用起来不便并影响了其可采性。

电子证据的优点之一是由于其来自电子元件，其信息是准确、清晰、精确、真实、客观且中立的，电子元件中存在的任何内容，与例如随时可能被反驳的证人证言相比。此外，电子证据提供了直到目前无法获取的信息，正如电子设备中所包含的内容那样。

另一个优点是此类证据由于其包含的信息具有完备性、可靠性和可行性。电子证据被认为是解决某些犯罪至关重要的，因为它是唯一的表现证明，事实非常有用。收集和使用电子证据既快速又简单，存储它们并不复杂。

由于对数据处理程序以及在这方面对诉讼法的解释缺乏了解，许多人认为确定此类证据的法律价值是困难的。这种困难源于缺乏适当且系统的监管，以及缺乏统一的司法判例。人们对这种证据的脆弱性和易被操纵性存在普遍的恐惧，考虑到其高度的易失性，这是证明其真实性的缺点之一。一些人认为法官和检察官不理解技术证据，而且很难解释。出于这种感觉，一些人拒绝在法庭上使用它。另一个缺点是保存电子证据的困难，以及关于如何正确存储以进行妥善保存的信息非常匮乏。

遇到的其他缺点涉及缺乏法律支持和认证模型：在法庭上接受电子证据似乎更困难，因为法官对电子证据要求的保证比对传统证据更多。欧洲一些司法机构表现出的理解缺失对于正在开发的任务是不便利的。此外，获取和解释由电子设备提供的信息以便转换为电子证据的过程被认为是耗耗时的，导致了高昂的成本并阻碍了其使用。

## 处理电子证据

程序标准并不包含任何监管在法庭上收集、保护或出电子证据的特定程序。通常情况下，各国在传统证据的通用程序中采用“类比”方法。

许多适用于可以类比应用于电子证据的程序。计算机取证领域的警察和私立专家没有在法庭上获取、保护或呈现电子证据的特定程序。从法律实践的角度来看，存在监管刑事和民事案件中证据保护的通用程序标准，这些标准可以通过类比扩展到电子证据。目前尚未建立用于保护或保存电子证据的程序，每个国家将通过类比解释为传统证据（即在大多数情况下为文件证据和证言证据）所立的准则，来在在法庭上保护这些证据。

## 电子证据在法庭上被采纳必须满足的要求

证据的合法性是一项基本要求，另一个是对基本权利的尊重，其中你经常可以发现关于保护个人数据和工人权利的引用。证据的可靠性、其关联性，以及在特定时刻是最佳证据，是法官在考虑特定证据可采性时的其他基本要求。

立法中决定电子证据是否可采的其它要求包括使用性、比例性和有效性。有效性被理解为证明指控的能力。其他法律规定尽可能使用原件而非复件。

# 附录 C

![](img/b9b072aa44ff9fed4a4e158d0420d424_603_0.png)

如果你使用的是 BSD 发版而不是 Linux 会怎样？本附录将概述伯克利软件发行版（BSD）操作系统家族中的安全特性。我们将首先概述主要的 BSD 项目以及安全功能是如何集成到所有 BSD 中的。接下，我们将介绍针对特定 BSD 的特定安全增强功能。最后，我们将为您提供一些用于获取更多信息的资源。

## BSD 项目概览

BSD 与 Linux 的相似之处在于它是开源的且类 UNIX 的。然而，它的某些差异使其在安全环境中使用极具吸引力。与 Linux 通过发行版将内核开发与用户态分离不同，每个 BSD 项目都提供了一个由开发工程团队控制的完全集成的操作系统。每个项目都拥有自己的第三方应用程序集合，并监控操作系统和软件集合的每日构建（nightly builds）。这种紧凑的集成使得更容易发现和修复软件不兼容问题，降低了升级破坏依赖关系或对生产系统产生负面影响的可能性。此外，对安全漏洞进行测试和发布补丁也更加容易。

每个 BSD 操作系统的源代码均受宽松的 BSD 许可证保护，该许可允许开源和商业开发项目自由地修改和分发。这在安全环境中是一个优势，因为在这些环境中可能不希望公开代码修改；由于这个原因，BSD 被应用于许多安全设备中。

尽管 BSD 代码出现在数百个操作系统和产品中，但三个主要的 BSD 项目是：

- NetBSD，成立于 1993 年 3 月（http://www.netbsd.org）
- FreeBSD，成立于 1993 年 6 月（http://www.freebsd.org）
- OpenBSD，成立于 1995 年 10 月（http://www.openbsd.org）

过去几年中，还出现了 DragonFly BSD（http://www.dragonflybsd.org），它是 FreeBSD 的一个分支；以及两个专注于桌面级支持的、基于 FreeBSD 的项目：DesktopBSD（http://www.desktopbsd.org）和 PC-BSD（http://www.pcbsd.org）。

> 本章将重点介绍 FreeBSD、OpenBSD 和 NetBSD 项目。

如图 C-1 所示示例所示，每个 BSD 项目都提供 cvs 接口，便于浏览和检索代码。每个代码库都可以追溯到项目存在的第一天，任何人都可以浏览任何代码的完整历史。这些 Web 仓库的地址如下：

- **NetBSD** http://www.netbsd.org/bsdweb.cgi/
- **FreeBSD** http://www.freebsd.org/cgi/cvsweb.cgi/
- **OpenBSD** http://www.openbsd.org/cgi-bin/cvsweb/

## 所有 BSD 中包含的安全特性

安全从底层开始，从操作系统的安装开始。BSD 安装哲学的一个示例体现在某个 OpenBSD 的安全目标中：提供一个“默认安全”（secure by default）的安装，让新手用户不需要在夜之间成为安全专家。FreeBSD、NetBSD 和 OpenBSD 提供的每个安装都提供了可安装的“组集”（sets）选择，使得安装一个精简但功能完备的操作系统变得简单。在安全领域，少即是多，因为你无法利用不存在的东西。这意味着，安装极少的内容并根据需要添加功能，比进行大型安装后再删掉不需要的功能要好。安装完成后，所有 BSD 都提供了下述的安全特性。

### securelevel (安全级别)

BSD 内核提供了多个安全级别，为管理员调整操作系统以满足特定环境的安全需求提供了起点。关于每个 BSD 的 securelevels 及其影响的影响可以在 `init`(8) 中找到。随着 securelevels 的增加，内核将阻止执行某些操作，例如：

- 加载或卸载内核模块
- 取消文件标志
- 卸载文件系统
- 修改防火墙规则
- 降低安全级别

需要注意的是，securelevels 提供的保护可以被任何具有单用户模式（single-user mode）访问权限的人绕过。这就是为什么在创建安全环境时，物理安全系统是一个重要组成部分的原因。

### 安全脚本 (Security Scripts)

每个 BSD 都会安装一套每天运行的安全脚本并将结果通过电子邮件发送给超级用户。这些脚本会检查可能的安全违规，包括：

- 检查密码数据库是否存在空密码以及 UID 或 GID 为 0 的情况
- 检查 .hosts 的变化
- 检查 SUID 和 SGID 权限的变化

关于这些检查的详情可以在 NetBSD 的 `security.conf`(5)、OpenBSD 的 `security`(8) 以及 FreeBSD 的 `periodic.conf`(5) 中找到。

### sysctl(8)

传统上，Linux 使用 `/proc` 伪文件系统来跟踪内核状态或系统当前发生的情况。`/proc`提供了开放进程和内核状态的深度见解，但没有提供直接与内核交互的机制。BSD 系统现在使用 `sysctl`(8) 机制动态查看和修改内核状态。

`sysctl`(8) 使用 MIB 来描述可见和可修改的参数。要查看所有可用 MIB，使用 `sysctl -a`：

```
sysctl -a | grep ip
sysctl -a | grep tcp
sysctl -a | grep udp
sysctl -a | grep icmp
sysctl -a | grep arp
```

以下是一些增加安全性的 sysctl 更改示例：

- 修改头部中的 TTL 值以防止指纹识别：
  `sysctl -w net.inet.ttl=255`
- 强制使用随机 ID 以防止信息收集：
  `sysctl -w net.inet.random_id=1`
- 禁用 ICMP 重定向：
  `sysctl -w net.inet.icmp.drop=1`
- 禁用定向广播：
  `sysctl -w net.inet.ip.directed_broadcast=0`
- 禁用源路由（源路由允许攻击者访问内部系统）：
  `sysctl -w net.inet.ip.allowsrcoute=0`

### 安全脚本 (Security Scripts)

在 FreeBSD 系统上可以使用 blackhole (4) 提供某些针对隐性的防护：

```
sysctl -w net.inet.tcp.blackhole=2
sysctl -w net.inet.udp.blackhole=2
```

在 FreeBSD 中，网络 MIB 随种协议描述，例如 tcp(4) 和 icmp(4)。

### rc.conf

BSD 系统不使用运行级别（runlevels）或包含脚本的子目录结构。相反，使用单个配置文件 `/etc/rc.conf` 来决定启动时运行的服务。此外，该文件包含了启动时实施的安全设置。其中一些包括：

- 清空 /tmp
- 禁止在 motd（登录信息）中显示操作系统
- 设置安全级别
- 加载防火墙规则集

可用配置设置随 BSD 而异，详情请见 FreeBSD 和 NetBSD 的 rc.conf(5) 以及 OpenBSD 的 rc.conf(8)。

### rc.subr(8)

在 NetBSD 和 FreeBSD 中，rc(8) 原生支持运行 chroot(8)；它会自动设置监狱环境，包括创建一个 /var/run/log 套接字，使 syslog(8) 能够正常工作。rc.subr(8) 进一步描述了 user_group_groups 和 chroot 变量。

这是一个在没有 chroot 能力的情况下通过 rc(8) 框架以权限运行的自定义持久脚本示例：

## 附录 C: BSD

```
start_precmd-ircd_hybrid_precmd
ircd_hybrid_precmd () {
  /usr/bin/touch $pidfile /usr/sbin/chown $irc $pidfile 600 $pidfile
# 在没有 chroot 的情况下，group 和 groups 派自 passwd 数据库。
# 在 chroot 的情况下，必须指定 _group 和 groups，或者保留 root 的组。
  : ${user}-irc
  : ${group}-irc
  : ${groups}-irc
  rc_flags="foreground $rc_flags"
}
```

```bash
/etc/rc.sub
load_rc_config name
run_rc_command "$1"
```

要调用此 rc 脚本，请在 `/etc/rc.conf` 中添加以下行：
```conf
irchybrid-chroot="usr/local/ircd/"
irchybrid-user="irc"
hybrid-groups="irc"
irchybrid-id="YES"
hybrid-flags="--configfile /usr/local/ircd/ircd.conf
```

### chflags(1)

`chflags`(1) 是 Linux `chattr`(1) 命令的 BSD 等效命令。文件标志（属性）为 UNIX 文件的读、写、执行权限提供了扩展。它们可用于防止即使是超级用户（root）修改或删除敏感文件。

例如，设置 `schg`（系统更改/不可变）标记可以帮助防止操作系统二进制文件被删除或修改，从而帮助防范 rootkit：

```bash
chflags schg -R /bin /sbin /usr/bin /usr/sbin
```
