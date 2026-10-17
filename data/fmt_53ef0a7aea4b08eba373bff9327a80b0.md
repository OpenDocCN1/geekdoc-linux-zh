
与无线电栈（第 6.3 节）类似，TinyOS 串行栈遵循分层结构（图 6.1，第 89 页）。TinyOS 串行通信栈的最低层在 `TEP 113` 中定义，并处理在不可靠的串行连接上交换数据包。与无线电数据包一样，这些数据包在大多数情况下是“主动消息”数据包。在本章的其余部分，我们将使用 `message` 指代串行 AM 数据包的有效载荷，不同的消息类型由其 AM 类型标识。

串行 AM 数据包的布局使用外部类型定义：

```
typedef nx_struct serial_header {
  nx_uint16_t dest;  /* packet destination */
  nx_uint16_t src;   /* packet sender */
  nx_uint8_t length; /* payload length, in bytes */
  nx_uint8_t group;  /* identifies a specific sensor network */
  nx_uint8_t type;   /* AM type */
} serial_header_t;
```

```
typedef nx_struct serial_packet {
  serial_header_t header;
  nx_uint8_t data[];
} serial_packet_t;
```

列表 7.1 串行 AM 数据包布局

`type` 字段用于分发有效载荷（`data[]`）。串行 AM 数据包没有页脚。`dest`（目标）和 `src`（发送者）字段对于通过串行连接交换的数据包来说并不直接相关，因为发送者和目标通常是隐含的。同样，`group` 也不相关：它用于区分参与不同应用但共享物理连接的不同 mote。这些字段是为了与通过无线电发送的 AM 数据包保持一致而包含的，并在某些基站 mote 应用中使用，而在其他应用中被忽略。例如，在将无线电 AM 数据包转发到/来自 PC（作为串行 AM 数据包）的 `BaseStation` 应用中：

- 从 `BaseStation` 到 PC：`src`、`dest` 和 `group` 与接收到的无线电 AM 数据包中的相同。
- 从 PC 到 `BaseStation`：发送的无线电 AM 数据包将其目标设置为 `dest`，但将其发送者和 `group` 设置为 `BaseStation` mote 的。

有了这些选择，带有 `BaseStation` mote 的 PC 就像带有直接连接的 mote 无线电的 PC 一样工作。

相反，`TestSerial` 应用（TinyOS 标准发行版的一部分）忽略这三个字段。`TestSerial` 是一个用于测试串行连接性的应用：mote 和 PC 只是相互发送包含连续数字的消息。mote 将这些数字的低三位显示在其 LED 上，而 PC 只是打印这些数字。`TestSerial` 使用以下简单的外部类型来

![](img/53ede4f4266a5731b93bff15d85fa06a_137_0.png)

图 7.1 TestSerial 数据包布局。

指定其消息布局：

```
typedef nx_struct test_serial_msg {
  nx_uint16_t counter;
} test_serial_msg_t;
```

清单 7.2 TestSerial 数据包布局

包含 `test_serial_msg_t` 消息的串行 AM 数据包通过 AM 类型字段 9 进行标识。图 7.1 显示了 `serial_packet_t` 与 `test_serial_msg_t` 外部类型之间的最终连接关系（该图未显示最低的数据包交换层，因为该层不使用外部类型进行指定）。

### 7.2 使用 mig

`mig` 工具会生成一个类，用于表示给定的 nesC `nx_struct M` 的值。该类提供读取、写入和报告 `M` 字段属性的方法。对于由 `mig` 生成的 `M` 类，`net.tinyos.message` 包提供了相应的类和方法，使你能够发送和接收有效载荷为 `M` 类型值的串行 AM 数据包。

