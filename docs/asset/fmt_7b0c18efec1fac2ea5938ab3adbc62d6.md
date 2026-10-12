
当然，如果设备不是`eth0`，你应该调整此命令。如果你的`DHCP`服务器有多个网络接口，这个问题可能会发生。某些`DHCP`配置默认允许这样做。如果你的不允许，你可以按照第9章“跳过自动配置获取控制”所述修改`DHCP`脚本或添加命令。你可以通过输入`-n`来验证此路由是否存在。如果路由存在，它应该出现在输出的顶部：

| 目的 | 网关 | 生成掩码 | 标志 | 跃点 | 接口 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `255.255.255.255` | `255.0.0.0` | `255.255.255.255` | `UH` | `0` | `0` | `eth0` |

## 设置全网络选项

大多数`DHCP`配置文件以一组设置全局选项的参数开头。列表`27.1`显示了一个典型的`dhcp.conf`文件，包含了许多你可能使用的全局选项。许多但并非所有全局选项都以关键字`option`开。无论参数是否以该关键字开头，大多数后面都跟着一个值。该值可以是`IP`地址、主机名、数字、布尔值（`true`或`false`）或其他其他数据。

## 列表 27.1：示例 `dhcp.conf` 文件

```bash
default-lease-time 86400;
max-lease-time 172800;
option subnet-mask 255.255.255.0;
option routers 172.27.15.1;
option domain-name-servers 172.27.15.2,10.72.81.2;
option domain-name "threeroomco.com";
option nbtbios-servers 172.27.15.2;
option nbtbios-node-type 8;
get-lease-hostname true;
subnet 172.27.15.0 netmask 255.255.255.250 (
  range 172.27.15.50 172.27.15.254;
);
```
