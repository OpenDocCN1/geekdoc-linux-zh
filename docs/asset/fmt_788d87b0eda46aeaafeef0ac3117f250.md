
This process of identifying the cluster member's boot device should be performed on each cluster member's system console before the installation and configuration of the TruCluster Server software.

## 4.3 Firmware for a Cluster

Firmware on the AlphaServer and the StorageWorks storage subsystem components is the first software that is executed when the hardware powers up and usually the last software to execute as the hardware is powered down. It is also the software that directly controls the hardware and as such is platform dependent.

Although firmware is platform dependent, it is operating system independent. There have been many modifications to the operating system that are designed to interoperate with newer firmware features. For this reason, you should always install the latest firmware available from HP for the AlphaServers and for the StorageWorks storage subsystem of your cluster. All too frequently, operating system problems encountered by users can be traced to not having the appropriate firmware and operating system combination. As one colleague once said, "the PAL code makes the difference."10

### 4.3.1 Alpha Firmware

Alpha Firmware updates usually come on new Alpha Firmware Release CDs that accompany the release of a new version of Tru64 UNIX. Alpha Firmware updates can also be found on the Web at:

```
ftp://ftp.digital.com/pub/Digital/Alpha/firmware/
```

> 10 PAL code or Privileged Architecture Library (`PAL-code`) is made up of non-interruptible functions required to support the lowest level of activities on an AlphaServer system such as context switching, system call initiation, and interrupt/exception dispatching.

在更新任何 AlphaServer 的 Alpha 固件之前，务必查阅固件的发行说明，了解新功能、注意事项和已知异常。务必查阅与要更新的 AlphaServer 对应的固件发行说明，以了解在您的 AlphaServer 上更新固件的确切步骤。

**重要提示：**

在执行任何 Alpha 固件升级时，请勿中止更新。此外，您应避免在升级过程中可能导致 AlphaServer 断电的任何情况（即，除非 AlphaServer 已连接至 UPS，否则请勿在雷雨期间升级固件）。如果发生上述任一事件，请联系当地的 HP 现场工程师检查系统。

以下示例提供了如何更新特定 AlphaServer 固件的简要步骤<sup>11</sup>。

- 将固件 CD 插入 CDROM 并确定 CDROM 是哪个设备。

  ```
  P00>>> show dev
  dga1.1001.0.7.1        $1$DGA1        HSG80   V86F
  dkc0.0.0.7.0         DKC0            RZ1DD-LS 0306
  dqa0.0.0.0.105.0      DQA0            CD-224E 9.5B
  dva0.0.0.0.0          DVA0
  ...
  ```

- 重新初始化服务器。

  ```
  P00>>> init
  ```

- 从 Alpha 固件 CD 启动。

  ```
  P00>>> boot DQA0
  ...
  [Release notes are displayed.]
  ```

- 在提示时，输入引导文件或按回车键接受固件 CD 上的默认引导文件。

  ```
  ...
  The default bootfile for this platform is
  [DS20]DS20_V6.1_EXE
  Hit <RETURN> at the prompt to use the default bootfile.
  ```

- 从主菜单中选择以下菜单项：

    - CMOS setup

    - Advanced CMOS setup

    - Console Selection: Digital UNIX Console (SRM)

- 按 F10 键保存您的选择。

- 关闭系统电源然后重新打开电源。

> 11 根据 AlphaServer DS20 V6.2 控制台固件发行说明。

### 4.3.3 主机总线适配器固件

从 Alpha 固件更新版本 6.1 开始，主机总线适配器固件和 Alpha 固件会同时更新。需要更新的设备列表中包含 KGPSA 主机总线适配器——即 `pga0` 设备。只需确保为该设备更新固件即可。

### 4.3.4 HSZ/HSG RAID 阵列控制器固件

HSZ/HSG RAID 阵列控制器固件的更新应交由 HP 现场服务工程师处理。只有真正了解自己在做什么的客户才应尝试此更新，并且只有在对存储子系统上的任何数据进行完整备份后才可进行。

支持 TruCluster Server 的最低 HSZ/HSG 固件版本见表 4-3。

要确定您的 HSZ/HSG 控制器的固件级别，请使用以下命令：

```
HSG> show this
Controller:
    HSG80 ZG14100634 Software V86F-8, Hardware E16
...
```

在此示例中，`HSG80` 控制器处于 ACS 固件版本 V86F-8。 “-8” 通常表示固件的补丁级别。适用于 HSG ACS 固件的相同约定和注意事项也可适用于 HSZ 系列控制器的 HSOF 固件。

### 4.3.5 光纤通道交换机固件

同样，与 HSZ/HSG RAID 阵列控制器固件一样，只有 HP 现场服务工程师才应执行光纤通道交换机固件的更新。

## 4.4 配置和验证集群互连硬件

实现集群需要一个专用的集群互连，所有集群成员都连接到其中。集群互连为虚拟专用网络提供基础，允许所有集群成员之间进行通信。此集群互连在集群节点或成员之间提供节点间通信（通过 ICS<sup>12</sup>）。*TruCluster* Server 软件在集群内创建此虚拟专用网络，并且此虚拟专用网络与集群互连提供的物理通信通道并存。

> 12 节点间通信子系统在第 18 章中介绍。

这是如何工作的？对于每个成员，集群软件都会为集群互连创建一个虚拟网络设备。在 V5.1A 中，该设备名为 `ics0`。在 V5.0A 和 V5.1 中，该设备名为 `mc0`，因为当时仅支持 Memory Channel 适配器卡作为集群互连。无论如何，该设备都有自己的 IP 名称和 IP 地址，用于建立系统在集群中的成员资格。

可用于集群互连的硬件可以是 Memory Channel (`MC`) 适配器或以太网局域网 (`LAN`) 卡，但不能同时混用两者。

集群互连在集群内提供以下功能：

- **集群成员之间的健康状态消息。** 连接管理器使用此信息来监控集群成员并协调成员资格。有关连接管理器子系统的更多信息，请参阅第 17 章。

- **集群成员之间的分布式锁管理器 (`DLM`) 锁定。** 用于协调对共享资源的访问。有关 DLM 的更详细信息，请参阅第 18 章。
