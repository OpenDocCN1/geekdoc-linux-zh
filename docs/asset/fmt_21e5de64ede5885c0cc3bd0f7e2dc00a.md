
一般描述：TCP 客户端。
父类：`SocketStream`

方法：

- `void Connect(HostAddress& Addr);` 连接到 `Addr` 处的主机。

抛出异常：
- `NetConnectException`

### Datagram（类）

构造函数：

```cpp
Datagram(HostAddress& Me, ENetwork Network=eIPv4, EProtocol Protocol=eDatagram);

Datagram(ENetwork Network=eIPv4, EProtocol Protocol=eDatagram);
```

一般描述：通用数据报（UDP）套接字。
父类：`Socket`

方法：

- `void MinimizeDelay(bool Setting);` 请求最小数据包延迟。
- `void MaximizeThroughput(bool Setting);` 请求最大网络吞吐量。
- `void MaximizeReliability(bool Setting);` 请求最大可靠性。
- `void MinimizeCost(bool Setting);` 请求最小成本。
- `void PermitFragNegotion(EFrag Setting);` 设置分片协商。

抛出异常：
- `NetConfigException`

### Broadcast（类）

构造函数：

```cpp
Broadcast(HostAddress& Me);
```

一般描述：子网广播套接字。
父类：`Datagram`

方法：（无）

抛出异常：
- `NetConfigurationException`

### MessageGroup（类）

构造函数：

```cpp
MessageGroup(HostAddress& Me, ENetwork Network=eIPv4);
```
