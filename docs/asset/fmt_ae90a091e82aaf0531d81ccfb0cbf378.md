
## Section 4: IPX-devices (strongly recommended)

```
# =================================================================
# Section 4: IPX-devices (strongly recommended)
#
# This section contains information for the ipx-router built into mars_nwe
# and/or the external program "nwrouted".
#
# Both processes exchange the ipx-packets between your machine and the rest
# of the world (in other words: their functionality is essential). Of
# course, to use one of both is already sufficient.
#
# Note for people with other IPX/NCP servers on the net:
# - choose the same frame-type as the other servers use
# - make sure your network-number is not already in use by another
# server (see the output of slist under Linux or DOS)
#
# Under Linux, it is possible to let the kernel detect all values
# automatically for you. This is only possible (and only makes sense then)
# if there are other IPX/NCP servers on the same net which are setup
# correctly.
#
# .......................................................................
#
# Syntax:
# 4 NET_NUMBER DEVICE FRAME TICKS
#
# NET_NUMBER: this number is determined by the router of the physical
# network you're attached to. Use '0x0' to let the
# linux-kernel determine your network number by listening
# on the local network
# DEVICE: the network-interface associated with the NET_NUMBER. Use
# a "*" (star) to automatically setup all devices at once.
# FRAME: the frame-type of the data-packets on your local network.
# Possible values are:
# ethernet_ii
# 802.2
# 802.3 (default)
# snap
# token
# auto automatic detection of the frame-type used
# in your ipx-environment
# TICKS: the time data-packets need to get delivered over a
# certain interface. If your connection goes through several
# routers, the shortest path can be determined by summing up
#
```

### 列表 18.4 继续

```
#  all ticks for every route and compare the results.
#  (1 tick = 1/18th second)
#  ...............................................................
#
# Examples:
#  4      0x0    *      AUTO    1      # automatic setup
#  4      0x10   eth0   802.3   1      # manual setup
#
#  4      0x10   eth0   802.3   1
#  4      0x0    *      802.3   1
```

在第 4 节中，你定义使用的帧类型，正如前面所述，它定义了在你的局域网段中哪些机器被视为同一网络的一部分。如果你的 NetWare 仿真器是网络上唯一的服务器，你可以通过使用示例中的自动设置行来允许软件自行配置。如果它不是网络上唯一的服务器，你应咨询你的 NetWare 管理员以确定正确的值。

`/etc/nwsrv.conf` 文件的第 5 节，如列表 18.5 所示，是一个布尔标志，告诉服务器是否在服务器软件的每次调用之间保存路由信息。

### 列表 18.5 `/etc/nwsrv.conf` 文件第 5 节—保存 IPX 路由标志

```
# ==============================================================
# Section 5: Saving of ipx-routes (required)
#
# This entry controls if the information regarding the ipx-routes should be
# saved beyond the lifetime of the server.
#
# ...............................................................
#
# Syntax:
#     5      SAVE_FLAG
#
# SAVE_FLAG:
#  0      don't save routes (default)
#  1      do save routes
# ...............................................................
#
5  0
```

同样，除非你的 NetWare 网络上有特别复杂的路由方案，否则可能没有理由更改第 5 节参数的值。

`/etc/nwsrv.conf` 文件的第 6 节确定我们将仿真的 NetWare 版本。本节如列表 18.6 所示。

### 列表 18.6 `/etc/nwsrv.conf` 文件第 6 节—版本欺骗

```
# ==================================================
# Section 6: version-"spoofing"
#
# Some clients work better if the server tells that it is a 3.11 Server,
# although many calls (namespace services) of a real 3.11 Server are
# missing yet.
# To test the namespace calls, this entry must be set to > 0 and `config.h`
# must be altered before compiling "mars_nwe".
#
# ............................................................
#
# Syntax:
# 6 SERVER_VERSION
#
# SERVER_VERSION: the version-number reported to DOS-clients
# 0 Version 2.15 (default)
# 1 Version 3.11
# 2 Version 3.12 (not implemented yet)
# ............................................................
#
6 0
```

你在第 6 节中设置的值有助于向客户端定义你的功能。如列表 18.6 所示，默认值是最安全的选择；然而，如果你遵循 IPX-HOWTO 中的示例，你将把此参数的值设置为 1 以使用 3.11 版本。

配置文件中如列表 18.7 所示的下一节设置密码处理策略。语法是节号后跟一个数字标志，该标志指定 DOS 客户端的密码将如何处理。列表中的注释解释了可能数值值的含义。

### 列表 18.7 `/etc/nwserv.conf` 文件的第 7 节—DOS 客户端密码处理
