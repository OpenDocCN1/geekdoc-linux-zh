

```
[bob@pcbsd-1233] /usr/home/bob# iocage list
JID UUID BOOT STATE TAG
- 44599667-9574-11e5-9cc9-08002738ba74 off down bobsecond
- 527c21ff-9573-11e5-9cc9-08002738ba74 off down
2015-11-27@17:57:04
```

新 jail 的名称为 bobsecond，其引用 UUID 为 44599667-9574-11e5-9cc9-08002738ba74。

## EXERCISE 25.2

与示例 25.1 中所示的步骤类似，在你的系统上创建一个轻量级 jail。用你自己的唯一名称为 jail 命名或标记。然后使用 zfs list 命令显示该 jail 的 ZFS 文件系统及其挂载点。该 jail 的大小是多少字节？

### Example 25.2: Listing Jails and Starting Them Automatically at System Boot

如示例 25.1 所示，以下命令列出当前 jails 的信息：

```
# iocage list
JID UUID BOOT STATE TAG
- 44599667-9574-11e5-9cc9-08002738ba74 off down bobsecond
```

可以看到 boot 标志为 off。这意味着 jail 不会在启动时启动。STATE 标识符表示 jail 未启动或处于非活动状态。

在系统启动时自动启动 jail：要允许 iocage 在启动时启动你的 jail，请在 /etc/rc.conf 中添加以下行：

```
iocage_enable="YES"
```

可以使用以下命令将单个 jail 标记为在系统启动时启动：

```
# iocage set boot=on bobsecond
```

你可以通过设置其优先级来指定 jail 的启动顺序：

```
# iocage set priority=20 bobsecond
```

值越低表示启动优先级越高，即更早启动 jail。

## EXERCISE 25.3

对于你在章节练习 25.2 中创建的 jail，修改其属性使其在系统启动时自动启动。然后重新启动系统以查看 jail 是否自动启动。

### Example 25.3: Looking Into, Starting, Stopping, and Destroying a Jail

你可以在不启动或运行 jail 的情况下 chroot 进入你的 jail：

```
# iocage chroot bobsecond
root@pcbsd-1233: / #
```

这对于修改 jail 很有用。使用 ls 命令探索 jail：

```
root@pcbsd-1233:/ # ls
.cshrc  bin   etc   media  rescue  sys   var
.profile boot  lib   mnt    root    tmp
COPYRIGHT dev libexec proc  sbin    usr
root@pcbsd-1233:/ #
```

查看网络连接的配置方式：

```
root@pcbsd-1233:/ # ifconfig
em0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> metric 0 options=9b<RXCSUM,TXCSUM,VLAN_MTU,VLAN_HWTAGGING,VLAN_HWCSUM>
ether 08:00:27:38:ba:74
inet6 fe80::a00:27ff:fe38:ba74%em0 prefixlen 64 scopeid 0x1
inet 192.168.0.16 netmask 0xffffffff broadcast 192.168.0.255
nd6 options=23<PERFORMNUD,ACCEPT_RTADV,AUTO_LINKLOCAL>
media: Ethernet autoselect (1000baseT <full-duplex>)
status: active
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> metric 0 mtu 16384
options=600003<RXCSUM,TXCSUM,RXCSUM_IPV6,TXCSUM_IPV6>
inet6 ::1 prefixlen 128
inet6 fe80::1%lo0 prefixlen 64 scopeid 0x2
inet 127.0.0.1 netmask 0xff000000
nd6 options=21<PERFORMNUD,AUTO_LINKLOCAL>
root@pcbsd-1233:/ #
```

要退出 chroot，请按 <CTRL-D> 或输入 exit。

启动 jail

```
[bob@pcbsd-1233] /usr/home/bob# iocage start bobsecond
* Starting 44599667-9574-11e5-9cc9-08002738ba74 (bobsecond)
+ Started (shared IP mode) OK
+ Starting services OK
[bob@pcbsd-1233] /usr/home/bob#
[bob@pcbsd-1233] /usr/home/bob# iocage list
JID          UUID                                 BOOT  STATE TAG
```

```
1 44599667-9574-11e5-9cc9-08002738ba74  off  up    bobsecond
- 527c21ff-9573-11e5-9cc9-08002738ba74  off  down
2015-11-27@17:57:04
[bob@pcbsd-1233] /usr/home/bob#
```

名为 bobsecond 的 jail 已启动。

访问 jail 控制台：此命令允许你在不登录的情况下访问 jail：

```
[bob@pcbsd-1233] /usr/home/bob# iocage console bobsecond
FreeBSD 10.2-RELEASE-p4 (GENERIC) #0: Tue Aug 18 15:15:36 UTC 2015
Welcome to FreeBSD!
Release Notes, Errata: https://www.FreeBSD.org/releases/
...
root@44599667-9574-11e5-9cc9-08002738ba74:~ #
```

你现在已如同在控制台登录一样进入了 jail。例如，我们现在可以手动启动 sshd。观察它如何自动创建缺失的密钥：

```
root@44599667-9574-11e5-9cc9-08002738ba74:~ # service sshd onestart
Generating RSA1 host key.
2048 09:c9:e8:a8:b3:dc:5b:e6:22:9c:a8:f4:6b:76:da:c7:10
root@44599667-9574-11e5-9cc9-08002738ba74 (RSA1)
Generating RSA host key.
2048 a4:03:c5:76:ed:41:80:77:20:3f:d6:99:89:37:4d
root@44599667-9574-11e5-9cc9-08002738ba74 (RSA)
Generating DSA host key.
1024 78:4b:04:4b:e8:f5:09:a5:5f:0e:71:02:b4:c6:b2:7b
root@44599667-9574-11e5-9cc9-08002738ba74 (DSA)
Generating ECDSA host key.
256 c7:98:87:dc:16:37:df:95:21:d0:24:04:75:a8:50:c3
root@44599667-9574-11e5-9cc9-08002738ba74 (ECDSA)
Generating ED25519 host key.
256 53:08:ac:52:d3:3e:ba:53:9e:ec:0b:c6:42:22:bc:c8
root@44599667-9574-11e5-9cc9-08002738ba74 (ED25519)
Performing sanity check on sshd configuration.
Starting sshd.
root@44599667-9574-11e5-9cc9-08002738ba74:~ #
```

检查网络配置：

```
root@44599667-9574-11e5-9cc9-08002738ba74:~ # ifconfig
em0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> metric 0 mtu 1500
```

