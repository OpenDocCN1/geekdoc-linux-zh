
所需或必需。`ifPhysAddress` 中包含的地址用于系统间的低级网络通信。每当一个数据包从此接口发出时，该地址将用作数据包的源地址。

`ifAdminStatus` 和 `ifOperStatus` 对象显示接口的管理状态和操作状态。网络管理员使用管理状态来控制接口。该对象提供了控制接口何时标记为 `up` 或 `down` 的能力。此外，还可以设置第三种状态 `testing`。`up` 状态意味着允许数据包通过接口流动，而 `down` 状态意味着不接收或发送来自此接口的数据包。这与接口的物理连接状态无关。换句话说，网络接口可能已连接到运行中的网络，但如果它被标记为 `down`，则该接口不会读取任何网络流量。`testing` 状态启用内部接口诊断以验证接口的正确操作。`ifOperStatus` 对象显示接口的当前状态，它是 `ifAdminStatus` 对象所表示的已定义状态之一。该对象获取特定接口的状态。

> `ifAdminStatus` 对象的访问权限为读写；接口组中的所有其他对象都无法由网络管理员修改，因为它们具有只读访问权限。这一点的原因应该显而易见且合乎逻辑。接口的计数器和描述性信息不应被更改，这是合理的，因为保持接口类型信息以避免网络配置问题并维护准确的性能指标非常重要。

`ifSpecific` 对象包含 `ccitt.nullOID` 的值，它代表一个有效但为空的 OID 字符串。接口组包含以下对象集合。

- **对象名称：** `ifNumber`
- **OID：** `interfaces.1`
- **对象类型：** Integer
- **访问模式：** read-only
- **描述：** 本地系统中包含的网络接口总数

**对象名称：** ifTable
**OID：** `interfaces.2`
**对象类型：** Sequence of ifEntry
**访问模式：** na
**描述：** 此表的接口条目列表或行

**对象名称：** ifEntry
**OID：** `interfaces.ifTable`
**对象类型：** Sequence
**访问模式：** not-accessible
**描述：** 包含其下方定义的所有对象的特定接口条目

**对象名称：** ifIndex
**OID：** `ifEntry.1`
**对象类型：** Integer
**访问模式：** read-only
**描述：** 用于访问网络接口的特定介质类型的 MIB 引用定义

**对象名称：** ifDescr
**OID：** ifEntry.2
**对象类型：** DisplayString [255]
**访问模式：** read-only
**描述：** 接口的字符串描述，包括从操作系统角度看到的接口名称；可能的值包括：eth0、ppp0 和 lo0

**对象名称：** ifType
**OID：** ifEntry.3
**对象类型：** INTEGER
**访问模式：** read-only
**描述：** 接口类型。表 6.3 列出了具体类型

**对象名称：** ifMtu
**OID：** ifEntry.4
**对象类型：** Integer
**访问模式：** read-only
**描述：** 接口的最大传输单元。这表示可在接口上发送和/或接收的最大帧

**对象名称：** ifSpeed
**OID：** ifEntry.5
**对象类型：** Gauge
**访问模式：** read-only
**描述：** 接口的数据速率（容量）

**对象名称：** ifPhysAddress
**OID：** ifEntry.6
**对象类型：** PhysAddress
**访问模式：** read-only
**描述：** 接口的数据链路地址

**对象名称：** ifAdminStatus
**OID：** ifEntry.7
**对象类型：** Integer
**访问模式：** read-write
**描述：** 接口的管理状态，它是 `ifOperStatus` 对象中列出的已定义状态之一。设备所有者可利用此对象控制接口

**对象名称：** ifOperStatus
**OID：** ifEntry.8
**对象类型：** Integer
**访问模式：** read-only
**描述：** 接口当前的操作状态。已定义的状态包括 up(1)、down(2) 和 testing(3)

**对象名称：** ifLastChange
**OID：** ifEntry.9
**对象类型：** TimeTicks
**访问模式：** read-only
**描述：** 接口最后更新为其当前操作状态的时间

**对象名称：** ifInOctets
**OID：** ifEntry.10
**对象类型：** Counter
**访问模式：** read-only
**描述：** 接口接收的八位字节（字节）数，包括任何数据链路帧字节

**对象名称：** ifInUcastPkts
**OID：** ifEntry.11
**对象类型：** Counter
**访问模式：** read-only
**描述：** 通过高层协议交付给子网的单播数据包数量

**对象名称：** ifInNUcastPkts
**OID：** ifEntry.12
**对象类型：** Counter
**访问模式：** read-only
**描述：** 交付给高层网络协议的非单播数据包数量

**对象名称：** ifInDiscards
**OID：** ifEntry.13
**对象类型：** Counter
**访问模式：** read-only
**描述：** 被丢弃的入站数据包数量（尽管无错误），不会被交付给高层网络协议

**对象名称：** `ifInErrors`
**OID：** `ifEntry.14`
**对象类型：** `Counter`
**访问模式：** `read-only`
**描述：** 因错误而未被交付给高层网络协议的入站数据包数量

**对象名称：** `ifInUnknownProtos`
**OID：** `ifEntry.15`
**对象类型：** `Counter`
**访问模式：** `read-only`
**描述：** 因未知或不支持的网络协议而被丢弃的入站数据包数量

**对象名称：** `ifOutOctets`
**OID：** `ifEntry.16`
**对象类型：** `Counter`
**访问模式：** `read-only`
**描述：** 接口上发送的八位字节（字节）数。这也包括任何数据链路帧字节

**对象名称：** `ifOutUcastPkts`
**OID：** ifEntry.17
**对象类型：** Counter
**访问模式：** read-only
**描述：** 高层协议（如 IP）请求发送到网络单播地址的数据包数量。这包括被丢弃或未发送的数据包

**对象名称：** ifOutNUcastPkts
**OID：** ifEntry.18
**对象类型：** Counter
**访问模式：** read-only
**描述：** 高层协议（如 IP）请求发送到非单播地址的数据包数量。这也包括被丢弃或因其他原因未发送的数据包。

**对象名称：** ifOutDiscards
**OID：** ifEntry.19
**对象类型：** Counter
**访问模式：** read-only
**描述：** 因与特定错误条件无关的原因而无法发送的数据包数量。例如，这可能是由数据包的 TTL 过期引起的

**对象名称：** ifOutErrors
**OID：** ifEntry.20
**对象类型：** Counter
**访问模式：** read-only
**描述：** 因错误而无法发送的数据包数量

**对象名称：** `ifOutQLen`
**OID：** `ifEntry.21`
**对象类型：** `Gauge`
**访问模式：** `read-only`
**描述：** 设备上输出数据包队列的长度

**对象名称：** `ifSpecific`
**OID：** `ifEntry.22`
**对象类型：** `Object Identifier`
**访问模式：** `read-only`
**描述：** 用于实现网络接口的特定介质类型的 MIB 引用定义

## 地址转换组

`at` 组由单个表组成，该表提供从网络地址到物理地址的映射。图 6.4 显示了地址转换组的树视图。该组已被弃用（这意味着它已被另一组 MIB 对象取代），但为了与现有的 MIB-I 标准向后兼容而保留。许多现有代理继续支持此组，包括 Linux 代理。既然是这样，我们在此描述该组。
