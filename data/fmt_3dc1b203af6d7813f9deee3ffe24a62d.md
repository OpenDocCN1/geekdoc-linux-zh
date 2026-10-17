
## 25.2.4 Jail 类型

### Basejails

Basejails 在每次启动时重新克隆其基础文件系统。它们非常适合需要在多个 jail 上同时进行修补或升级的环境。

### 模板

模板只是一个将 `template` 属性设置为“yes”的 jail。

将 jail 转换为模板：

```
# iocage set template=yes UUID|TAG
```

执行此操作后，该 jail 可以通过以下命令列出：

```
# iocage list -t
```

从此模板部署 jail：

```
# iocage clone TEMPLATE_UUID tag=mynewjail
```

模板可以通过设置 `template` 属性相互转换。

### 空

空 jail 适用于不受支持的 jail 设置或测试。

创建空 jail：

```
# iocage create -e
```

它们非常适合用于实验不受支持的发行版或 LINUX jail。

## 25.2.5 最佳实践

以下是使用 `iocage` 管理的 jail 的一些通用指南。

- 使用 PF（PF 包过滤防火墙）作为模块：这是通用内核中的默认设置。
- 始终为你的 jail 和模板使用易于识别的标签！

  这将帮助你避免错误并轻松识别 jail。

- 设置 `notes` 属性：将 `notes` 属性设置为有意义的内容，特别是对于你可能只偶尔使用的模板和 jail。
- 检查你的防火墙规则：当在 VNET jail 内使用 IP 或 Internet 协议防火墙（IPFW）时，在 `/etc/rc.conf` 开头放入 `firewall_enable="YES" firewall_type="open"`。这样你可以排除防火墙的阻止。测试完一切后，再将其锁定。如果同时使用两者，也请检查主机上的 PF 防火墙规则。
- 清除旧快照：删除不需要的快照，特别是数据变化很大的 jail！
- 使用 `chroot` 子命令：如果需要访问或修改处于停止状态的模板或 jail 中的文件，请使用：

  ```
  # iocage chroot UUID | TAG
  ```

  这样，你无需启动 jail 或转换模板。

## 25.2.6 高级用法

### 克隆

当 jail 被克隆时，`iocage` 会创建一个 ZFS 克隆文件系统。克隆是廉价的轻量级快照。

克隆依赖于其源快照和文件系统。如果你希望销毁源 jail 并保留其克隆，则需要先提升克隆，否则无法销毁源 jail。

创建克隆：按如下方式将 `myjail` 克隆为 `myjail2`：

```
# iocage clone myjail tag=myjail2
```

从现有快照克隆 jail：

```
# iocage clone myjail@snapshotname tag=myjail3
```

提升克隆：要提升克隆的 jail：

```
# iocage promote UUID | TAG
```

此步骤将反转克隆和源 jail 的关系。基本上，克隆将成为源，而源 jail 将被降级为克隆。

然后，你可以使用以下命令删除被降级的 jail：

```
# iocage destroy UUID | TAG
```

### 更新 jail

更新使用 `freebsd-update` 实用程序处理。Jail 可以在停止或运行状态下更新。

将 jail 更新到最新补丁级别：

```
# iocage update UUID | TAG
```

这将自动创建 jail 的回滚快照。  
当你完成更新并且 jail 正常工作后，只需删除快照：

```
# iocage snapremove UUID|TAG@snapshotname
```

如果更新破坏了 jail，只需回滚到快照即可：

```
# iocage rollback UUID|TAG@snapshotname
```

如果你希望在不影响 jail 的情况下测试更新，请创建一个克隆并以与前面概述相同的方式更新它。

克隆 jail：

```
# iocage clone UUID|TAG tag=testupdate
```

### 升级 jail

升级使用 `freebsd-update` 实用程序处理。默认情况下，`upgrade` 命令将尝试将 jail 升级到主机的发行版版本（`uname -r`）。

根据 jail `type` 属性，`basejails` 和非 `basejails` 的升级处理方式不同。

**升级非 basejail：** 要将普通 jail（非 basejail）升级到主机的发行版：

```
# iocage upgrade UUID | TAG
```

这将把 jail 升级到与主机相同的发行版。  
要升级到特定发行版：

```
# iocage upgrade UUID|TAG release=10.2-RELEASE
```

**升级 basejail：** 要升级 basejail，首先验证 jail 是否为 basejail：

```
# iocage get type UUID|TAG
```

此命令应返回 `type` "basejail"。  
升级可以在 jail 在线时强制执行，方法如下：

```
# iocage upgrade UUID|TAG
```

这将在 jail 运行期间强制重新克隆 basejail 文件系统（无停机时间）并使用新发行版的更改更新 jail。

```
# iocage set release=10.1-RELEASE UUID|TAG
```

这将在下次 jail 启动时导致 jail 从 10.1 发行版重新克隆其文件系统。  
这不会使用下一个发行版的更改更新 jail 的文件！

### Autoboot

确保在 `/etc/rc.conf` 中设置了 `iocage_enable="YES"`。

要使 jail 在启动时自动启动：

```
# iocage set boot=on UUID|TAG
```

启动优先级：可以通过设置优先级值来指定启动顺序：

```
# iocage set priority=20 UUID|TAG
```

值越低表示启动优先级越高。

### 快照管理

`iocage` 原生支持透明的 ZFS 快照管理。快照是数据的时点副本；是 jail 可以随时恢复到的安全点。最初，快照几乎不占用空间，因为只记录数据的变化。

列出 jail 的快照：

```
# iocage snaplist UUID|TAG
```

创建新快照，运行：

```
# iocage snapshot UUID|TAG
```

这将基于当前时间创建快照。

创建自定义命名的快照，运行：

```
# iocage snapshot UUID|TAG@mysnapshotname
```

**应用限制：** 动态应用限制：

```
# iocage cap UUID | TAG
```

**检查限制：** 检查活动限制：

```
# iocage limits UUID | TAG
```

**按百分比限制中央处理器 CPU 使用：** 将 CPU 执行限制为 20%：

```
# iocage set pcpu=20:deny UUID|TAG iocage cap UUID|TAG
```

检查限制：

```
# iocage limits UUID | TAG
```

**重置 jail 的属性：** `iocage reset` 命令会重置 jail 属性。要重置为默认值：

```
# iocage reset UUID | TAG
```

你也可以将所有 jail 重置为默认属性：

```
# iocage reset ALL
```

重置 jail 会保留 jail 的 `UUID` 和 `TAG`。其他所有内容都将丢失。请确保设置所需的任何自定义属性。

**自动安装软件包：** 软件包可以在 jail 创建时自动安装。在创建时指定 `pkglist` 属性，它应指向一个文本文件，每行包含一个软件包名称。请注意，为此工作你需要有互联网连接。`pkg install` 将尝试从在线仓库获取软件包。

使用你喜欢的文本编辑器创建一个 `pkgs.txt` 文件并添加软件包名称。

```
pkgs.txt:

nginx
```

现在只需创建 jail 并提供 `pkgs.txt` 文件：

```
# iocage create pkglist=/path-to/pkgs.txt tag=myjail
```
