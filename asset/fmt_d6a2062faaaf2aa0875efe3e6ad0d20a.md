
- 7. Duplicate Connections（重复连接）：未勾选

# 客户端设置

- 1. Topology（拓扑）：Subnet（子网）
- 2. DNS Default Domain（DNS 默认域名）：newvpn
- 3. DNS Server 1（DNS 服务器 1）：192.168.5.1
- 4. DNS Server 2（DNS 服务器 2）：94.140.14.14 (AdGuard DNS)
- 5. DNS Server 3（DNS 服务器 3）：94.140.15.15（另一个 AdGuard DNS 服务器）

# 高级客户端设置

- 1. Dynamic IP（动态 IP）：勾选
- 2. Advanced Configuration（高级配置）：
  - Custom Options（自定义选项）：
```
tun-mtu 1200; missfix 1160; push "dhcp-option DNS 192.168.5.1";
```
- 3. Gateway Creation（网关创建）：仅限 IPv4

对于网关创建 OpenVPN 设置：在 OpenVPN 部分的末尾选择 `IPv4`，这将为你节省掉大量的麻烦和痛苦！

注意：`RDRAND` 是 Intel 处理器内置的硬件随机数生成器（RNG）。它快速、易用，且 PfSense 可能正在使用它。警告：对于 99% 的读者来说，这完全是浪费时间。

### 什么是 RDRAND？为什么要关注它？

`RDRAND` 使用你的 CPU 生成随机数，但它是闭源的。你无法看到它的工作原理，并且有人担心某些随机数生成器可能并不如看起来那样随机。

*注：原文此处存在多处乱码或逻辑错误，如 "closed source" 应该为 "closed source", "RING" 应为 "RNG"，翻译已按原意处理*

# 4.1 在 Android 设备上导出 OpenVPN 配置

1. 转到 VPN > OpenVPN > Export。
2. 对于“remote”，选择你的 VPN 服务器。
3. 对于“Host Name”，输入 URL。
4. 在 Export Type 下选择 Android。
5. 下载配置文件（例如：`vpnuser.ovpn`）。

Specific Inc. Data Protection, Ltd. 是领先的数据保护服务提供。我们的使命是为日益数字化的世界提供保护数据安全的工具和专业知识。我们的服务利用尖端技术，包括人工智能和机器学习，在威胁造成损害之前进行检测和预防。我们还有一支安全专家可以就你的任何问题提供帮助。

了解更多

# 登录

请输入你的凭据以访问账户。

登录

# 导入配置

将配置文件导入到你的账户。

导入

# 资料

John Doe

john.doe@example.com
