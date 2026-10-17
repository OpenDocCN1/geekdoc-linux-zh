
```
USERCTL=no
PEERDNS=yes
TYPE=Wireless
DEVICE=eth0
HWADDR=00:02:2d:8c:f8:c5
BOOTPROTO=dhcp
ONBOOT=no
DHCP_HOSTNAME=
NAME=
ESSID='UNKNOWN!!'
CHANNEL=6
MODE=Managed
KEY=aecf-a00f-03
RATE=auto
```

- 3. 编辑文本文件 `/etc/pcmcia/network` 并找到以下行：
`'start'`

在此行紧之后，添加以下文本行：

```
[ -f /etc/sysconfig/network-scripts/ifcfg-$(device) ] && /etc/sysconfig/network-scripts/ifup ifcfg-$(device)
```
and on
