
注意

除非加载了 `mac_seeotherids(4)` 策略，否则用户可以看到 root 标签的进程。

## 16.5.6. MAC 多级安全模块 (The MAC Multi-Level Security Module)

模块名称：`mac_mls.ko`

内核配置行：`options MAC_MLS`

启动选项：`mac_mls_load="YES"`

`mac_mls(4)` 策略通过强制执行严格的信息流策略来控制系统中主体（subjects）和对象（objects）之间的访问。

在 MLS 环境中，每个主体或对象的标签中都设置了“许可”（clearance）级别以及“安全部门”（compartments）。由于这些许可级别达到了数千个，要彻底配置每个主体或对象将是一项艰巨的任务。为了减轻这种管理开销，该策略包含了三个标签：`mls/low`、`mls/equal` 和 `mls/high`，其中：

- 标记为 `mls/low` 的任何内容都具有低许可级别，不允许访问更高级别的信息。该标签还防止较高许可级别的对象向较低级别写入或传递信息。

- `mls/equal` 应该放置在免于该策略的对象上。

- `mls/high` 是可能的最高许可级别。分配此标签的对象将对系统中所有其他对象具有支配地位；然而，它们不会允许向较低类的对象泄露信息。

MLS 提供：

- 带有一组非分级类别的分级安全级别。
- 固定“不向上读、不向下写”（no read up, no write down）规则。这意味着主体可以对其同级或以下的对象具有读取权限，但不能高于。同样，主体对同级或以上的对象具有写入权限，但不能低于它们。
- 机密性，或防止数据被不当泄露。
- 系统设计的基础，用于并发处理多个敏感级别的数据，而不会在机密和秘密数据之间泄露信息。

以下是可用 `sysctl` 可调项：

- `security.mac.mls.enabled` 用于启用或禁用 MLS 策略。

- `security.mac.mls.pty_equal` 在创建期间将所有 `pty(4)` 设备标记为 `mls/equal`。

- `security.mac.mls.revocation_enabled` 在对象标签更改为较低等级的标签后撤销对其的访问。

- `security.mac.mls.max_compartments` 设置系统允许的最大部门级别级数。

## 第 16 章 强制访问控制 (Mandatory Access Control)

使用 `setfmac(8)` 来操作 MLS 标签。为对象分配标签：

```
# setfmac mls/5 test
```

获取文件 `test` 的 MLS 标签：

```
# getfmac test
```

另一种方法是在 `/etc/` 中创建一个主策略文件，其中指定 MLS 策略信息，并将该文件传递给 `setfmac`。

当使用 MLS 策略模块时，管理员计划控制敏感信息的流。默认的“向上读、向下写”（read up write down）将所有内容设置为低状态。所有内容都是可访问的，管理员逐渐增加信息的机密性。

除了三个基本的标签选项外，管理员根据需要对用户和组进行分组，以阻止它们之间的信息流。使用描述性词汇来查看许可级别中的信息可能会更容易，例如机密（Confidential）、秘密（Secret）和绝密（Top Secret）的分类。某些管理员则根据项目级别创建不同的组。无论分类方法如何，在实施限制性策略之前，必须有一个深思熟虑的计划。

MLS 策略模块的一些示例场景包括电子商务服务器、持有公司关键信息的文件服务器以及金融机构环境。

## 16.5.7. MAC Biba 模块 (The MAC Biba Module)

模块名称：`mac_biba.ko`

内核配置行：`options MAC_BIBA`

启动选项：`mac_biba_load="YES"`

`mac_biba(4)` 模块加载 MAC Biba 策略。该策略与 MLS 策略类似，但流规则略相反。这是为了防止信息的向下流动。在 MLS 环境中，每个主体或对象上都设置了“完整性”（integrity）标签。这些标签由分级等级和非分级组件组成。随着等级上升，其完整性也提高。支持的标签有 `biba/low`、`biba/equal` 和 `biba/high`，其中：

- `biba/low` 被认为是对象或主体可以的最低完整性。在对象或主体上设置 `biba/high` 将不允许读取访问。

