
6. 将你的代码添加到 `/home/user01/.bashrc` 的末尾。

7. 对。将你想添加到用户主目录的文件放在 `/etc/skel` 目录中。

8. 用户的主目录创建在 `/home/` 下。

9. 通过使用集中认证，你不需要在整个组织中创建或维护多个账户。

10. 你可以使用 `authconfig-tui` 命令或 `authconfig` 命令。

# 实验 7

# 任务 1 – 配置自定义

- 步骤 1。在 RHEL01 上创建一个包含以下信息的文件：

人力资源通知

所有员工接受随机抽检。

此致，

HR

- 步骤 2。将文件保存为 `hr_notice.txt`。

- 步骤 3。设置 `hr_notice.txt` 文件，使系统上创建的新用户在其主目录中收到此通知的副本。

当创建的用户主目录中有正确的文件时，任务完成。

# 任务 2 – 用户和组管理

步骤 1。在 RHEL01 上创建以下组：

- a. `sales`（销售）
- b. `engineering`（工程）
- c. `developers`（开发）

步骤 2。在 RHEL01 上创建一个新用户。满足以下要求：

- a. 用户名：`user01`
- b. 密码：`password`
- c. 主目录：`/home/user01`
- d. Shell：`BASH`
- e. 描述：普通用户
- f. UID：`500`
- g. GID：`500`
- h. `user01` 应该是 `sales` 组的成员

步骤 3。在 RHEL01 上创建一个新用户。满足以下要求：

- a. 用户名：`user02`
- b. 密码：`secret`
- c. 主目录：`/var/log`
- d. Shell：`BASH`
- e. 描述：审计员
- f. UID：`600`
- g. GID：`600`
- h. `user02` 应该是 `sales` 组的成员

步骤 4。在 RHEL01 上创建一个新用户。满足以下要求：

- a. 用户名：`user03`
- b. 密码：`supercool`
- c. 主目录：无
- d. Shell：无
- e. 描述：假假账户
- f. UID：`501`
- g. GID：`501`
- h. `user03` 应该是 `engineering` 组的成员

步骤 5。在 RHEL01 上创建一个新用户。满足以下要求：

- a. 用户名：`user04`
- b. 密码：`CheapThanFree`
- c. 主目录：`/home/user04`
- d. Shell：`Korn`
- e. 描述：开发者
- f. UID：`502`
- g. GID：`502`
- h. `user04` 应该是 `engineering` 组的成员

步骤 6。在 RHEL01 上创建一个新用户。满足以下要求：

- a. 用户名：`user05`
- b. 密码：`Security`
- c. 主目录：无
- d. Shell：无
- e. 描述：用户
- f. UID：`503`
- g. GID：`503`
- h. `user05` 应该是 `developers` 组的成员

# 任务 3 – 协作

步骤 1。在 `/opt` 创建以下组：

- a. `sales`
- b. `engineering`
- c. `developers`

步骤 2。在 `/opt` 设置以下权限：

- a. `770`
- b. `775`
- c. `775`

步骤 3。在 `/opt` 创建以下目录：

- a. `sales`
- b. `engineering`
- c. `developers`

步骤 4。将以下用户添加到相应的组中：

- a. `user01` 添加到 `sales`
- b. `user02` 添加到 `sales`
- c. `user03` 添加到 `engineering`
- d. `user04` 添加到 `engineering`
- e. `user05` 添加到 `developers`
- f. `user06` 添加到 `developers`

# 222 Red Hat® 考试实战指南：RHCSA® 和 RHCE® 认证指南与实验手册

第 3 步启动 Apache 服务：

```bash
# service httpd start
Starting httpd:
```

> 警告：你可能会收到关于 ServerName 未设置警告。现在忽略它即可。

第 4 步启用开机自启：

```bash
# chkconfig httpd on
```

第 5 步验证：

```bash
# chkconfig httpd -list
httpd      0:off  1:off  2:on  3:on  4:on  5:on
6:off
```

现在 HTTP 服务器已经在运行，你需要创建一个目录结构，用来存放你需要提供给客户端的文件。

第 6 步创建以下目录：

```bash
# mkdir /var/www/pub
```

`/var/www` 是 Apache 存储客户端可以访问的文件的默认位置。在该目录内，你创建一个“pub”目录，该目录实际上用于存放将安装在客户端上的 Red Hat CD 内容。

第 7 步，你应该确保 Red Hat CD 已挂载到光驱中：

```bash
# mount /dev/cd-rom /mnt
```

第 8 步，将文件从 CD 拷贝到之前创建的目录：

```bash
# cp -vR /mnt/* /var/www/pub/
```

这个过程需要一些时间，因为你正在复制整个 Red Hat CD 内容，它的很大。

第 9 步，当安装文件就绪后，你需要创建最后一个目录：

```bash
# mkdir /var/www/pub/kickstart
```

第 10 步，验证你现在的目录结构是否如下：

```text
# tree /var/www/pub
|-- BOOT
|   |-- BOOTX64.conf
|   |-- TRANS.TBL
|   -- splash.xpm.gz
|   -- TRANS.TBL
|-- EULA
|-- GPL
|-- HighAvailability
|-- LoadBalancer
|-- Packages
|-- README
|-- ResilientStorage
|-- ScalableFileSystem
|-- Server
|-- images
|   |-- README
|   |-- TRANS.TBL
|   |-- efiboot.img
|   |-- efdisk.img
|   |-- install.img
|   |-- product.img
|   |-- pxboot
|   |-- initrd.img
|   |-- vmlinuz
|-- isolinux
|   |-- boot.cat
|   |-- boot.msg
|   |-- grub.conf
|   |-- inittrd.img
|   |-- isolinux.bin
|   |-- isolinux.cfg
|   |-- memtest
|   |-- splash.jpg
|   |-- vesamenu.c32
|   |-- vmlinuz
|-- kickstart
|   |-- redhat-base.cfg
|-- media.repo
|-- repodata
```

**警告：**在使用 `tree` 命令之前，你可能需要安装它。取决于你在安装过程中安装了哪些包，`tree` 包可能已也可能未安装。

**警告：**如果你使用 `tree` 命令，你会得到一个巨大的文件列表，看起来与我的略有不同。我是手动创建的目录且没有显示文件，以展示目录结构的样子。你的 `tree` 结构应该充满了来自 Red Hat CD 的所有文件。

迁移提示

在 RHEL6 中，DVD 的布局完全不同，因此目录与 RHEL5 中的完全不同。

第 11 步。在此时，你通常会创建 kickstart 文件，但我们将在下一节中查看，现在只需创建一个占位符：

```bash
# touch /var/www/pub/kickstart/redhat-base.cfg
```

# 防火墙和 SELinux 配置

为了完成 kickstart 设置，你只需要对安全设置进行少量调整。由于我们还没有介绍 iptables 或防火墙规则，本节将向你现在需要的命令。我们将在第 12 章介绍防火墙规则。

你需要使用 TCP 端口 80 来让 HTTP 服务正常工作。使用 HTTP 协议进行 kickstart 的一个安全优势是，它只需要在...开放单个端口。

- 第 1 步。使用 `iptables` 命令创建你的防火墙规则：

```bash
# iptables -I INPUT 5 -p tcp -m tcp --dport 80 -j ACCEPT
```

- 第 2 步。保存你创建的规则：

```bash
# service iptables save
Saving firewall rules to /etc/sysconfig/iptables: [ OK ]
```

- 第 3 步。重启防火墙服务使更改生效：
