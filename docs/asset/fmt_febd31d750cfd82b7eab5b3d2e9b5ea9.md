
`104959 S 0:02.01 tftpd /tftp`

`104958 S 0:01.25 tftpd /tftp`

[sheridan]

```bash
# ps -A | grep tftp | grep -v grep
```

## 16.10.7.2 in_multi 属性

`in_single` 最常用的替代方案是 `in_multi`。该属性表示，如果服务已经运行在一个集群成员上，且客户端请求第二个实例，则服务可能在另一个集群成员上运行。因此，服务可能运行在多个成员上。选择运行服务器的集群成员将由最高的 `sel` 决定。如果有多个具有相同 `sel` 的成员，则在切换到具有相等 `sel` 的集群成员之前使用这些成员。除非所有高 `sel` 的成员都宕机或不可用，否则不会使用低 `sel` 的集群成员。

以下示例将 `in_single` 属性替换为 `in_multi` 属性。因此我们可以在两个成员上看到 `tftpd`。示例使用了默认集群别名（`babylon5`）。默认情况下，集群别名的 `sel` 为 3。对于此示例，将其改为 1，以便更容易查看 `in_multi` 属性的结果。

[molari]

```bash
# clumagr -s babylon5 | grep sel
memberid: 1, selw=3, selpi=1 JOINED
memberid: 2, selw=3, selpi=1 JOINED
```

[molari]

```bash
# clumagr -a=babylon5,selw=1
```

[molari]

```bash
# clumagr -s babylon5 | grep sel
memberid: 1, selw=1, selpi=1 JOINED
memberid: 2, selw=1, selpi=1 JOINED
```

[sheridan]

```bash
# clumagr -a=babylon5,selw=1
```

[sheridan]

```bash
# clumagr -s babylon5 | grep sel
memberid: 1, selw=1, selpi=1 JOINED
memberid: 2, selw=1, selpi=1 JOINED
```

接下来我们将服务更改为 `in_multi`。

[molari]

```bash
# grep tftp /etc/clua_services
tftp          69/udp          in_single
```

[molari]

```bash
# sed 's/single/multi/' /etc/clua_services > /etc/clua_services.temp
```

[molari]

```bash
# mv /etc/clua_services.temp /etc/clua_services
```

[molari]

```bash
# grep tftp /etc/clua_services
      in_multi
tftp        69/udp
```

在客户端，我们运行几个 `tftp` 命令并查看哪些集群成员属于该服务。结果显示两个集群成员都运行着 `tftpd` 服务器实例。这是由于应用于 `tftp` 服务的 `in_multi` 服务属性而允许的。将 `in_multi` 理解为入站请求可以在多个成员上处理。

从客户端系统：

```bash
# rsh molari ps -A | grep tftp | grep -v grep
# rsh sheridan ps -A | grep tftp | grep -v grep
# tftp babylon5 -get /tftp/big1 /dev/null & [1] 50390
# tftp babylon5 -get /tftp/big1 /dev/null & [2] 50366
# rsh molari ps -A | grep tftp | grep -v grep
104959 S 0:02.01 tftpd /tftp
# rsh sheridan ps -A | grep tftp | grep -v grep
525680 S 0:05.13 tftpd /tftpd
```

## 16.10.7.3 in_noalias 属性

另一种替代属性是 `in_noalias`。在服务上设置此属性表示，如果客户端使用集群别请求服务，则该服务不可用。注意，`in_single`、`in_multi` 和 `in_noalias` 是互斥的属性。这意味着对于特定服务只能应用这三个属性之一。如果您不小心设置了具有不兼容属性的服务，`clamgr -f` 命令将拒绝该属性并发出错误信息。以下示例显示了当尝试应用不兼容的 `in_noalias` 和 `in_multi` 组合时会发生什么。

```bash
# grep tfftp /etc/clua_services
tftp        69/udp                in_noalias,in_multi
```

```bash
# cluamgr -f
Illegal option supplied
service file entry: tfftp        69/udp                in_noalias,in_multi
```

以下示例显示，将 `in_noalias` 服务属性应用于 `tfftp` 服务，可以防止当客户端使用集群访问该服务时，`tftpd` 守护进程得以运行。如果客户端使用实际成员名称而非别名请求服务，则 `in_noalias` 属性将不起作用。

从客户端系统：

```bash
# rsh molari grep tfftp /etc/clua_services
tftp        69/udp                in_noalias
```

两个集群上目前均没有 `tfftp` 活动。

```bash
# rsh molari ps -A | grep tfftp | grep -v grep
# rsh sheridan ps -A | grep tfftp | grep -v grep
```

尝试使用集群别名获取一些 `tfftp` 活动。

```bash
# tfftp babylon5 -get /tftp/big1 /dev/null &
[1]        5118
```

```bash
# tfftp babylon5 -get /tftp/big1 /dev/null &
[2]        5119
```

由于 `in_noalias` 服务属性的作用，没有成功。

```bash
# rsh molari ps -A | grep tfftp | grep -v grep
# rsh sheridan ps -A | grep tfftp | grep -v grep
```

现在尝试使用实际集群成员名称（而非别名）获取一些 `tfftp` 活动。

```bash
# tfftp molari -get /tftp/big1 /dev/null &
[1]        5139
```

由于我们使用了实际成员名称，`tftpd` 守护进程在 `molari` 上启动。我们的请求没有受 `in_noalias` 属性的影响。

```bash
# rsh molari ps -A | grep tftp | grep -v grep
1049745 ?? S 0:01.70 tftpd /tftp
```

## 16.10.7.4 in_nolocal 属性

正如你（希望）记得的，集群别名提供了一个额外的 IP 地址，通过该地址可以访问集群服务。你可能希望限制对服务的访问，要求客户端必须使用集群别名来访问该服务。在服务上附加 `in_nolocal` 属性表示除非使用别名，否则无法访问该服务。这意味着使用任何成员的本地 IP 接口地址（或节点名称）都无法访问任何带有 `in_nolocal` 属性的服务。

以下示例首先显示了客户端使用集群别名成功访问服务，然后显示了由于 `tftp` 服务应用了 `in_nolocal` 属性而导致尝试失败。

从客户端系统：

```bash
# rsh sheridan grep tftp /etc/clua_services
tftp 69/udp in_multi,in_nolocal
```

使用集群别名启动一些 `tftp` 活动。效果非常完美。

```bash
# tftp babylon5 -get /tftp/big1 /dev/null &
[1] 51882
```

```bash
# rsh molari ps -A | grep tftp | grep -v grep
1049867 ?? S 0:00.00 tftpd /tftp
```

尝试使用成员名称启动一些 `tftp` 活动。由于 `in_nolocal` 属性，没有成功。

```bash
```
