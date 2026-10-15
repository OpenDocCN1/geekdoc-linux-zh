
# ping -s 1500 cuinfo.cornell.edu

使用 `ping` 命令时请注意以下限制。首先，仅凭 `ping` 命令很难区分网络故障和服务器故障。失败的 `ping` 只能你出了问题。
其次，`ping` 并对目标机器的状态提供太多保证。回显请求在 IP 协议栈内部处理，不需要在被探测的主机上运行服务器进程。响应仅保证机器已电源且没有发生内核恐慌（`kernel panic`）。你需要更高级的方法来验证 HTTP 和 DNS 等单个服务的可用性。

## 20.3 TRACEROUTE IP 数据包

`traceroute` 由 Van Jacobson 编写，让你发现 IP 数据包到达目的地所经过的网关序列。
语法简单如下：

```bash
traceroute hostname
```

有许多选项，但大多数在日常使用中并不重要。像往常一样，可以用符号或数字指定主机名。输出是一个主机列表，从第一个网关开始，到目的地结束。
例如，从 `jaguar` 主机到 `devil` 主机的 `traceroute` 产生如下输出：

```bash
% traceroute devil

traceroute to devil (192.225.55.137), 30 hops max, 38 byte packets

1 cor-gw2 (192.108.21.254) 0.840 ms 0.693 ms 0.671 ms

2 cor-gw4 (192.225.56.110) 4.642 ms 4.582 ms 4.674 ms

3 devil (192.225.55.137) 7.959 ms 5.949 ms 5.908 ms
```
