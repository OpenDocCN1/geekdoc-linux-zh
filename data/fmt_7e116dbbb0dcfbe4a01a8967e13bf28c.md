
```
top -09:32:52 20 min, 2 users, load average: 0.18, 0.10, 0.03
Tasks: 112 total, 2 running, 110 sleeping, 0 stopped, 0 zombie
CPU(s): 7.8 us, 1.5 sy, 0.0 ni, 90.7 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
Mem: 1829.4 total, 1438.1 free, 172.7 used, 218.6 buff/cache
Swap: 1024.0 total, 1024.0 free, 0.0 used, 1498.7 avail
| PID PR NI | VIRT | RES | SHR | %CPU | %MEM | TIME | COMMAND |
| 705 root | 20 | NI | 409956 | 34880 | 33620 | 0.0 | 1.9 | 0:00:04 | sssd |
| 706 root | 20 | NI | 454304 | 34472 | 14304 | 0.0 | 1.8 | 0:00:06 | firewall |
| 725 root | 20 | NI | 611348 | 28244 | 14076 | 0.0 | 1.5 | 0:00:35 | tuned |
| 663 polkitd | 20 | NI | 1907312 | 23876 | 16040 | 0.0 | 1.3 | 0:00:04 | polkitd |
| 718 root | 20 | NI | 600316 | 17176 | 14832 | 0.0 | 0.9 | 0:00:07 | NetworkManager |
```

### 4.3. 按 `T`

| Tasks: 113 total, 2 running, 111 sleeping, 0 stopped, 0 zombie |

| %CPU(s): 7.8/1.5 0 |||||||| 173.7 used |

| Mem: 1829.4 total, 1436.7 free, 219.0 buff/cache |

| Swap: 1024.0 total, 1024.0, 0.0 used 149.7 avail |

| PID PR NI | VIRT | RES | SHR | %CPU | %MEM | TIME | COMMAND |

| 1180 student | 20 | 0 | 222448 | 30816 | 2008 | S | 12.0 | 0.2 | 1:59:04 | process101 |

| 705 root | 20 | 0 | 409956 | 34880 | 33620 | 0.0 | 1.9 | 0:00:04 | sssd |

| 706 root | 20 | 0 | 454304 | 34472 | 14304 | 0.0 | 1.8 | 0:00:06 | firewall |

| 725 root | 20 | 0 | 611348 | 28244 | 14076 | 0.0 | 1.5 | 0:00:30 | tuned |

| 663 polkitd | 20 | NI | 1907312 | 23876 | 16040 | 0.0 | 1.3 | 0:00:04 | polkitd |

| 718 root | 20 | NI | 600316 | 17176 | 14832 | 0.0 | 0.9 | 0:00:07 | NetworkManager |

### 4.4. 按 `Shift+B`

```
top -09:45:28 20 min, 2 users, load average: 0.10, 0.10, 0.04
Tasks: 110 total, 4 running, 106 sleeping, 0 stopped, 0 zombie
CPU(s): 6.8 us, 1.0 sy, 0.0 ni, 92.2 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
Mem: 1829.4 total, 1332.6 free, 175.0 used, 221.7 buff/cache
Swap: 1024.0 total, 1024.0 free, 0.0 used, 1495.3 avail
| PID USER PR | VIRT | RES | SHR | S | %CPU | %MEM | TIME | COMMAND |
| 27179 student | 20 | 0 | 222448 | 30660 | 2812 | R | 15.6 | 0.2 | 1:13:47 | process101 |
```

### 5. 关闭。`top` 配置已停止。确认更改已保存。

#### 5.1. 按 `Shift+B` 切换到关闭。

```
top -19:40:30 6 min, 2 users, load average: 0.11, 0.12, 0.09
Tasks: 112 total, 1 running, 111 sleeping, 0 stopped, 0 zombie
CPU(s): 7.6/1.5
Mem: 182.9/1829.4
Swap: 0.0/1024.0
```

#### 5.2. 按 `Shift+W` 保存此配置。默认配置存储在 `/home/student/.config/procs` 目录下的 `toprc`。在左终端 shell 中，确认它的存在。

```
[student@server ~]$ ls -l /home/student/.config/procs/toprc
-rw-rw-r-- 1 student 966 Feb 18 19:45 /home/student/.config/procs/toprc
```

#### 5.3. 在右终端 shell 中，退出 `top` 并重启。确认新显示使用了保存的配置。

```
top -09:41:30 20 min, 2 users, load average: 0.22, 0.16, 0.08
Tasks: 112 total, 2 running, 110 sleeping, 0 stopped, 0 zombie
CPU(s): 6.8 us, 1.3 sy, 0.9 ni, 91.7 id, 0.0 wa, 0.2 hi, 0.0 si, 0.0 st
Mem: 1829.4 total, 1432.6 free, 175.0 used, 221.7 buff/cache
Swap: 1024.0 total, 1024.0 free, 0.0 used, 1495.3 avail Mem
```

## 6. 将 `process101` 脚本复制到新文件 `process102`。编辑脚本以创建更多人工 CPU 负载。将负载从五万增加到十万。在后台启动 `process101` 进程。

#### 6.1. 在左终端 shell 中，使用 `cp` 命令将 `process101` 复制到 `process102`。

#### 6.2. 使用 `vim` 命令编辑 `process102` 脚本。将加法题从五万增加到十万。使用 `I` 进入交互模式。输入 `:wq` 保存文件。

```bash
[studentserver]$ $ process101
#!/bin/bash
while true; do
var=1
while [[ var -lt 100000 ]]; do
var=$((var+1))
done
sleep 1
done
```

#### 6.3. 在后台启动 `process102`。

```
[studentserver]$ $ process102 & &
[2] 20923
```

#### 6.4. 使用 `jobs` 命令确认两个进程都在后台运行。

```
[studentserver]$ $ jobs          process101 & &
[1]- Running         process102 & &
[2]+ Running
```

# 监控与管理 Linux 进程

```
499 %CPU(s): 0.0 us, 0.0 sy, 0.0 ni, 100 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0
500 Mib 1829.4 total, 1428.7 free, 179.0 used, 221.8 buff/cache
501 Mib 1024.0 total, 1024.0 free, 0.0 used, 1492.1 avail Mem
PID USER PRIRT RESZ SHR %CPU %MEM TIME+ COMMAND
20723 student 20 0 222448 3016 2764 S 24.7 0.2 0:53.28 process102
1180 student 20 0 222448 3056 2068 S 12.0 0.2 0:51.06 process101
...output omitted..
```

> 注意