- `biba/equal` 应该放置在认为免于该策略的对象上。

- `biba/high` 允许向较低对象写入，但不允许读取对象。建议将此标签放在影响整个系统完整性的对象上。

Biba 提供：

- 带有一组非分级类别的分级完整级别。
- 固定“向上写、不向下读”（write up, no read down）规则。主体对同级或以下的对象具有写入权限，但不能高于。同样，主体对同级或以上的对象具有读取权限，但不能低于它们。
- 通过防止数据的不当修改确保完整性。
- 完整性级别而非敏感性级别。

## MAC 低水位模块

以下可调项用于操作 Biba 策略：

- `security.mac.biba.enabled` 用于启用或禁用目标机器上 Biba 策略的执行。

- `security.mac.biba.pty_equal` 禁用 `pty(4)` 设备上的 Biba 策略。

- `security.mac.biba.revocation_enabled` 在标签支配主体时强制撤销对对象的访问。

要访问系统对象的 Biba 策略设置，请使用 `setfmac` 和 `getfmac`：

```
# setfmac biba/low test
```

```
# getfmac test
```
test: biba/low
```

完整性与敏感性不同，用于保证信息不被不受信的方操纵。这包括主体和对象之间传递的信息。它确保用户仅能够修改或访问被授予权限的信息。

在初始规划阶段，管理员必须准备好将用户划分等级、级别和区域。一旦启用此策略模块，系统将默认设置为高标签，由管理员为用户配置不同的等级和级别。

可能包含某些主题。例如，所有开发者对源代码仓库、源代码编译器和其他开发实用程序具有修改访问权限。其他用户将被归入其他类别，如测试人员、设计人员或终端用户，他们仅被允许读取访问。

低完整性主体无法向高完整性主体写入数据，且高完整性主体无法列出或读取低完整性对象。在最低等级上设置标签可以使主体无法访问。该安全策略模块的某些预期环境包括受限的 Web 服务器、开发和测试机以及源代码仓库。用性较小的实现可能是个人工作站、作为路由器的机器或网络防火墙。

## 16.5.8. MAC 低水位（Low-watermark）模块

模块名称：`mac_lomac.ko`

内核配置行：`options MAC_LOMAC`

启动选项：`mac_lomac_load="YES"`

与 MAC Biba 策略不同，`mac_lomac(4)` 策略允许在降低完整性以防破坏任何完整性规则后，允许对低完整性对象的访问。

低水位（Low-watermark）完整性策略的工作方式与 Biba 几乎相同，例外是使用浮动标签通过辅助等级分区（auxiliary grade compartment）支持主体降级。此辅助分区的形式为 `[grade]`。在分配带有辅助等级的策略时，使用语法 `lomac/10[2]`，其中 `2` 是辅助等级。

该策略依赖于所有系统对象无处不在的完整性标签，允许主体从低完整性对象读取数据，然后降低主体的标签，以防止未来使用 `[grade]` 向高完整性对象写入数据。该策略可能比 Biba 提供更好的兼容性，且需要的初始配置更少。

与 Biba 和 MLS 策略一样，使用 `setmac` 和 `setpmac` 用于在系统对象上设置标签：

```
# setmac /usr/home/trhodes lomac/high[low]
```

```
# getfmac /usr/home/trhodes lomac/high[low]
```

第 16 章 强制性访问控制

辅助等级 `low` 是仅由 MAC LOMAC 策略提供的功能。

## 16.6. 用户锁定（User Lock Down）

此示例考虑了一个用户少于五十人的较小型存储系统。用户将具有登录能力，并允许存储数据和访问资源。

对于这种场景，`mac_bsdextended(4)` 和 `mac_seeotherids(4)` 策略模块可以共存，并在隐藏用户进程的同时阻止访问系统对象。

首先向 `/boot/loader.conf` 中添加以下行：

`mac_seeothertherids_load="YES"`

通过向 `/etc/rc.conf` 中添加此行可以激活 `[mac_bsdextended(4)]` 安全策略模块：`ugidfw_enable="YES"`。

存储在 `/etc/rc.bsdextended` 中的默认规则将在系统初始化时加载。然而，默认条目可能需要修改。由于该机器预计仅为用户服务，除了最后两行外，所有内容都可以保持注释状态，以便强制默认加载用户拥有的系统对象。

将所需的用户添加到此机器上并重启。为了测试目的，请尝试在两个控制台上以不同用户的身份登录。运行 `ps aux` 查看其他用户的进程是否可见。验证在另一个用户的家目录下运行 `[ls(1)]` 是否失败。

除非已修改特定的 `sysctls` 以阻止超级用户访问，否则不要尝试使用 root 用户进行测试。

注意

当添加新用户时，他们的 `[mac_bsdextended(4)]` 规则将不在规则列表中。要快速更新规则集，使用 `kldunload(8)` 和 `kldload(8)` 卸载并重新加载安全策略模块。jail。

## 16.7. MAC Jail 中的 Nagios

本节演示了在 MAC 环境中实现 Nagios 网络监控系统所需的步骤。这作为一个示例，管理员仍需在生产环境之前测试所实施的策略是否符合网络的安全要求。

此示例要求在每个系统上设置 `multilabel`。它还假设在尝试集成到 MAC 框架之前，`net-mgmt/nagios-plugins`、`net-mgmt/nagios.` 和 `www.apache2` 均安装、配置并正常运行。

### 16.7.1. 创建不安全用户类

通过向 `/etc/login.conf` 添加以下用户类开始程序：

```
insecure:\
:copyright=/etc/COPYRIGHT:\
:welcome=/etc/motd:\n
:setenv=MAIL=/var/mail/$,BLOCKSIZE=K:\n
:path=~/bin:sbin:/bin:usr/sbin:usr/bin:usr/local/sbin:usr/local/bin\n
:manpath=/usr/share/man /usr/man:\
Configure Users
:nologin=/usr/sbin/nologin:\
:cputime=1h30m:\
:datasize=8M:\
:vmemoryuse=100M:\
:stacksize=2M:\
:memorylocked=4M:\
:memoryuse=8M:\
:filesize=8M:\
:coredumpsize=8M:\
:openfiles=24:\
:maxproc=32:\
:priority=0:\
:requirehome:\
:passwordtime=91d:\
:umask=022:\n:ignoretime@:\
:label=biba/10(10-10):
```

然后，在默认用户类部分添加以下行：

`:label=biba/high:`

保存编辑并执行以下命令重建数据库：

```
# cap_mkdb /etc/login.conf
```

### 16.7.2. 配置用户

使用 `setmac` 将 root 用户设置为默认用户类：

```
# usermod -L default
```

非 root 账户现在需要登录类，否则用户将被拒绝执行命令。以下脚本可以解决问题：

```
# for x in awk -F: '($3 >= 1001) && ($3 != 65534) { print $1 }'\etc/passwd`; do pw usermod -L default; done
```

接下来将 nagios 和 www 账户放入 insecure 类：

```
# pw usermod nagios
```

```
# pw usermod www
```

### 16.7.3. 创建上下文文件（Contexts File）

现在应创建 `/etc/policy`。这是系统的默认 BIBA 策略。

```
# System:
/var/run/.* ?biba
/dev/.* ?biba
/var ?biba
/var/spool/.* ?biba
/var/log/.* ?biba
/var/tmp/.* ?biba
/tmp/.* ?biba
/var/spool/mqueue ?biba
```

接下来，在 `/etc/mac.conf` 的主部分添加这些编辑：

```
default_labels ifnet ?biba
default_labels process ?biba
default_labels socket ?biba
```

### 16.7.4. 加载配置

为了完成配置，向 `/boot/loader.conf` 中添加以下行：

`mac_biba_load="YES"`

`mac_seetheruidis_load="YES"`

`security.mac.biba.trust_all_interfaces=1`

并在在 `/etc/rc.conf` 的网络配置中添加以下行。如果主网络配置通过 DHCP 进行，可能每次启动都需要手动配置：

`maclabel`

### 16.7.5. 测试配置

首先，确保系统初始化时不会启动 Web 服务器和 Nagios。确保 root 无法访问 Nagios 配置目录中的任何文件。如果 root 可以列出 `/var/spool/nagios` 的内容，说明有问题。相反，应该返回“拒绝访问”错误。

如果一切正常，现在可以启动 Nagios、Apache 和 Sendmail：

```
# cd /etc/mail/&& make stop && \
setpbmac biba/equal make start && setpbmac biba/10-(10-10\) apachelt start && \
setpbmac biba/10\(10-10\)/usr/local/etc/rc.d/nagios.sh forstart
```

双检查以确保一切运行正常。如果不是，检查日志文件中的错误信息。如果需要，

使用 `sysctl(8)` 禁用 `mac_biba(4)` 安全策略模块，并尝试像通常一样重新启动一切。

注意

root 用户仍然可以安全强制执行并编辑其配置规则。以下命令将允许新生成的 shell 将安全策略降级到较低级别：

```
# setpmac biba/10 csh
```

325

MAC 框架故障排排除

为了防止这种情况发生，请使用 `login.conf(5)` 强制用户进入某个范围。如果 `setpmac(8)` 尝试运行超出隔间范围的命令，将返回错误且不会执行该命令。在这种情况下，将 root 设置为 `biba/high(high-high)`。

# # 16.8. MAC 框架故障排排除

本节讨论了常见的配置错误及其解决方法。

multilabel 未能在根 (/) 分区上保持启用：

以下步骤可能会解决此瞬态性错误：

- 1. 编辑 `/etc/fstab` 并将根分区设置为 `ro`（只读）。

- 2. 重启到单用户模式。

- 3. 在 `/` 上运行 `tunefs -l enable`。

- 4. 重启系统。

- 5. 执行 `mount -urw /` 将 `/etc/fstab` 中的 `ro` 改回 `rw` 并再次重启系统。

- 6. 再次检查 `mount` 的输出，以确保根文件系统上已正确设置 `multilabel`。

在使用 MAC 建立安全环境后，Xorg 不再启动：

这可能是由 MAC 分区策略或某个 MAC 标记策略中的标记错误导致的。

要进行调试，请尝试以下操作：

- 1. 检查错误信息。如果用户处于不安全类，则分区策略可能是魁祸首。

尝试将用户的类恢复为默认类，并使用 `cap_mkdb` 重新构建数据库。如果这没有缓解问题，请进入第二步。

- 2. 再次检查为用户、Xorg 和 `/dev` 条目设置的标签策略是否正确。

- 3. 如果这两种方法都解决问题，请将错误信息和环境描述发送到 FreeBSD 通用邮件列表。

出现 `_secure_path: unable to state .login_conf` 错误：

当用户尝试从 root 用户切换到系统中的另一个用户时，可能会出现此错误。此消息通常发生在用户的标签设置高于其尝试变成的用户时。例如，如果 joe 的默认标签为 `biba/low`，而 root 的标签为 `biba/high`，则 root 无法查看 joe 的家目录。无论 root 是否使用过 `su` 变成 joe，这种情况都会发生，因为 Biba 完整性模型不允许 root 查看设置为较低完整性级别的对象。

系统不再识别 root：

当发生这种情况时，`whoami` 返回 0，`su` 返回 `who are you?`。

这可能是由于标记策略被 `sysctl(8)` 禁用或策略模块被卸载导致的。如果策略被禁用，需要重新配置登录能力数据库。双检 `/etc/login.conf` 以确保所有标签选项都已移除，并使用 `cap_mkdb` 重新构建数据库。

如果策略限制了对 `master.passwd` 的访问，也会发生这种情况。这通常是由管理员在与系统使用的通用策略冲突的标签下修改了文件。在这种情况下，系统将读取用户信息，但由于文件继承了新标签，访问将被拦截。使用 `sysctl(8)` 禁用策略，一切都将恢复正常。

326

# 第 17 章 安全事件审计

作者：Tom Rhodes 和 Robert Watson。

# 17.1. 节要介绍
