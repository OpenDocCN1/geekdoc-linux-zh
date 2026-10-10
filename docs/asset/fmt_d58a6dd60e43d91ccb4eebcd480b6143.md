
```bash
#! /bin/sh
# 以下是用户可配置的部分。
dial=/usr/sbin/dial
FIFO=""

./etc/init.d/functions

# 在配置文件中查找 fifo
NEW_FIFO=`egrep '^fifo' /etc.options | sed -e 's/fifo//
# 前一行导致脚本搜索配置文件中描述 FIFO 的正则表达式。如果没有选项文件，我们不会启动它。
test -x /usr/sbin/dial || exit 0
test -f /etc.options || exit 0

# 脚本剩余部分是对命令行参数的处理。
if [ "$NEW_FIFO" != "" ]; then
  # 用户位置存在且是一个命名管道
  FIFO=$NEW_FIFO;
  case "$1" in
  start)
    echo -n "按需启动守护进程: "
    if [ "$FIFO" != "" ]; then
      if test -p $FIFO; then
        rm -f $FIFO
      fi
      mknod --mode=660 $FIFO
      chown root.dialout $FIFO
      if test -p $FIFO; then
        echo -n "fifo 已创建"
      fi
    fi
    start-stop-daemon --start --quiet \
      --pidfile /var/run/dial.pid --exec /usr/sbin/dial
    echo "拨号中..."
    ;;
  stop)
    echo -n "按需停止守护进程: "
    if [ "$FIFO" != "" ]; then
      if test -p $FIFO; then
        rm -f $FIFO
        echo -n "fifo 已移除"
      fi
    fi
    start-stop-daemon --stop --quiet \
      --pidfile /var/run/dial.pid --exec /usr/sbin/dial
    echo "拨号中..."
    ;;
  reload)
    if [ "$FIFO" != "" ]; then
      if test -p $FIFO; then
        echo "reset" > $FIFO
        echo "拨号配置已重载。"
      else
        echo "无法重载拨号配置: 未找到 FIFO。"
        exit 2
      fi
    else
      echo "无法重载 diald 配置: "
      echo "需要在 /etc/diald/diald.options 中添加 fifo 语句。"
      exit 2
    fi
    ;;
  force-reload|restart)
    echo -n "正在停止 diald... "
    pid=`cat /var/run/dial.pid`
    start-stop-daemon --stop --pidfile /var/run/dial.pid \
      --exec /usr/sbin/dial
    while ps $pid >/dev/null 2>/dev/null
    do
      echo -n "等待中... "
      sleep 5
    done
    echo "完成。"
    start-stop-daemon --start --quiet \
      --pidfile /var/run/dial.pid --exec /usr/sbin/dial
    echo "Diald 已重启。"
    ;;
  *)
    echo "用法: /etc/init.d/diald (start|stop|reload|restart|force-reload)"
    exit 1
    ;;
esac
exit 0
```

# dosplashFX

此脚本在启动过程中向启动屏幕上打印不同的消息。

在当前配置下，它只打印“正在初始化....”的消息。

```bash
#!/bin/sh
###########################################
#Name : dosplashFX
#
#Description: 管理启动屏幕
#
#Copyright (C) 1999 Corel Corporation
#
# EXHIBIT A -Corel Public License
#
```

## 附录 D: 初始化脚本

# 576 Corel Linux 操作系统入门套件：官方指南

```bash
#!/bin/sh
###########################################
#Name : dosplashFX
#
#Description: 管理启动屏幕
#
#Copyright (C) 1999 Corel Corporation
#
# EXHIBIT A -Corel Public License:
#
```

此文件的内容受 Corel 公共许可限制。

```bash
Version 1.0 (the "License"); you may not use this file except in
# compliance with the License. You may obtain a copy of the License at
# linux.corel.com/license.
# 根据许可协议分发的软件按“原样”基础分发，
# 不提供任何形式的明示或暗示担保。请查看许可协议
# 以了解规定的权利和限制。
# 原始代码是 splashFX。
# 原始代码开发者是 Corel Corporation。
# Corel 创建的部分版权所有 (C) 1999 保留所有权利。
# 贡献者：
################################

/sbin/splashFX install
/sbin/splashFX say " 正在初始化...\n
```

# halt

`halt` 脚本控制 Linux 系统由管理员停止时各种函数的停止以及函数的停止顺序。

```bash
#! /bin/sh
# halt
# 执行 halt 命令。
# 版本: @(# halt 2.75 19-May-1998 miquels@cistron.nl
#

PATH=/sbin/bin:/usr/sbin:/usr/bin

# 检查是否需要切断。
if [ -x /etc/init.d/ups-monitor ]
then
    /etc/init.d/ups-monitor poweroff
fi

halt -d -f -i -p
```

# hostname.sh

`hostname.sh` 脚本正如其名，用于计算机的主机名。

## 附录 D：初始化脚本

```bash
#
# hostname.sh    设置主机名。
# 版本: @(#)hostname.sh 1.00 22-Jun-1998 miquels@cistron
#
```

```bash
hostname --file /etc/hostname
```

### hwclock.sh

`hwclock.sh` 脚本比较主板上的硬件时钟与操作系统维护的系统时钟，并在必要时更改设置。

```bash
# hwclock.sh    根据 /etc/default/rcS 中的 UTC 设置
# 设置并调整 CMOS 时钟（另见 rcS(5)）。
# 版本: @(#)hwclock.sh 2.00 14-Dec-1998 miquels@cistron
#
```
