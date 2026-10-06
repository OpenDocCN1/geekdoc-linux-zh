
Docs: `man.usbguard-daemon(8)`

Main PID: 6122 (`usbguard-daemon`)

Tasks: 3 (limit: 11493)

Memory: 1.2M

CGroup: `system.slice/usbguard.service`

`--6122 /usr/bin/usbguard-daemon -f -s /etc/usbguard/usbguard-daemon.conf`

Nov 07 09:44:06 localhost.local `systemd[1]`: Starting USBguard daemon...

Nov 07 09:44:07 localhost.local `systemd[1]`: Started USBguard daemon.

- 列出由 `USBGuard` 识别的 USB 设备：

```
# usbguard list-devices
allow: id 1d6b:0002 serial "0000:02:00:00" name "xHCI Host Controller" hash...
```

## 更多资源

- `usbguard(1)` 和 `usbguard-daemon.conf(5)` 手页

# 12.3. 使用 CLI 阻塞和授权 USB 设备

本过程概述了如何使用 `usbguard` 命令授权和阻塞 USB 设备。

### 前提条件

- `usbguard` 服务已安装并运行。

### 步骤

- 列出由 `USBGuard` 识别的 USB 设备：

```
# usbguard list-devices
allow: id 1d6b:0002 serial "0000:02:06.7" name "EHCI Host Controller"
"JD00bBiktys2ct3mSqKopnOVV2hMGYADWt+ouIF22=" parent-hash
"4PHGcaDWKPtKdYwpIRG722cB9iG9f9ea93+Gt9c=" via-port "usb1" with-interface
09:00:00
block: 6: id 1ab1:0000024937962" name "Voyager"
"CrXiaWlf2ZU5+WckOE7yORSO82Mzbun7Hdb95Q=" parent-hash
"JD00bBiktys2ct3mSqKopnOVV2hMGYADWt+ouIF22=" via-port "1-3" with-interface
08:06:50
```

2. 授权设备 6 与系统交互：

```
# usbguard allow-device 6
```

3. 撤销授权并移除设备 6：

```
# usbguard reject-device 6
```

4. 撤销授权并保留设备 6：

```
# usbguard block-device 6
```

### 注意

`USBGuard` 使用 `block`（阻塞）和 `reject`（拒绝）术语，具有以下含义：

- *block*：暂时不要与此设备交互。
- *reject*：忽略此设备，就像它不存在一样。

## 更多资源

- *列出 `usbguard` 命令的所有选项：*

```
$ usbguard --help
```

- `usbguard(1)` 手页

# 12.4. 为 USB 设备创建自定义策略

以下过程包含为 USB 设备创建规则集的步骤，以反映您应用场景的需求。

### 前提条件

- *`usbguard` 服务已安装并运行。*
- */etc/usbguard/rules.conf* 文件包含一个由 `usbguard generate-policy` 命令生成的初始规则集。

### 步骤

- 1. 创建一个授权当前连接的 USB 设备的策略，并将生成的规则存储到 `rules.conf` 文件中：

```
# usbguard generate-policy --no-hashes > ./rules.conf
```

`--no-hashes` 选项不会为设备生成哈希属性。在配置设置中避免使用哈希属性，因为它们不是持久的。

- 2. 使用您喜欢的文本编辑器编辑 `rules.conf` 文件，例如：

```
# vi ./rules.conf
```

### Red Hat Enterprise Linux 8 安全加固

- 3. 根据需要添加、删除或编辑规则。例如，以下规则仅允许具有单一大容量接口的设备与系统交互：

```
allow with-interface equals ( 08::* )
```

请参阅 `usbguard-conf(5)` 手页获取详细的规则语言描述和更多示例。

- 4. 安装更新后的策略：

```
# install -m 0600 -o root -g root /etc/usbguard/rules.conf
```

- 5. 重启 `usbguard` 以应用新策略：

```
# systemctl restart usbguard
```

### 验证步骤

- 1. 检查激活的策略，例如：

```
# usbguard list-rules
4: allow with-interface 08::*
```

## 更多资源

- `rules.conf(5)` 手

# 12.5. 授权用户和组使用 IPC 接口

本过程用于授权特定用户或组使用 USBGuard 接口。默认情况下，只有 root 用户可以使用此接口。

### 前提条件

- `usbguard` 服务已安装并运行。
- */etc/usbguard/rules.conf* 文件包含一个由 `generate-policy` 命令生成的初始规则集。

### 步骤

- 1. 使用您喜欢的编辑器编辑 */etc/usbguard/usbguard-daemon.conf* 文件：

```
# vi /etc/usbguard/usbguard-daemon.conf
```

- 2. 例如，添加一行允许 `wheel` 组的所有用户使用接口，并保存文件：

```
IPCAllowGroups=wheel
```

3. 使用 `usbguard` 命令添加用户或组。例如，以下命令允许 `josec` 用户完全访问设备、策略列表和异常部分：

```
# usbguard add-user joesec --devices ALL --policy list,listen --exceptions ALL
```

要移除 `josec` 用户的权限，请使用 `usbguard remove-user` 命令。

4. 重启 `usbguard` 守护进程以应用更改：

```
# systemctl restart usbguard
```

## 更多资源

- `usbguard(1)` 和 `rules.conf(5)` 页

# 12.6. 将 USBGuard 授权事件记录到 Linux 审计日志

使用以下步骤将 USBGuard 授权事件集成到标准的 Linux 审计日志。默认情况下，`usbguard` 守护进程将事件记录到 */var/log/usbguard/usbguard-audit.log* 文件。

### 前提条件

- `usbguard` 服务已安装并运行。
- `auditd` 服务正在运行。

### 步骤

- 1. 使用您喜欢的文本编辑器编辑 `usbguard-daemon.conf` 文件：

```
# vi /etc/usbguard/usbguard-daemon.conf
```

- 2. 将 `AuditBackend` 从 `FileAudit` 为 `LinuxAudit`：

```
AuditBackend=LinuxAudit
```

- 3. 重启 `usbguard` 守护进程以应用配置更改：

```
# systemctl restart usbguard
```

### 验证步骤

- 1. 查询审计守护日志以获取 USB 授权事件，例如：

```
# ausearch -ts recent -m USER_DEVICE
```

## 更多资源

- `usbguard-daemon.conf(5)` 手页

# 12.7. 更多资源

- `usbguard(1)`, `rules.conf(5)`, `usbguard-daemon.conf(8)` 和 `usbguard-daemon.conf(5)` 页

- USBGuard 主页