`Mig` 生成的类使用后备数组（backing array）来表示结构值，该字节数组以与在 mote 上相同的表示形式存储结构值，因此也与 TinyOS 数据包中的表示形式一致。图 7.2 显示了一个典型场景：一个 mote 向 PC 发送串行 AM 数据包。在 mote 上，数据包由指向 `serial_packet_t` 的指针 `x` 表示。`x` 的表示形式与 PC 串行连接上数据包的表示形式相同。在 PC 端，`mig` 生成的类使用包含相同字节的后备数组来表示 `serial_header_t`（串行 AM 数据包头部的外部类型）值。

![](img/53ede4f4266a5731b93bff15d85fa06a_138_0.png)

图 7.2 Mig 与外部类型。

`Mig` 生成的类支持 C 结构体的所有特性，包括位域、数组、联合和嵌套结构（也可以将 `mig` 用于常规 C 结构体，但生成的代码是针对特定 mote 的，因为不同 mote 具有不同的字节序和不同的 C 结构体布局规则）。它们允许你执行在 nesC 程序中对结构体所能执行的所有操作（甚至更多）：

- 创建一个新的（所有字段初始化为零）结构值。
- 将某个结构的一部分转换为另一个结构（例如，将 `serial_packet_t` 的 `data[]` 字段转换为 `test_serial_msg_t`）。
- 读取和写入任意字段。
- 获取字段信息：其偏移量、大小、符号性等。
- 获取表示特定结构值的字节数组。

`Mig` 生成的类是 `net.tinyos.message.Message` 的子类，以简化可处理多种消息布局的通用代码编写。`Message` 类的主要公共功能是提供对 `mig` 生成类后备数组的访问。后备数组是 Java `byte[]` 数组的一个切片，由偏移量和长度指定。该数组、偏移量和长度通过以下三个方法返回：

```
public byte[] dataGet();
public int baseOffset();
public int dataLength();
```

清单 7.3 后备数组方法

例如，在图 7.2 中，用于 `serial_header_t` 的 `mig` 生成类从表示整个串行 AM 数据包的 9 字节数组中取从偏移量 0 开始的 7 字节切片。使用 `byte[]` 数组的切片允许 `mig` 生成的类表示存储在另一个 `mig` 生成类中的值，从而支持将一个结构的一部分“转换”为另一个结构。

对于 `test_serial_msg_t`，由 `mig` 生成的 `TestSerialMsg` 类的基本构造函数和方法是：

- `TestSerialMsg()`：创建一个新的（字段初始化为零）`test_serial_msg_t` 值。
- `static int offset_counter()`：返回 `test_serial_msg_t` 结构中 `counter` 字段的偏移量（以字节为单位）。
- `get_counter()`：返回 `counter` 字段的值。
- `set_counter(int value)`：修改 `counter` 字段的值。

#### 7.2.1 发送和接收 mig 生成的数据包

`net.tinyos.message` 包提供了一个名为 `MoteIF`（表示“mote 接口”）的类，使得发送和接收由 `mig` 生成类指定的消息变得简单。

在使用 `MoteIF` 之前，你需要打开与基站 mote 的连接。这通过调用 `net.tinyos.packet.BuildSource.makePhoenix` 方法完成，该方法的参数是数据包源名称。该数据包源名称指定了你如何访问基站 mote（例如，通过串口）以及所有相关参数（例如，设备名称、波特率等）。在本节的其余部分中，我们将使用 `"serial@COM1:telosb"` 作为数据包源，它表示通过串口 `COM1` 以 Telos mote 的正常波特率（115,200 波特）进行串行通信。大多数使用 `MoteIF` 的 Java 程序都会接受一个命令行参数来指定实际的数据包源。第 7.4 节将更详细地讨论数据包源及其动机。

使用 `MoteIF` 和 `mig`，发送 `test_serial_msg_t` 消息的代码非常简单，如下面这段摘自 `TestSerial.java` 文件的简化代码所示。连续数据包的发送使用 `MoteIF` 的 `send` 方法，该方法接受一个 `mig` 生成类的对象作为参数：
