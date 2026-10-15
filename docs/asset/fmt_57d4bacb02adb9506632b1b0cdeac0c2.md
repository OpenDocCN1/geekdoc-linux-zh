
```
root@solaris:~# zoneadm list -v
ID NAME        STATUS    PATH          BRAND    IP
0 global       running   /             solaris  shared
1 firstzone    running   /zones/firstzone solaris  excl
```

```
root@solaris:~# dladm show-link
LINK          CLASS    MTU    STATE    OVER
net0          phys     1500   up       --
vboxnet0      phys     1500   up       --
firstzone/net0 vnic     1500   up       net0
```

## 14. 登录新区域，检查操作系统的名称。

```
root@solaris:~# zlogin firstzone
[Connected to zone 'firstzone' pts/2]
Oracle Corporation    SunOS 5.11 11.2 June 2014
root@firstzone:~# uname -a
SunOS firstzone 5.11 11.2 i86pc i386 i86pc
```

## 15. 检查分配给 firstzone 的 IP 地址。这将是你从主机机器、你的局域网或互联网访问该区域时使用的 IP 地址。IP 地址的前三个字段，192.168.0，表示子网。

```
root@firstzone:~# ipadm show-addr
ADDR OBJ    TYPE    STATE    ADDR
lo0/v4      static  ok       127.0.0.1/8
net0/v4     dhcp    ok       192.168.0.25/24
lo0/v6      static  ok       ::1/128
net0/v6     addrconf ok      fe80::8:20ff:fe86:6094/10
```

## 16. 此命令显示自动创建的 net0 VNIC。

```
root@firstzone:~# dladm show-link
LINK    CLASS    MTU    STATE    OVER
net0    vnic     1500   up       ?
```

## 17. 列出从区域内部可用的 ZFS 数据集。

```
root@firstzone:~# zfs list
NAME              USED    AVAIL    REFER    MOUNTPOINT
rpool             899M    889G     144K     /rpool
rpool/ROOT        897M    889G     144K     legacy
rpool/ROOT/
solaris           897M    889G     819M     /
rpool/ROOT/solaris/
var               68.7M   889G     67.5M    /var
rpool/VARSHARE    1.41M   889G     1.12M    /var/share
rpool/VARSHARE/
pkg               296K    889G     152K     /var/share/pkg
rpool/VARSHARE/pkg/ repositories 144K 889G 144K /var/share/pkg/ repositories
rpool/export 456K 889G 152K /export
rpool/export/home 304K 889G 152K /export/home
rpool/export/home/bob 152K 889G 152K /export/home/bob
```

## 18. 注销 firstzone 区域。

```
root@firstzone:~# exit

logout

[Connection to zone 'firstzone' pts/2 closed]
```

## 19. 再次登录 firstzone。

```
root@solaris:~# zlogin firstzone

[Connected to zone 'firstzone' pts/2]

Oracle Corporation SunOS 5.11 11.2 June 2014

root@firstzone:~#
```

## 20. Ping 主机。

```
root@firstzone:~# ping 192.168.0.25

192.168.0.25 is alive
```

## 21. 注销 firstzone。

```
root@firstzone:~# exit

logout

[Connection to zone 'firstzone' pts/2 closed]

root@solaris:~#
```

结论：使用 `zone.cfg` 和 `zoneadm` 命令，我们创建了一个名为 `firstzone` 的新区域，并能够检查其与主机系统的连接。

## 练习 25.5

在纸上绘制图 25.1，比书中显示的略大一些。然后在你的绘图上标注示例 25.4 中使区域进入图 25.1 中所示任何状态的步骤编号。

## 25.3.4 在区域中安装 Web 服务器应用程序

## 示例 25.5：在区域中安装 Web 服务器应用程序

目标：创建一个用于安装 Web 服务器应用程序的新 Solaris 区域，并将 Apache Web 服务器应用程序安装到该区域中。

介绍：使用与示例 25.4 相同的方法，我们创建一个名为 `appzone` 的新 Solaris 区域。然后，我们展示如何安装 Apache Web 服务器到

that new zone. The example details the use of the `pkg install` command to do the installation.

We do not show the detailed use of the Apache web server.

## Prerequisites:
- 1. You must have completed Example 25.4.
- 2. Your Solaris system must be connected to the Internet, and you must have access to an Oracle Solaris IPS online repository.

Procedures: Do the following steps, in the order presented here, to meet the objectives of this example.

- 1. Create a zone, named `appzone`, using a minimum amount of information.

```
root@solaris:~# zonecfg -z appzone "create ; set zoneroot=/zones/appzone"
```

- 2. Use the `zonecfg` command to get information about the new zone.

```
root@solaris:~# zonecfg -z appzone info

zonename: appzone

zoneroot: /zones/appzone

...

Output truncated...
```

- 3. Install the zone, as in Example 25.4, from an online Oracle IPS repository.

```
root@solaris:~# zoneadm -z appzone install

The following ZFS file system(s) have been created:

 rpool/zones/appzone

Progress being logged to /var/log/zones/

zoneadm.20141017T110817Z.appzone.install

 Image: Preparing at /zones/appzone/root.

 Install Log: /system/volatile/install.4635/install_log

 AI Manifest: /tmp/manifest.xml.YJ4abj

 SC Profile: /usr/share/auto_install/sc_profiles/enable_sci.xml
```
