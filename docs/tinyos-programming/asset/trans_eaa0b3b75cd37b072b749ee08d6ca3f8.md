

将同一个接口实例化为三个实例会产生大量额外的布线。除了 LedsC 之外，还有一个 NoLedsC，可以作为空替换插入：对 NoLedsC 的调用不执行任何操作。

```
configuration LedsC {
  provides interface Leds;
}
```

```
configuration NoLedsC {
  provides interface Leds;
}
```

## A.7.3 循环冗余校验

循环冗余校验（CRCs）是检查数据是否已损坏的一种简单方法。在数据之后，你附加一个 CRC。读取数据的人可以重新计算数据的 CRC 并检查它是否与附加的 CRC 匹配。如果两者不匹配，则数据或 CRC 本身存在位错误。由于 CRC 通常比数据短得多，因此假设数据已被损坏。CRCs 在网络中被大量使用，以检查数据包的有效性。当然，由于 CRCs 比数据本身短，因此损坏的数据包通过 CRC 检查是可能的，但可能性很小。

CRC 值与加密哈希不同。CRCs 的目的是检测突发位错误。通常，n 位 CRC 总能检测到小于 n 位的单次错误突发。相比之下，加密强度高的哈希具有熵特性，使得检测到（或未能检测到）任何类型错误的机会是均匀的。

```
module CrcC {
  provides interface Crc;
}
```

模块 CrcC 可以在 tos/system 中找到。

## A.7.4 Printf

有时，在调试时，让 mote 发送简单的文本消息会非常有用。TinyOS 有一个 printf 库——类似于 C 标准库函数——用于此目的。你可以在组件中使用 printf，而 printf 库会通过串行端口发送适当的包。你必须通过 PrintfC 的 SplitControl.start 启动 printf 库。

```
configuration PrintfC {
  provides (
    interface SplitControl as PrintfControl;
    interface PrintfFlush;
  )
}
```

有关使用 printf 库的更多详细信息，请参阅 TinyOS 网站上的教程。

## A.8 低功耗

在大多数情况下，TinyOS 会自动将系统和硬件置于可能的最低功耗状态。对于外设，这通常通过电源锁实现（第 11.2 节）。例如，当应用程序从闪存芯片写入或读取时，TinyOS 会自动将其打开，执行操作，然后在完成后将其关闭。

通信是此行为的主要例外。由于通信子系统，例如无线电和串行端口，需要能够接收和发送，TinyOS 需要应用程序通过 SplitControl 接口明确告知它何时可以安全地打开和关闭它们。

然而，在无线电的情况下，有许多技术可以用来节省电量。例如，而不是始终保持无线电开启，TinyOS 可以让它大部分时间处于关闭状态，定期将其打开足够长的时间以听是否有数据包。发送方多次发送数据包，直到接收方唤醒、听到它并确认它，或者超时发生。

关于如何设置这些间隔的完整讨论超出了本书的范围。重要的接口是 LowPowerListening，一些（但不是全部）无线电提供。LowPowerListening 允许应用程序设置无线电的检查间隔以及它期望接收方使用的检查间隔。TinyOS 有一个教程，介绍如何在编写低功耗应用程序时使用此接口，第 12.2.3 节也简要举例说明了其用法。

[18] P. Levis and G. Tolle. TEP 118: Dissemination. www.tinyos.net/ tinyos-2.x/doc/.

[19] J. Liu, N. Priyantha, F. Zhao, C.-J. M. Liang, and Q. Wang. Towards discovering data center genome using sensor nets. In EmNets '08: Proceedings of the Fifth Workshop on Embedded Networked Sensors, 2008.

[20] S. Madden, M. J. Franklin, J. M. Hellerstein, and W. Hong. TinyDB: An acquisitional query processing system for sensor networks. Transactions on Database Systems (TODS), 30(1), 2005, 122–173.

[21] A. Mainwaring, J. Polastre, R. Szewczyk, D. Culler, and J. Anderson. Wireless sensor networks for habitat monitoring. In Proceedings of the ACM International Workshop on Wireless Sensor Networks and Applications, 2002.

[22] M. Maroti, B. Kusy, G. Simon, and A. Ledeczi. The flooding time synchronization protocol. In SenSys '04: Proceedings of the Second International Conference on Embedded Networked Sensor Systems, pages 39–49, New York, NY, USA, 2004. ACM Press.

[23] J. Polastre, J. Hill, and D. Culler. Versatile low power media access for wireless sensor networks. In SenSys '04: Proceedings of the Second International Conference on Embedded Networked Sensor Systems, pages 39–49, New York, NY, USA, 2004. ACM Press.

[24] D. Rand. PPP Reliable Transmission. Internet Network Working Group RFC1663, July 1994.

[25] C. Sharp, M. Turon, and D. Gay. TEP 102: Timers. www.tinyos.net/tinyos-2.x/doc/.

[26] R. Szewczyk, J. Polastre, A. Mainwaring, and D. Culler. An analysis of a large scale habitat monitoring application. In SenSys '04: Proceedings of the Second International Conference on Embedded Networked Sensor Systems, New York, NY, USA, 2004. ACM Press.

[27] G Tolle and D. Culler. Design of an application-cooperative management system for wireless sensor networks. In EWSN '05: Proceedings of Second European Workshop on Wireless Sensor Networks, 2005.

[28] G Tolle, P. Levis, and D. Gay. TEP 114: SIDs: Source and Sink Independent Drivers. www.tinyos.net/tinyos-2.x/doc/.

[29] T. von Eicken, D. E. Culler, S. C. Goldstein, and K. E. Schauser. Active messages: A mechanism for integrated communication and computation. In ISCA '92: Proceedings of the International Symposium on Computer Architecture, pages 256–266, 1992.

[30] G Werner-Allen, K. Lorincz, J. Johnson, J. Lees, and M. Welsh. Fidelity and yield in a volcano monitoring sensor network. In OSDI '06: Seventh USENIX Symposium on Operating Systems Design and Implementation, 2006.

