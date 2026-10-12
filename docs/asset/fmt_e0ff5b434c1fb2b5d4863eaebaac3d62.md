
```
+ - usr/lib/amanda/sendbackup-gnutar
- usr/lib/amanda/sendsize
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/amanda-client-2.3.0-6.i386
Binary Packaging: amanda-server-2.3.0-6
Finding dependencies...
Requires (2): libc.so.5 libdb.so.2
usr/doc/amanda-server-2.3.0-6
usr/doc/amanda-server-2.3.0-6/COPYRIGHT
usr/doc/amanda-server-2.3.0-6/INSTALL
...
+ - usr/sbin/amrestore
- usr/sbin/amtape
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/amanda-server-2.3.0-6.i386
```

## 302 真实世界的软件包构建

...
Source Packaging: amanda-2.3.0-6
amanda-2.3.0.spec
amanda-2.3.0-linux.patch
amanda-rpm-instructions.tar.gz
amanda-2.3.0.tar.gz
393 blocks
Generating signature: 0
Wrote: `/usr/src/redhat/SRPMS/amanda-2.3.0-6.src.rpm`
#

如果我们快速看一眼客户端和服务器子包，我们会发现它们确确包含了文件：

```
# cd /usr/src/redhat/RPMS/i386/

# ls -l amanda-*

-rw-r-- 1 root 211409 Nov 21 15:56 amanda-client-2.3.0-1.i386.rpm

-rw-r-- 1 root 521814 Nov 21 15:57 amanda-server-2.3.0-1.i386.rpm

# rpm -qil amanda-*
```

| Name | amanda-client | Distribution: (none) |
| Version | 2.3.0 | Vendor: (none) |
| Release | 1 | Build Date: Thu Nov 21 15:55:59 1996 |
| Install date: (none) | Build Host: moocow.rpm.org |
| Group | System/Backup | Source RPM: amanda-2.3.0-1.src.rpm |
| Size | 737101 |
| Summary | Client-side Amanda package |

Description:
Amanda 网络包包含了跨网络执行自动备份所需的软件。Amanda 由两个包组成——客户端（此包）和服务器：

客户端包允许具有网络能力的系统由运行 amanda 服务器的系统进行文件系统备份。

注意：为了让系统执行其自身的备份，请同时安装客户端和服务器包！

```
/usr/doc/amanda-client-2.3.0-1

/usr/doc/amanda-client-2.3.0-1/COPYRIGHT

/usr/doc/amanda-client-2.3.0-1/INSTALL

...

usr/lib/amanda/sendbackup-gnutar

usr/lib/amanda/sendsize
```

## 304 在不同系统上安装软件包 真实世界的软件包构建

## 在不同系统上安装软件包

看起来我们快完成了。让我们在另一个没有运行过 amanda 的系统上安装软件包，并在那里进行测试：

```
# rpm -ivh amanda-#1.i386.rpm

amanda-client ############################################

amanda-server #################################

#
```

安装过程非常顺利。然而，测试并不顺利。为什么？什么都没有配置！服务器配置文件、客户端的 inetd.conf，所有内容都缺失了。如果我们停下来思考一下，这很合理：我们在构建系统上执行了所有步骤，但这些步骤中没有没有是可以被打包成文件的。

按照安装说明中的步骤操作后，一切都正常运行。虽然我们可以预期用户完成大部分与 amanda 配置相关的繁琐工作，但 RPM 确实具有在安装和删除软件包时运行脚本的能力。我们为什么不利用这个特性来让用户过得更轻松呢？

## 20.4.3 收尾工作

在流程的这一阶段，我们进入了冲刺阶段。软件已正确构建并打包。现在是时候停止从“构建软件”的角度来看问题，而是开始从“打包软件”的角度来看待问题了。

区别在于从用户的角度来看软件包。软件包安装是否方便？还是说需要花费大量精力才能使其运行？当软件包被删除时，它是会清理现场，还是会在文件系统中到处留下残留的碎片？

让我们在这个规格文件（spec file）上多花一点精力，让用户的生活变得更轻松。

## 创建安装脚本

当需要安装后配置时，amanda 绝不是好对付的！我们先处理客户端。让我们看看我们编写的脚本部分，对其进行注释，然后继续：

`%post client`

```
# 检查他们之前是否安装过 amanda...

# 如果安装过，那么这些内容都不应该是必须的...

if [ "$1" = 1 ];

then
```

## 20.4 软件包构建

首先，我们用 `%post` 语句开始脚本，并指定该脚本是用于客户端子包。正如注释所示，我们只在这是第一次安装客户端子包时才执行以下任务。为了实现这一点，我们使用了传递给脚本的第一个也是唯一的的参数。它是一个数字，表示在当前安装完成后将安装多少个该软件包的实例。

如果参数等于 1，意味着目前没有安装其他客户端子包实例，而这一个是第一个。让我们继续：

- # 设置磁盘设备以便 bin 可以读取它们
# (这实际上是在 Red Hat Linux 上完成的；只需要将 bin 添加到
# disk 组

```
if grep "disk::.*bin" /etc/group > /dev/null

then

  true
```

- # 如果 disk 组中有任何成员，在逗号后添加 bin，
`sed -e 's/disk::[0-9]\{1,\}/\1,\/\1,bin/' /etc/group > /etc/group.tmp`

- # 如果 disk 组中没有成员，添加 bin。
`sed -e 's/disk::[0-9]\{1,\}/\1,bin/' /etc/group.tmp > /etc/group`

```
# 清理！

rm -f /etc/group.tmp
```

amanda 的要求之一是，在客户端上运行备份的用户需要能够从每个磁盘设备读取。Red Hat 的人员通过创建一个组并赋予该组对每个磁盘的读写权限，为我们完成了一半工作。由于我们的备份用户是 bin，我们只需要将 bin 添加到组中。

下一部分与上一部分相关。它重点关注让 bin 在执行备份时访问所有内容：

- # 同时设置组可写 /etc/dump

```
chgrp disk /etc/dump

chmod g+w
```
Amanda 使用 dump 来备份备份，由于 dump 在 `/etc/dump` 中跟踪备份， bin 该文件的读写权限是理所当然的。在完美的世界里，`/etc/dump` 应该设置为允许组读写，但我们必须手动执行。不过这不是大问题。接下来，我们需要创建适当的网络相关条目，以便 amanda 客户端与 amanda 服务器通信，反之亦然：

- # 在 /etc/services 中添加 amanda 行

```
if grep "amanda" /etc/services > /dev/null

then

    true

else

    echo "amanda 1080/udp # Added by package amanda"
```

通过 grep 查找以 amanda 开头的行，我们可以轻松查看 `/etc/services` 是否已经配置好。如果没有，我们简单地在末尾添加一行。我们还为系统管理员添加了注释，让他们知道这个条目的来源，或者让他们通过 `rpm -q amanda-client` 命令自行查看。我们将所有操作写在一行是为了使脚本更简单。让我们看看脚本中其余关于网络的部分：

- # 在 /etc/inetd.conf 中添加 amanda 行

```
if grep "amanda" /etc/inetd.conf > /dev/null

then

    true

else

    echo "amanda udp # Added by package amanda-client" >>/etc/inetd.conf
```
