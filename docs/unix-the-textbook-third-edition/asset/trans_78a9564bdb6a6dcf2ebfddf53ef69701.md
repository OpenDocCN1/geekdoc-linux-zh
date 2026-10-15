

创建基础 jail：

```
# iocage create -b
```

创建轻量级 jail 并将其 IP 地址和标签名设为 myjail：

```
# iocage create -c tag=myjail ip4_addr="em0|10.1.1.10/24"
```

列出 jail：列出所有 jail：

```
# iocage list
```

查看所有已下载的发行版：

```
# iocage list -r
```

查看可用模板：

```
# iocage list -t
```

启动、停止或重启 jail：要启动或停止系统上的任何 jail，均可互换使用 UUID 和 TAG。为了简化 UUID 处理，iocage 也接受在任何子命令中使用部分 UUID。

启动标签为 myjail 的 jail：

```
# iocage start myjail
```

使用完整 UUID 启动 jail，运行：

```
# iocage start 26e8e027-f00c-11e4-8f7f-3c970e80eb61
```

或者，只使用部分 UUID 启动 jail，只输入前几个字符：

```
# iocage start 26e8
```

要停止 jail，只需改用 stop 子命令而不是 start：

```
# iocage stop myjail
```

要重启 jail，运行以下命令，该 jail 必须已在运行：

```
# iocage restart myjail
```

注意：短 UUID 在 iocage 的所有操作和子命令中均受支持。

配置 jail：任何属性都可以用 set 子命令重新配置。
设置 jail 的 tag 属性：

```
# iocage set tag=myjail 26e8e027
```

获取 jail 属性：要验证任何属性，请使用 get 子命令：

```
# iocage get tag 26e8e027
```

获取所有属性，或显示所有支持的属性：

```
# iocage get all 26e8e027
```

系统范围默认值：从 iocage 版本 1.6.0 开始，可以设置系统范围默认值。这些默认值将重新应用于所有新创建的 jail。要为属性创建系统范围默认值覆盖，只需指定 default 关键字而不是 jail UUID 或标签即可。

关闭所有新创建 jail 的 VNET 功能：

```
# iocage set vnet=off default
```

销毁 jail：

```
# iocage destroy myjail
```

jail 必须已停止或关闭后才能被销毁。
警告：这将不可逆地销毁 jail！

## 25.2.3 iocage 网络

Jail 根据所需功能有多种网络选项。

### 25.2.3.1 用于基于 IP 别名的网络（共享 IP）

iocage 会尝试判断系统是否支持 VNET，如果支持，则默认对新创建的 jail 启用它。

确保 VNET 已禁用：

```
# iocage get vnet UUID | TAG
```

如果设置为 "on"，则禁用它：

```
# iocage set vnet=off UUID | TAG
```

如果需要，可以配置系统范围默认值。这仅对新创建的 jail 生效。

```
# iocage set vnet=off default
```

配置 IP 地址：

```
# iocage set ip4_addr="em0|10.1.1.10/24" UUID | TAG
```

如果需要多个地址，只需用逗号分隔配置指令即可：

```
# iocage set ip4_addr="em0|10.1.1.10/24,em0|10.1.1.11/24" UUID | TAG
```

启动 jail：

```
# iocage start UUID | TAG
```

验证 jail 中可见的 IP 配置（此操作需要 jail 正在运行）：

```
# iocage exec UUID | TAG ifconfig
```

### 25.2.3.2 用于 VNET 网络

在 /etc/rc.conf 中添加网桥配置（在主机上）：

```
cloned_interfaces="bridge0 bridge1"
ifconfig_bridge0="addm em0 up"
ifconfig_em0="up"
```

在 /etc/sysctl.conf 中添加以下可调参数：

```
net.inet.ip.forwarding=1
net.link.bridge.pfil_onlyip=0
net.link.bridge.pfil_bridge=0
net.link.bridge.pfil_member=0
```

为 jail 配置默认网关：

```
# iocage set defaultrouter=10.1.1.254 UUID | TAG
```

配置 IP 地址：

```
# iocage set ip4_addr="vnet0|10.1.1.10/24" UUID | TAG
```

启动 jail 并 ping 默认网关。
启动 jail：

```
# iocage start UUID | TAG
```

打开进入 jail 的控制台：

```
# iocage console UUID | TAG
```

Ping 默认网关：

```
# ping 10.1.1.254
```

### 25.2.3.3 配置网络接口

iocage 对共享 IP 和 VNET jail 的网络配置进行透明处理。

配置共享 IP jail：

IPV4

```
# iocage set ip4_addr="em0|192.168.0.10/24" UUID|TAG
```

IPV6

```
# iocage set ip6_addr="em0|2001:123:456:242::5/64" UUID|TAG
```

此命令将在启动时为共享 IP jail 在接口 em0 上添加 192.168.0.10/24 的 IP 别名，以及 2001:123:456:242::5/64。

配置 VNET jail：

要同时配置 IPV4 和 IPV6：

```
# iocage set ip4_addr="vnet0|192.168.0.10/24" UUID|TAG
```

```
# iocage set ip6_addr="vnet0|2001:123:456:242::5/64" UUID|TAG
```

```
# iocage set defaultrouter6="2001:123:456:242::1" UUID|TAG
```

对于 VNET jail，还必须指定默认路由。

此外，要启动没有 IPV4/6 地址的 jail，请设置以下属性：

```
# iocage set ip4_addr=none ip6_addr=none UUID|TAG
```

```
# iocage set defaultrouter=none defaultrouter6=none UUID|TAG
```

## 25.2.4 Jail 类型

iocage 支持五种不同的 jail 类型：

- thick（默认）
- thin
- base
- template
- empty

完整（thick）：完整（thick）jail 是默认类型，使用以下命令创建：

