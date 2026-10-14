
除了这些类型，还有 `auditlog` (审计日志), `boottarget` (启动目标), `eventlog` (事件日志), `firmware` (固件), `kit` (工具包), `kitcomponent` (包组件), `kitrepo` (包仓库), `monitoring` (监控), `notification` (通知), `osdistribupdate` (操作系统发行版更新), `policy` (策略), `rack` (机架) 和 `zone` (区域)。遗憾的是，并非所有项都有清晰的描述。例如你可以指定机架、固件或交换机，但似乎没有工具来管理它们。一个对象的描述可以在 xCAT 中分布在多个表中。xCAT 已经有许多更多表类型，其中一些可以存储不同对象类型的数据。例如 `domain`、`hosts`、`hypervisor`（虚拟机管理器）、`ipmi`、`mac`、`nodelist`、`nodetype`、`scripts`。所有表可以通过 `tabdump` 命令获取。如果添加 `-d` 参数，将获得相同的列表。默认情况下，xCAT 命令只能由超级用户执行。xCAT 支持共享和远程管理，即你可以在服务节点上安装 xCAT 服务器。重要的是，远程服务器上的 `/etc/passwd` 与 xCAT 服务器匹配。用户名将是 `xadmin`。在 xCAT 服务器上执行证书生成：

```
/opt/xcat/share/xcat/scripts/setup-local.sh xadmin
```

以下文件将出现在 `~xadmin/.xcat`：`ca.pem`、`cert.pem`、`key.pem` 和 `req.pem`。如果我们想执行远程管理，将它们复制到远程服务器的相同目录。此外，必须在远程服务器设置环境变量 `XCATSERVER=localhost`。现在允许 `xadmin` 执行命令。要做到这一点，使用 `tabedit` 编辑 `policy` 表：

```
#priority,name,commands,parameters,comments
"1",

2
",allow
```

我们允许 `xadmin` 从任何远程服务器执行命令。如果指定的不是 `*`，则任何命令都将不受允许。你可以指定更复杂的限制，如下：

```
mkdef -t policy -o name=xadmin commands=stat parameters=h02-h05
```

允许 `h02-h05` 执行 `stat` 命令。这意味着 `h01` 不能执行 `stat`。注意表中的 key 是执行优先级。这是一个数值参数，可以是 `6.1`。策略按升序排序；触发第一个匹配规则。

## 节点管理

让我们向集群添加第一个节点。xCAT 中的节点有三种类型：`stateful`（安装在硬盘上）、`stateless`（通过网络加载并在 RAM 中运行）和 `satellite`（通过 NFS 加载并在 RAM 中存储）。最常用的变是 `stateful`（服务节点）和 `satellite`（计算节点）。

首先，我们需要获取软件包和文件来创建镜像。为了实现这一点，我们需要所需发行版的 iso 镜像。xCAT 支持 Redhat、Ubuntu、SLES 和 Windows，但注意并非所有版本都得到官方支持。RHEL 7.6 的示例：

```
copys RHEL-7.6-20181010.0-Server-x8664-dvd.iso
```

引导节点：默认将创建 `install`、`netboot` 和 `satellite` 镜像。如果在生成期间未明确指定，镜像将是 `rhel76-x8664-satellite-compute`。

为 "compute" 组的节点添加描述：

```
chtab node=compute \
nodesf.netboot=pxe
nodesf.tftpserver=10.0.0.102
nodesf.nfserver=10.0.0.1
nodesf.installnic=eth0 nodesf.primarynic=eth0
htab node=compute \
nodetype.os=rhel76
nodetype.arch=x86_64 nodetype.profile=compute
nodetype.nodetype=osi=
htab key=system \
passwd.username=root
passwd.password=cluster
htab netname=main_vlan
networks.dynamicrange="10.0.0.200-10.0.0.254"
```

现在任何添加到 `compute` 组的节点将获得指定的参数。让我们添加节点描述：

```
mkdef -t node1 groups=all,compute arch=x86_64 \
bmc=node1ipmi bmcusername=ADMIN bmcpassword=admin
mac=XX:XX:XX:XX:XX mgt=ipmi netboot=pxe \
provmethod=rhel76-x8664-satellite-compute
```

为了避免每次编写节点的 IP 地址，可以使用模板机制。执行命令：

```
htab node=compute hosts.ip='\(d+)|10.0.0.(10+\$1)|'.
```

通过这种方式我们将 `compute` 组中每个节点的 IP 地址 设置为 `10.0.0.X`，其中 X 是通过节点号加 10 得到的。因此 `node15` 将获得地址 `10.0.0.25`。

让我们检查节点的节点的参数：

```
lsdef node1
Object name: node1
arch=x86_64
bmc=10.1.1.3
bmcpassword=admin
bmcusername=ADMIN
groups=all,compute
mac=00:10:30:30:40:03
```

## 第 26 章 集群管理系统 – XCAT 及其他系统

`mgt=ipmi`

`netbook=pxe`

`postbootscripts=otherpkgs`

`postscripts=syslog,remoteshell,syncfiles`

`provmethod=rhel76-x86_64-statelite-compute`

让我们来看看镜像的特征：

```
lsdef -t osimage rhel76-x86_64-statelite-compute
Object name: rhel76-x86_64-statelite-compute
imagetype=linux
osarch=x86_64
osname=Linux
osvers=rhel76
otherpkgdir=/install/post/otherpkgs/rhel76/x86_64
authorization=755
pkgdir=/install/rhel76_x86_64
pkglist=/opt/xcat/share/xcat/netboot/compute.rhel7.pkglist
profile=compute
provmethod=statelite
rootimgdir=/install/netboot/rhel76/x86_64-compute
```

`pkglist` 参数——此文件指定了镜像的包列表。该列表相当精简，如果你需要额外的包，可以进行扩展。最好的方法是创建一个新的配置，例如通过将 `compute.rhel7.pkglist` 复制到 `myprofile.rhel7.pkglist`。模板也应该以相同的方式复制。

如果你想添加未包含在发行版中的包（或未通过 `polycds` 命令从磁盘复制的包），你应该将它们拷贝到 `/install/post/otherpkgs` 目录，并在文件 `/install/custom/install/centos/compute.rhel7.otherpkgs.pkglist` 中列出它们的名称。

要更改其他镜像参数，例如磁盘分区（如果有），我们将使用模板。默认镜像创建模板位于 `/opt/xcat/share/xcat/centos/compute.rhel7.tmpl` 文件（或对应发行版的类似文件）。将其复制到 `/install/custom/install/centos` 目录并进行编辑。同样，你可以创建一个新模板，例如为服务节点创建一个。文件名必须与模板匹配，例如，服务模板的名称将为 `service.rhel7.tmpl`。现在你可以重新生成镜像，但强烈建议使用命令删除旧镜像：

```
rm -Rf /install/netboot/rhel76/x86_64/compute/
```

对于 `satellite` 版本的镜像，在（重新）生成后，执行命令 `liteimg rhel76-x86_64-satellite-compute`。

此命令在卫星模式后修改镜像。它不能用于无状态模式。
