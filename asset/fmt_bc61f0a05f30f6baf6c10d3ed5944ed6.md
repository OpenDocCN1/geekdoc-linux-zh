
`ipchains -A input -s $EXTERNAL_INTERFACE -s $CLASS_B -j $DENY`

`ipchains -A input -s $EXTERNAL_INTERFACE -d $CLASS_B -j $DENY`

`ipchains -A input -s $EXTERNAL_INTERFACE -s $CLASS_B -j $REJECT`

`ipchains -A input -s $EXTERNAL_INTERFACE -d $CLASS_B -j $REJECT`

```bash
# 拒绝声称来自或来自 C 类私有网络的包

ipchains -A input -s $EXTERNAL_INTERFACE -s $CLASS_C -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -d $CLASS_C -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s $CLASS_C -j $REJECT

ipchains -A input -s $EXTERNAL_INTERFACE -d $CLASS_C -j $REJECT
```

```bash
# 拒绝声称来自回环接口的包

ipchains -A input -s $EXTERNAL_INTERFACE -s $LOOPBACK -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s $LOOPBACK -j $REJECT
```

```bash
# 拒绝广播地址包

ipchains -A input -s $EXTERNAL_INTERFACE -s $BROADCAST_DEST -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -d $BROADCAST_SRC -j $DENY
```

```bash
# 拒绝 D 类多组地址 (in.h) (NET-3-HOWTO)
# 多组地址作为源地址是非合法的
# 多组地址使用 UDP

ipchains -A input -s $EXTERNAL_INTERFACE -s $CLASS_D_MULTICAST -j $DENY
```

```bash
# 拒绝保留的 IP 地址

ipchains -A input -s $EXTERNAL_INTERFACE -s $CLASS_RESERVED -j $DENY
```

```bash
ipchains -A input -s $EXTERNAL_INTERFACE -s 1.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 2.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 5.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 7.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 23.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 27.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 31.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 37.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 39.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 42.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 48.0.0.0/4 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 56.0.0.0/7 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 60.0.0.0/8 -j $DENY
```

```bash
# 65.000001/3 包含了 64 - 65-79 范围

ipchains -A input -s $EXTERNAL_INTERFACE -s 65.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 66.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 67.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 68.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 69.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 70.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 71.0.0.0/8 -j $DENY

ipchains -A input -s $EXTERNAL_INTERFACE -s 72.0.0.0/8 -j $DENY
```

```bash
ipchains -A input -i EXTERNAL_INTERFACE -s 73.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 74.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 75.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 76.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 77.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 78.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 79.0.0.0/8 -j $DENY

# 80: 01010000 /4 掩码 80

ipchains -A input -i EXTERNAL_INTERFACE -s 80.0.0.0/4 -j $DENY

# 96: 01100000 /4 掩码 96

ipchains -A input -i EXTERNAL_INTERFACE -s 96.0.0.0/4 -j $DENY

# 126: 01111110 /3 包含了 127-128 范围

ipchains -A input -i EXTERNAL_INTERFACE -s 112.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 113.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 114.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 115.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 116.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 117.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 118.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 119.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 120.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 121.0.0.0/8 -j $DENY

ipchains -A input -i EXTERNAL_INTERFACE -s 122.0.0.0/8 -j $DENY
```
