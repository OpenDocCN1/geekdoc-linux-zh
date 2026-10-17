
```bash
~]# aide --check
AIDE 0.15.1 found differences between database and filesystem!!
Start timestamp: 2017-03-30 14:12:56

Summary:
    Total number of files: 147173
    Added files:   1
    Removed files: 0
    Changed files: 2
    ...
```

至少，`AIDE`应配置为每周运行一次扫描。最多，`AIDE`应每天运行一次。例如，要使用`cron`安排`AIDE`在凌晨4:05执行（参见系统管理员指南中的*自动化系统任务*章节），请向`/etc/crontab`添加以下行：

```
05 4 * * * root /usr/sbin/aide --check
```

### 4.11.3. 更新 AIDE 数据库

在验证系统变更（如软件包更新或配置文件调整）后，更新您的基线`AIDE`数据库：

```
~]# aide --update
```

`aide --update`命令创建`/var/lib/aide/aide.db.new.gz`数据库文件。要开始将其用于完整性检查，请从文件名中移除`.new`子字符串。

### 4.11.4. 额外资源

有关`AIDE`的更多信息，请参见以下文档：

- `aide(1)`手册页
- `aide.conf(5)`手册页
- Red Hat Enterprise Linux 7 安全配置指南（OpenSCAP 安全指南）：使用`AIDE`验证完整性
- `AIDE`手册

## 4.12. 使用 USBGUARD

`USBGuard`软件框架通过实施基于设备属性的基本白名单和黑名单功能，提供针对侵入式 USB 设备的系统保护。为了执行用户定义的策略，`USBGuard`使用 Linux 内核的 USB 设备授权功能。`USBGuard`框架提供以下组件：

- 守护程序组件，具有进程间通信 (`IPC`) 接口，用于动态交互和策略执行。
- 与运行中的`USBGuard`实例交互的命令行界面。
- 用于编写 USB 设备授权策略的规则语言。
- 用于与守护程序组件（实现为共享库）交互的 C++ API。

### 4.12.1. 安装 USBGuard

要安装`usbguard`软件包，请以`root`身份输入以下命令：

```
~]# yum install usbguard
```

要创建初始规则集，请以`root`身份输入以下命令：

```
~]# usbguard generate-policy > /etc/usbguard/rules.conf
```

> **注意**
>
> 要自定义`USBGuard`规则集，请编辑`/etc/usbguard/rules.conf`文件。有关更多信息，请参见`usbguard-rules.conf(5)`手册页。此外，请参见第 4.12.3 节，“*使用规则语言创建自己的策略*”中的示例。

要启动`USBGuard`守护程序，请以`root`身份输入以下命令：

```bash
~]# systemctl start usbguard.service
~]# systemctl status usbguard
- usbguard.service - USBguard daemon
    Loaded: loaded (/usr/lib/systemd/system/usbguard.service; disabled;
                vendor preset: disabled)
    Active: active (running) since Tue 2017-06-06 13:29:31 CEST; 9s ago
      Docs: man:usbguard-daemon(8)
  Main PID: 4984 (usbguard-daemon)
   CGroup: /system.slice/usbguard.service
           └4984 /usr/sbin/usbguard-daemon -k -c /etc/usbguard/usbguard-daem...
```

要确保`USBGuard`在系统启动时自动启动，请以`root`身份使用以下命令：

```bash
~]# systemctl enable usbguard.service
Created symlink from
/etc/systemd/system/basic.target.wants/usbguard.service to
/usr/lib/systemd/system/usbguard.service.
```

要列出`USBGuard`识别的所有 USB 设备，请以`root`身份输入以下命令：

```bash
~]# usbguard list-devices
1: allow id 1d6b:0002 serial "0000:00:06.7" name "EHCI Host Controller"
    hash "JD0b9BiktYs2ct3mSQkopnOOV2h9MGYADwhT+0utF2s=" parent-hash
    "4PHGcaDKwtPjKDoYpIRG722cB9Lsigz91Iea93+Gt9c=" via-port "usb1" with-interface 09:00:00
...
6: block id 1b1c:1ab1 serial "000024937962" name "Voyager" hash
    "CrXgiaWIF2bZAU+5WkzOE7y0rdSO82XMzmb7HDv95Q=" parent-hash
    "JD0b9BiktYs2ct3mSQkopnOOV2h9MGYADwhT+0utF2s=" via-port "1-3" with-interface 08:06:50
```

要授权设备与系统交互，请使用`allow-device`选项：

```
~]# usbguard allow-device 6
```

要取消授权并移除系统中的一个设备，请使用`reject-device`选项。如果仅取消授权设备，请使用`block-device`选项的`usbguard`命令：

```
~]# usbguard block-device 6
```

`USBGuard`使用*block*和*reject*术语，含义如下：

- block - 暂时不与此设备通信
- reject - 忽略此设备，仿佛它不存在一样

要查看`usbguard`命令的所有选项，请输入带有`--help`指令：

```
$ usbguard --help
```

### 4.12.2. 创建白名单和黑名单

`usbguard-daemon.conf`文件由`usbguard`守护程序在解析其命令行选项后加载，并用于配置守护程序的运行时参数。要覆盖默认配置文件（`/etc/usbguard/usbguard-daemon.conf`），请使用`-c`命令行选项。有关更多细节，请参见`usbguard-daemon(8)`手册页。

要创建白名单或黑名单，请编辑`usbguard-daemon.conf`文件并使用以下选项：

- `RuleFile`=`<path>`
    - `usbguard`守护程序使用此文件从中加载策略规则集，并写入通过`IPC`接口接收到的新规则。
- `IPCAllowedUsers`=`<username>` [`<username>` ...]
    - 守护程序将接受`IPC`连接的用户名列表，以空格分隔。
- `IPCAllowedGroups`=`<groupname>` [`<groupname>` ...]
    - 守护程序将接受`IPC`连接的组名列表，以空格分隔。
- `IPCAccessControlFiles`=`<path>`
    - 持有`IPC`访问控制文件的目录路径。
- `ImplicitPolicyTarget`=`<target>`
    - 如何处理不符合策略中任何规则的设备。可接受的值：`allow`, `block`, `reject`。
- `PresentDevicePolicy`=`<policy>`
    - 当守护程序启动时，如何处理已经连接的设备：
        - `allow` - 授权每个现有设备
        - `block` - 取消授权每个现有设备
        - `reject` - 移除每个现有设备
        - `keep` - 仅同步内部状态并保持现状
        - `apply-policy` - 对每个现有设备评估规则集
