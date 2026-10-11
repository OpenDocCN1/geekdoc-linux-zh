
| Name | Mtu | Net/Dest Address | Ipkts | Ierrs | Opkts | Oerrs | Collis | Queue |
|---|---|---|---|---|---|---|---|---|
| 0 | 8232 | loopback localhost | 18927030 | 0 | 18927030 | 0 | 0 | |
| le0 | 1500 | sunys 310417964 | 0 | 17193381 | 52064 | 7573173 | | |
| sunys/home/martyp/shellprogs | | | | | | | | |
| le0 | 1500 | sunys 310418018 | 0 | 17193388 | 52064 | | | |
| le0 | 1500 | sunys 310418738 | 0 | 17193395 | 52064 | 7573173 | | |
| le0 | 1500 | sunys 310419579 | 0 | 17193401 | 52064 | 7573173 | | |
| le0 | 1500 | sunys 310420295 | 0 | 17193401 | 52064 | 7573173 | | |
| le0 | 1500 | sunys 310421099 | 0 | 17193446 | 52064 | 7573173 | | |
| le0 | 1500 | sunys 310421786 | 0 | 17193455 | 52064 | | | |
| le0 | 1500 | sunys 31042425 | 0 | 17193462 | 52064 | | | |
| le0 | 1500 | sunys 310423089 | 0 | 17193467 | 52064 | | | |
| le0 | 1500 | sunys 310423749 | 0 | 17193471 | 52064 | | | |
| le0 | 1500 | sunys 310424507 | 0 | 17193478 | 52064 | | | |

`martyp $`

`net1` 每 30 秒产生一次我们想要的 `le0` 输出，在 Solaris 系统上运行。我们也在每次循环中打印 `i` 的值，可以看到我们正在正确地递增。在 HP-UX 系统上，`netstat` 命令被修改为提供较少的信息。以下脚本自动产生局域网接口列表并为每个网卡产生输出：

```bash
#!/bin/sh

# ( ) Header: 创建网络统计输出的脚本

# ( ) Source: $

# ( ) Locker: $

# ( ) Slag: $

# ( ) INPUT:

# ( ) OUTPUT:

# ( ) FILES USED:

## ksh 编程

# NOTES:

# AUTHOR:

# REVISION:

# Setup

PATH=/bin:/usr/sbin:/local/bin;

# Determine OS级别

OS_VERSION=$(uname -r | awk -F. '{print $2}')

if [ $OS_VERSION -lt 10 ];
then
  COMMAND1=/bin
else
  COMMAND1=/usr/sbin
fi

if [ -x $COMMAND1 ]; then
  COMMAND2=/usr/sbin
  if [ -x $COMMAND2 ]; then
    if [ $OS_VERSION -lt 10 ]; then
      for CARD in $(ls /dev/lan* | awk -F/ '{print $3}'); do
        echo ""
      done
    fi
  fi
fi

COMMAND1 << EOF >/dev/null | egrep ""
name

# 使用输出的字段3 获取使用的网卡实例

for NMID in '$COMMAND2' | grep 0x | awk '{print $3}'; do
  echo ""
done

COMMAND1 << EOF >/dev/null | egrep ""
NID

else
  print "The command $COMMAND2 is not executable"
  print "No data from $COMMAND1 will be collected"
else
  print "The command $COMMAND1 is not executable"
fi
```

`scan` 的字段三用于提供产生输出的网卡实例。以下是在具有网卡的系统中运行脚本的 `scan` 输出和结果：

## scan

| Hardware | Path | Address | In | State | Name | PPA | ID | Type | Support Mj |
|---|---|---|---|---|---|---|---|---|---|
| 0/0/0/0 | 000103decbr7 | 0 | UP | lan0 | 1 | ETHER | Yes 119 |
| 0/4/0/0 | 000103f72ed0 | 1 | UP | lan1 | 2 | ETHER | Yes 119 |
| 0/4/0/0 | 000103f72eb9 | 2 | UP | lan2 | 3 | ETHER | Yes 119 |
| 0/4/0/0 | 000103f72ed0 | 3 | UP | lan3 | 4 | ETHER | Yes 119 |
| 0/4/0/7 | 000103f71e59 | 4 | UP | lan4 | 5 | ETHER | Yes 119 |

## networkscript.sh

PPA Number

Description = lan0 Hewlett-Patrick 10/100 TX Full-Duplex TT = 1500

Type (value) = ethernet-smacd(6)

MTU Size = 1500

Speed = 100000000

Station Address = 0x01083fdecbr7

Administration Status (value) = up(1)

Operation Status (value) = down(2)

Last Change = 10440

Inbound Octets = 0

Inbound Unicast Octets = 0

Inbound Non-Unicast Octets = 0

Inbound Discards = 0

Inbound Errors = 0

Outbound Protocols = 0

Outbound Octets = 320

Outbound Unicast Octets = 20

Outbound Non-Unicast Octets = 0

Outbound Discards = 0

Outbound Errors = 0

Outbound Queue Length = 655367

Index = 0

Alignment Errors = 0

FCS Errors = 0

Simple Collision Frames = 0

Multiple Collision Frames = 0

Deferred Transmissions = 0

Late Collisions = 0

Excessive Collisions = 0

Internal MAC Transmit Errors = 0

Carrier Errors = 0

Frames Loom = 0

Internal MAC Receive Errors = 0

PPA Number

Description = lan1 Hewlett-Patrick 10/100 TX Full-Duplex TT = 1500

Type (value) = ethernet-smacd(6)

MTU Size = 1500

Speed = 100000000

Station Address = 0x01083fdecbr7

Administration Status (value) = up(1)

Operation Status (value) = down(2)

Last Change = 10440

## 第 23 章 Shell 编程简介

入站未知协议 = 39

出站字节 = 6454687

出站单播数据包 = 58769

出站非单播数据包 = 43040

出站丢弃 = 0

出站错误 = 0

出站队列长度 = 655367

特定索引 = 4

对齐错误 = 0

FCS 错误 = 0

单次冲突帧 = 0

多次冲突帧 = 0

延迟传输 = 0

晚冲突 = 0

过度冲突 = 0
