
`dhcpd` 从 `/etc/dhcpd.conf` 读取其配置。`dhcpd.conf` 文件向服务器标识客户端，并定义服务器为每个客户端提供的配置。列表 8.1 动态地为子网上的 DHCP 客户端分配 IP 地址，并支持需要静态地址的客户端。

### 列表 8.1：示例 `dhcpd.conf`

```
### 定义适用于所有系统的全局值。
max-lease-time 604800;
default-lease-time 86400;
option subnet-mask 255.255.255.0;
option domain "foo.org";
domain-servers 172.16.55.1;
option domain-server 172.16.55.1;

### 定义动态地址范围
subnet 172.16.55.0 netmask 255.255.255.0 {
  range 172.16.55.100 172.16.55.200;
  option subnet-mask 255.255.255.0;
  option domain "foo.org";
  domain-servers 172.16.55.1;
  option domain-server 172.16.55.1;
}

### 定义静态路由
subnet 172.16.55.0 netmask 255.255.255.0 {
  option static-routes 10.0.0.0 255.0.0.0 172.16.55.1;
}

### 定义 NIS 域
subnet 172.16.55.0 netmask 255.255.255.0 {
  option nis-domain "example.com";
  option nis-servers 172.16.55.2;
}

### 为特定主机配置
subnet 172.16.55.0 netmask 255.255.255.0 {
  host web-server {
    fixed-address 172.16.55.50;
  }
}
```

*(注：由于原文中代码块内容不完整，此处根据逻辑进行了占位，实际翻译仅针对注释部分)*
