
```text
/var/log/apt/term.log { rotate 12 monthly notifempty }

/var/log/apt/history.log { rotate 12 monthly notifempty }
```

```text
/var/log/syslog

{
    rotate 7
    daily
    missingok
    notifempty
    delaycompress
    compress
    postrotate
        reload syslog >/dev/null >&1
    endscript
}

/var/log/mail.info
/var/log/mail.warn
/var/log/mail.err
/var/log/mail.log
/var/log/daemon.log
/var/log/kern.log
/var/log/auth.log
/var/log/user.log
/var/log/messages

{
    rotate 4
    weekly
    missingok
    delaycompress
    delaycompress
    sharedscripts
    postrotate
        reload syslog >/dev/null >&1
    endscript
}
```

```text
# 使用 Xft?
use_xft yes

# 启用 Xft 时
xftfont Ubuntu:size=9

# gap 是距离起始对齐像素数
minimum_size 10
gap_x 13
gap_y 45

# 文本对齐，其他可能的值已注释
alignment top_left
alignment top_right
alignment bottom_left
alignment bottom_right

# 添加空格以防止内容移动？这只影响对象
use_spacer right

# 从已用内存减去文件缓冲区
no_buffers yes

# 使用双缓冲（减少闪烁，对所有人都有效）
double_buffer yes

# 允许图标出现、窗口移动以及透明
own_window yes
own_window_type override
own_window_transparent yes

#own_window_hints docked,below,skip_taskbar

# 如果你想让 Conky 在后台运行，设置为 yes
background yes

# 更新间隔（秒）
update_interval 1

cpu_avg_samples 1

net_avg_samples 1

# -- 开始显示配置 -

$(align)${color #EA6B36}$sysname $kernel

$(align)${color #EA6B36}$exec cat /etc/issue.net on machine host $hostname

$(color #EA6B36} 时间:${color #E7E7E7} $time

$(color #EA6B36} 平均负载:${color #E7E7E7} $loadavg

$(color #EA6B36} 当前 CPU 使用率:${color #E7E7E7} $(color #EA6B36)CPU0:${color #E7E7E7} $(cpu cpu)

-- $(color #EA6B36)CPU1:${color #E7E7E7} $(cpu1)

-- $(color #EA6B36)CPU2:${color #E7E7E7} $(cpu2)

-- $(color #EA6B36)CPU3:${color #E7E7E7} $(cpu3)

-- $(color #EA6B36)CPU4:${color #E7E7E7} $(cpu4)

-- $(color #EA6B36)CPU5:${color #E7E7E7} $(cpu5)

-- $(color #EA6B36)CPU6:${color #E7E7E7} $(cpu6)

-- $(color #EA6B36)CPU7:${color #E7E7E7} $(cpu7)

$(color #EA6B36} 更新:

-- $(color #EA6B36}$exec 3000 /usr/lib/update-notifier.py

-- 人类可读格式

$(color #EA6B36}安全性:${color #E7E7E7}$exec 3000 /usr/lib/update-notifier.py --human-readable | grep security

$(color #EA6B36}状态:${color #E7E7E7}$(battery0)

$(color #EA6B36} CPU 使用率 $(color #E7E7E7}$(text name 1)$alignr$(text cpu 1) $(text mem)

$(color #E7E7E7)$text name 2)$alignr$(text cpu 2) $(text mem)

${color #EA6B36}

$(color #E7E7E7)$text name 3)$alignr$(text cpu 3) $(text mem)

$(color #EA6B36}内存使用

$(color #E7E7E7)$text name 1)$alignr$(text cpu 1) $(text mem)

$(color #E7E7E7)$text name 2)$alignr$(text cpu 2) $(text mem)

$(color #E7E7E7)$text name 3)$alignr$(text cpu 3) $(text mem)

$(color #EA6B36} RAM 使用率 $(color #E7E7E7)$mem%mem

$(color #EA6B36} 交换分区使用率 $(color #E7E7E7)$swap%swap

$(color #EA6B36} 进程 $(color #E7E7E7)$processes%swap

$(color #EA6B36} 运行中 $(color #E7E7E7)$running_processes

$(color #EA6B36} 硬盘:

$(color #E7E7E7)$fs_used /$fs_size $bar

/media/ $(color #E7E7E7)$fs_used /$fs_size /media/

$(color #EA6B36} 无线网络:

$(color #EA6B36} ESSID: $(color #E7E7E7)$wireless_essid wlan0

$(color #EA6B36} AP: $(color #E7E7E7)$wireless_ap wlan0

$(color #EA6B36}$exec iwconfig wlan0 | grep "Frequency" | cut -c24-44

$(color #EA6B36} 模式: $(color #E7E7E7)$wireless_mode wlan0

$(color #EA6B36} 比特率: $(color #E7E7E7)$wireless_bitrate wlan0

$(color #EA6B36} 本地 IP: $(color #E7E7E7)$addr wlan0

$(color #EA6B36} 链路质量: $(color #E7E7E7)$wireless_link_qual_perc wlan0

$(color #EA6B36} 总下载 $(color #E7E7E7)$totaldownload wlan0

$(color #EA6B36} 总上传 $(color #E7E7E7)$totalup wlan0

$(color #EA6B36} 下载速度 $(color #E7E7E7}$downpeed wlan0)$color #E7E7E7)

$${color #EA6B36} 上传速度: $(color #E7E7E7)$upspeed wlan0)

$(color #E7E7E7)$downspeed wlan0 15, 150 00000 0000ff)$alignr$

$(color #E7E7E7)$downspeed eth0 15, 150 0000ff ff0000)

$(color #EA6B36} 有线网络:

$(color #EA6B36} 本地 IP $(color #E7E7E7)$addr eth)

$(color #EA6B36} 总下载 $(color #E7E7E7)$toldown eth)

$(color #EA6B36} 总上传 $(color #E7E7E7)$totalup eth)
```
