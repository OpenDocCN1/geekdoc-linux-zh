
### 如何操作...

这五个简单的步骤将引导你完成权限提权：

- 1. 通过以下命令在`/etc/sudoers.d/`中创建一个新的`sudoers`定义文件：
  `# visudo -f /etc/sudoers.d/clustering`
- 2. 执行以下命令，为最常用的工具创建一个名为`CLUSTERING`的命令别名：
  `Cmnd_Alias CLUSTERING = /sbin/ccs, /sbin/clustat, /sbin/clusvcadm`
- 3. 现在，为所有集群`CLUSTERS`创建一个主机别名，如下：
  `Host_Alias CLUSTERS = cluster1, cluster2`
- 4. 接下来，执行以下命令为所有管理员`CLUSTERADMINS`创建用户别名：
  `User_Alias CLUSTERADMINS = spalatine, dvader, okenobi, qjinn`
- 5. 现在，让我们创建一个`sudo`规则，允许`CLUSTERADMINS`中的用户在`CLUSTERS`组内的所有服务器上执行`CLUSTERING`中的命令，如下：
  `CLUSTERADMINS CLUSTERS = (root) CLUSTERING`

### 更多功能...

要编辑`sudoers`文件，你可以使用文本编辑器编辑`/etc/sudoers`，或者使用`visudo`工具，它会在退出时自动检查你的语法。

一个好主意是保持原始`/etc/sudoers`文件不变，并修改位于`/etc/sudoers.d/`中的文件。这样在必要时，`sudo``rpm`就可以更新`sudoers`文件。

### 另另

有关关于`sudo`的更多信息，请参阅`sudoers (5)`手页。

# 使用 firewalld 保护网络

`firewalld`是一组脚本和守护进程，用于管理`RHEL`系统上的`netfilter`。它的目标是创建一个简单的命令行界面来管理你系统上的防火墙。

### 如何操作...

默认情况下，`firewalld`包含在`"core"``rpm`包中，但由于某些原因可能未安装（你在`kickstart`中漏掉它就是一个原因！）。执行以下步骤：

- 通过以下命令行安装`firewalld`：
  `# yum install -y firewalld`
- 现在，通过以下方式启用`firewalld`：
  `# systemctl enable firewalld`
- 最后，通过以下命令启动`firewalld`：
  `# systemctl start firewalld`

# 查看 firewalld 状态

通过以下命令列出所有已激活的服务：
`firewall-cmd --list-all`

通过以下命令查看所有允许的服务：
`firewall-cmd --list-services`

通过以下命令查看所有允许的端口：
`firewall-cmd --list-ports`

通过以下命令列出所有区域：
`firewall-cmd --list-zones`

通过以下命令查看默认区域：
`firewall-cmd --get-default-zone`

通过以下命令查看特定区域的配置：
`firewall-cmd --zone=public`

通过以下命令查看该区域允许的服务：
`firewall-cmd --zone=public --list-services`

# 配置服务

查看当前允许的服务列表：
`firewall-cmd --list-services`

要添加一个`HTTP`服务：
`firewall-cmd --zone=public --add-service=http`

要永久添加一个服务：
`firewall-cmd --zone=public --add-service=http --permanent`

要移除一个服务：
`firewall-cmd --zone=public --remove-service=http`

要永久移除一个服务：
`firewall-cmd --zone=public --remove-service=http --permanent`

要添加一个端口：
`firewall-cmd --zone=public --add-port=8080/tcp`

要永久添加一个端口：
`firewall-cmd --zone=public --add-port=8080/tcp --permanent`

要移除一个端口：
`firewall-cmd --zone=public --remove-port=8080/tcp`

要永久移除一个端口：
`firewall-cmd --zone=public --remove-port=8080/tcp --permanent`

# 配置端口

查看所有允许的端口：
`firewall-cmd --list-ports`

要添加一个端口：
`firewall-cmd --zone=public --add-port=8080/tcp`

要永久添加一个端口：
`firewall-cmd --zone=public --add-port=8080/tcp --permanent`

要移除一个端口：
`firewall-cmd --zone=public --remove-port=8080/tcp`

要永久移除一个端口：
`firewall-cmd --zone=public --remove-port=8080/tcp --permanent`

# 重新加载配置

在更改配置后重新加载防火墙：
`firewall-cmd --reload`

# 启动和停止服务

启动防火墙：
`systemctl start firewalld`

停止防火墙：
`systemctl stop firewalld`

启用自机启动：
`systemctl enable firewalld`

禁用自机启动：
`systemctl disable firewalld`

# 使用 kdump 和 SysRq

`kdump`是一种`Linux`内核机制，允许在内核崩溃时创建内存转储。

`SysRq`是`Linux`内核支持的一个功能，允许在系统无响应时发送组合键。

### 如何操作...

首先，我们将设置`kdump`和`SysRq`，随后我将向你如何使用它们进行调试。

# 安全 RHEL 7

安装并配置`kdump`和`SysRq`

让我们看看是如何安装的：

- 1. 执行以下命令安装`kdump`必要的包：
  `# yum install -y kexec-tools`
- 2. 确保`/etc/sysconfig/grub`文件中的`GRUB_CMDLINE_LINUX`变量中存在`crashkernel-auto`，使用以下命令：
  `GRUB_CMDLINE_LINUX="rd.lv.system=usr rd.lv.system=swap vconsole.keymap=us rd.lv.system=/root vconsole.font=latinyr crashkernel-auto"`
- 3. 运行以下命令启动`kdump`：
- 4. 现在，通过以下方式启用在开机时启动`kdump`：
- 5. 通过以下命令配置`SysRq`以接受所有命令：
  `# echo "kernel.sysrq = 1" >> /etc/sysctl.d/sysrq.conf`
  `# sysctl -q -p /etc/sysctl.d/sysrq.conf`
- 6. 执行以下命令重新生成`initramfs`（初始内存系统）以包含`kdump`所需的信息：
  `# dracut --force`
- 7. 最后，通过以下命令进行重启：

# 使用 kdump 工具分析转储

虽然你可以在`vmcore-dmesg.txt`文件找到大部分所需信息，但有时查看`vmcore`转储的位和字节是有用的，即使只是为了知道`Red Hat`的人员在你要求你发送`vmcore`转储时在做什么。

执行以下步骤：

- 1. 通过以下命令安装调试`vmcore`转储必要的工具：
  `# yum install -y --enablerepo=* crashkernel-debuginfo`
- 2. 执行以下命令定位你的`vmcore`：
  `# find /var/crash -name 'vmcore'`

# 第 9 章

如果你没有核心转储（`core dump`），可以通过执行以下命令来手动触发：

```bash
echo c > /proc/sysrq-trigger
```

3. 使用`crash`分析内容，如下：

`# crash /var/crash/127.0.0.1-2015.10.31-12:03:06/vmcore /usr/lib/debug/lib/modules/*/vmlinux`

在这里，`<kernel>`是为以下创建的内核：

```
crash 7.0.2-al17
```
