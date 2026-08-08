# Bash 脚本示例：任务完成后关机（最终版 - FreeBSD 与 Linux）








以下 bash 脚本示例已 FreeBSD 和 Linux 上经过测试，两者均可正常运行。它使用了 `pgrep`（FreeBSD 上为 `sys-utils`，Linux 上为 `procs`）。或者在 Linux 上也可以使用 `pidof`。

```bash
#!/bin/sh # or #/usr/local/bin/bash For FreeBSD
#!/bin/bash # For Linux

## 创建锁
scriptname=$(basename $0)
pidfile=/tmp/$scriptname.lock
## 锁定
exec 200>$pidfile
lock -n 200 || exit 1
p=$$
echo Spid 1>&200

SERVICE="mplayer" # 在 mplayer 命令行上观看长视频
### CHECK="pidof "$SERVICE" # 同样运行良好
CHECK="pgrep -f "$SERVICE" >/dev/null 2>&1
if [ ! -z "$CHECK" ]; # 同样运行良好
then
### echo "$SERVICE is running..."
sleep 300s
else
### echo "$SERVICE is NOT running"
echo "Powering-off in next 3 minutes."
sleep 18s # 它适用于 sysVinit 和 systemd
## 释放锁
sudo rm -f$pidfile
sudo shutdown -p now # 对于 sysVinit shutdown -p +3
### sudo systemctl poweroff # 对于 systemd (未测试)
fi
exit 0
```

