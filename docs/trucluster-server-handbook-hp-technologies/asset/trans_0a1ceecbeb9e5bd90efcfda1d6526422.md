

## 7.4.5 如何查看特定组件的所有信息？

```
# hwmgr -get attribute -id 46

46:
name = COMPAQ AlphaServer DS10 466 MHz
category = platform
memory_size_MB = 256
registration_time = Tue Mar 20 12:39:23 2001
user_name = (null) (settable)
location = (null) (settable)
software_module = (null)
state = available
state_previous = unknown
state_change_time = none
event_count = 0
last_event_time = none
```

## 7.4.6 如何仅查看某些组件的少量属性？

你可以通过指定 "-a attribute" 选项来查看最少一个属性。

```
# hwmgr -get attribute -a dev_base_name -id 59

59:
dev_base_name = dsk7
```

下面是一个显示多个属性的示例，其中包括搜索不包含特定值的属性。

```
# hwmgr get -a name -a dev_base_name -a power_mgmt_capable!=1

2:
name = CPU0
power_mgmt_capable = 0

30:
name = FDI-fdio-unit-0
dev_base_name = Floppy0
power_mgmt_capable = 0

45:
name = SCSI-WWID:0710002c::"COMPAQ   CRD-8402B" :d05b000:00000100000*
dev_base_name = cdrom0
power_mgmt_capable = 0
```

下面是一个类似的示例，我们在此搜索包含特定值的属性。我们还将搜索范围限制在 "disk" 类别。

```
# hwmgr -get -a -a dev_base_name -a cluster_disables=1 -cat disk
45:
dev_base_name = cdrom0
cluster_disables = 1
```

请注意，部分条件解析无法按预期工作。例如，HWID 为 40 的组件将 "COMPAQ" 列为制造商。

```
# hwmgr -get -a -a manufacturer -id 40
40:
manufacturer = COMPAQ
```

然而，当我们明确指定 "manufacturer!=COMPAQ" 时，得到的结果与预期相反。

```
# hwmgr -get -a -a manufacturer!=COMPAQ
40:
manufacturer = COMPAQ
...
```

如果我们查找 "manufacturer=COMPAQ"，则看不到任何输出。

```
# hwmgr -get -a -a manufacturer=COMPAQ
<no output>
```

我们认为这可能是字符串解析问题，但：

```
# hwmgr -get -a -a dev_base_name -a state=available -cat disk
30:
dev_base_name = floppy0
state = available
40:
dev_base_name = dsk0
state = available
...
```

这似乎是一个错误，我们已通知 COMPAQ 客户支持中心。

### 7.4.7 如何设置组件的“可设置”属性？

某些组件具有用户可设置的属性，如名称 (`user_name`) 或物理位置 (`phys_location`)。在大型配置中，能够为设备指定对你有意义的名称，例如“我的启动磁盘”或其位置，这非常有用。首先，让我们找到特定设备的“可设置”属性。

```
# hwmgr --get attr -id 46 | grep "(settable)"

user_name = (null) (settable)
location = (null) (settable)
```

这是什么设备？

```
# hwmgr --get attr -id 46 -a name

46:
  name = COMPAQ AlphaServer DS10 466 MHz
```

它是系统。好吧，让我们将“user_name”设置为系统的主机名。请注意，“user_name”属性目前限制为十五个字符。例如：

```
# hostname | wc -c

17
```

请注意，此系统的完全限定主机名为十六个字符（“wc -c”返回一个额外的字符，可能是换行符）。所以让我们尝试设置属性，使其超过十五个字符。

```
# hwmgr --set attr -a user_name=$(hostname) -id 46
hwmgr: 46: Attribute "user_name" value is too large.
```

现在让我们仅使用基本主机名来设置“user_name”属性。

```
# hwmgr --get attr -a user_name=$(hostname -s) -id 46

46:
  user_name = sheridan (settable)
```

验证更改是否已生效。

```
# hwmgr -get attr -id 46 -a name -a user_name
46:
name = COMPAQ AlphaServer DS10 466 MHz
user_name = sheridan (settable)
```

## 7.4.8 如何查找设备？

如果你有一个装满磁盘的大型机柜，不是能够快速找到你要找的设备就好了吗？可以。试试这个：

```
# hwmgr -flash light -dsc dsk3
```

虽然这仅适用于 SCSI 磁盘，但大多数磁盘目前仍是 SCSI，因此在近期内这是一个有用的命令。顺便说一下，如果由于机柜中其他磁盘活动导致闪烁过慢或过快，请尝试 "-nopause" 选项。

## 7.4.9 如何查找数据不一致的设备？

你可以使用带有 "-inconsistencies" 命令的 "hwmgr show component" 命令来定位硬件组件数据库文件中的软件不一致问题。“不一致”是指 dec_hwc_cdb 和 dec_hwc_ldb 文件中的可能内部错误。

```
# hwmgr show comp -i
HWID: HOSTNAME FLAGS SERVICE COMPONENT NAME
--------------------------------------------
106: molari rcd-i iomap SCSI-WWID:0c000008:0000-0e11-0018-9f1f
```

你可以通过添加 "-full" 选项来获取更多信息。

## 7.5 设备特殊文件管理器 (dsfmgr)

### 7.5.1 dsfmgr(8) 命令

dsfmgr 命令用于使用 Tru64 UNIX 版本 5.0 中定义的新命名约定来管理设备特殊文件。dsfmgr 使用以下数据库文件：

