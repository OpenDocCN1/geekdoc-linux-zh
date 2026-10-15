
| crw------ | 1 | root | system | 7, | Jul 26 2021 | sysdump |
| crw------ | 1 | root-- system | 7, | Jul 26 2021 | sysdumpctl |
| crw------ | 1 | root | system | 7, | Jul 26 2021 | sysdumpnull |
| crw-rw-rw | 1 | root | system | 5, | Jul 26 2021 | systrace |
| crw-rw-rw | 1 | root | system | 5, | Jul 26 2021 | scisitrl |
| crw-rw-rw | 1 | root | system | 1, | Jul 24 17:53 | tty |
| crw--w--w | 1 | root | system | 18, | Jul 24 17:58 | tty0 |
| crw-rw-rw | 1 | root | system | 19, | Jun 23 15:18 | tty1 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | tty0 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | ttypl |
| crw-rw-rw | 1 | root | system | 2, | Jul 26 2021 | zero |

# 获取系统快照 355

## 系统定义的 SSA 磁盘

```
################################
系统带驱动
rmt0 可 00-00-OS-5,0 5.0 GB 8mm 磁驱动
################################
系统 CD-ROM 驱动
cd0 可 00-00-OS-6,0 SCSI 多媒体 CD-ROM 驱动
################################
```

## 系统中的适配器

```
sio0 可 00-00 标准 I/O 平板
fda0 可 00-00-OD 标准 I/O 磁盘适配器
siota0 可 00-00-OK 键盘适配器
sa0 可 00-00-SI 标准 I/O 串口 1
sal 可 00-00-S2 标准 I/O 串口 2
scsi0 可 00-00-OS 标准 SCSI I/O 控制器
siota0 可 00-00-0T 平板适配器
cimma0 可 00-00-GM 鼠标适配器
ppa0 可 00-00-0P 标准 I/O 并口适配器
ent0 可 00-00-03 以太网高性能局域网适配器 (8ef5)
```

## 网络路由

### 路由表

| 目的地 | 网关 | 标志 | 引用 | 用量 | PMTU | 期组 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| default | 10.10.10.2 | UCG | 0 | 0 | en0 | |
| 10.10/16 | 10.10.10.1 | U | 37 | 135807 | en0 | |
| 127/8 | 127.0.0.1 | U | 5 | 264 | lo0 | |

协议族 2 (Internet) 的路由树：
协议族 24 (Internet v6) 的路由树：

```
:::1               :1               UH    0 0 loo 16896 -
```

列表 13.3 运行中的 AIsysconfig.ksh 壳脚本。（续）

## 网络接口统计

```
############################################################
| 名称 | Mtu | 地址 | 入数据包 | 入错误 | 出数据包 | 出错误 | 冲突 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| en00 | 1500 | link2 | 2.60.8c.2d.75.bi | 112330 | 0 | 108697 | 0 | 0 |
| en00 | 1500 | 10.10.yogi | 112330 | 0 | 108697 | 0 | 0 |
| loo | 16896 | link#1 | 28302 | 0 | 28304 | 0 | 0 |
| loo | 16896 | 127 loopback | 28302 | 0 | 28304 | 0 | 0 |
| loo | 16896 | :: | 28302 | 0 | 28304 | 0 | 0 |
############################################################
```

## 文件系统统计

| 文件系统 | 1024-块 | 空闲 | 已用 % | 已用 | 剩余用 % | 挂载点 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hd4` | 32768 | 10924 | 67% | 1854 | 12% | `/` |
| `/dev/hd2` | 1449984 | 61680 | 96% | 40941 | 12% | `/usr` |
| `/dev/hd9var` | 53248 | 10568 | 81% | 63 | 6% | `/var` |
| `/dev/hd3` | 106496 | 70184 | 35% | 223 | 1% | `/tmp` |
| `/dev/hd1` | 4096 | 3982 | 5% | 55 | 6% | `/home` |
| `/proc` | | | | | | `/` |
| `/dev/hd10opt` | 665360 | 14660 | 98% | 16260 | 10% | `/opt` |
| `/dev/scripts_lv` | 102400 | 25296 | 76% | 887 | 4% | `/scripts` |
| `/dev/lv_temp` | 409600 | 350456 | 15% | 26 | 1% | `/tmpfs` |

## 挂载信息

| 节点 | 挂载 | 覆盖 | vfs | 日期 | 选项 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hd4` | `/usr` | jfs | Jul 23 18:56 | rw,log=`/dev/hd8` |
| `/dev/hd2` | `/` | jfs | Jul 23 18:56 | rw,log=`/dev/hd8` |
| `/dev/hd9var` | `/var` | jfs | Jul 23 18:56 | rw,log=`/dev/hd8` |
| `/dev/hd3` | `/tmp` | jfs | Jul 23 18:56 | rw,log=`/dev/hd8` |
| `/dev/hd1` | `/home` | jfs | Jul 23 18:57 | rw,log=`/dev/hd8` |
| `/proc` | `/proc` | profs | Jul 23 18:57 | rw |
| `/dev/hd10opt` | `/opt` | jfs | Jul 23 18:57 | rw,log=`/dev/hd8` |
| `/dev/scripts_lv` | `/scripts` | jfs | Jul 23 18:57 | rw,log=`/dev/hd8` |
| `/dev/lv_temp` | `/tmpfs` | jfs | Jul 23 18:57 | rw,log=`/dev/hd8` |

## 定义卷组

`rootvg`

13.3 AIsysconfig.ksh 壳脚本运行。（续）

逻辑卷信息按卷组：

| LV 名称 | 类型 | PPS | LV 状态 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- |
| hnd5 | boot | 2 | closed | N/A |
| hnd6 | paging | 84 | 1 | N/A |
| hnd8 | jfs | 1 | 1 | N/A |
| hnd4 | jfs | 8 | 1 | `/` |
| hnd2 | jfs | 354 | 2 | `/user` |
| hnd9 | jfs | 13 | 2 | `/var` |
| hnd3 | jfs | 26 | 1 | `/tmp` |
| hnd1 | jfs | 1 | 1 | `/home` |
| hnd10 | jfs | 160 | 2 | `/opt` |
| scripts_lv | jfs | 25 | 1 | `/scripts` |
| lv_temp | jfs | 100 | 1 | `/tmpfs` |

分页空间

| 物理卷 | 卷组 | 大小 | 已用 % |
