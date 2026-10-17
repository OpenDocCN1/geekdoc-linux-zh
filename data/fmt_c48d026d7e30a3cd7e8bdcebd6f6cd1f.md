
如果你的 cron 任务是一个脚本，请确保其具有可执行权限（`chmod +x`），否则 cron 将无法执行它。或者，设置 cron 命令通过 shell 运行你的脚本（例如 `bash -c /bin/myscript.sh`）。

## systemd timers 的结构

一个 systemd 定时器包含两个文件：

- 定时器描述计划
- 服务单元指定要运行的内容

与 crontab 条目相比，systemd 定器既可以用绝对日历术语描述，也可以用相对术描述。表 4.6 systemd 定器类型

| 类型 | 描述 |
| :--- | :--- |
| `OnActiveSec` | 相对于激活 |
| `OnBootSec` | 相对于启动 |
| `OnStartSec` | 相对于开始 |
| `OnActiveSec` | 相对于上次活跃 |
| `OnInactiveSec` | 相对于上次非活跃 |
| `OnCalendar` | 特定的日期和时间 |

输出列出了定时器的名称以及它激活的服务名称。下面，我们使用 `systemctl` 命令列出所有定义的定时器。

```bash
systemctl list-timers
UNIT                         NEXT             LEFT             LAST             PASSED
systemd-tmpfiles.timer      Sun 2017-06-18 10:24:33  18h             Sat 2017-06-17 00:45:29  15h
```

## 第 4 章进程控制

要创建你自己的定时器，请将 `.timer` 和 `.service` 文件存放在 `/etc/systemd/system` 中。如果你需要定时器在启动启动时运行，请在定时器单元文件的末尾添加

```
[Install]
WantedBy=multi-user.target
```

不要忘记在启动时使用 `systemctl enable` 启用定时器。（你也可以通过 `systemctl start` 立即启动定时器。）

定时器的 `AccuracySec` 属性会在指定的窗口期内随机延迟一段时间，以推迟其激活。当定时器运行在大量网络化机器上，且你希望避免定时器在同一时刻触发时，此功能非常有用。（请记住，在 cron 中，你需要使用随机延迟脚本来实现这一点。）

`AccuracySec` 默认值为 60 秒。如果你想让定时器在预定时间精确执行，请使用 `AccuracySec=1ns`。（一个纳秒可能足够了。请注意，你并不会实际获得纳秒级的精度。）

### systemd 时间表达式

定时器允许灵活地指定日期、时间和间隔。`systemd.time` 手页是该规范语法的权威参考。

你可以使用间隔值表达式而不是秒来用于相对时间计时，例如作为 `OnActiveSec` 和 `OnBootSec` 的值时。例如，以下内容都是有效的：

- `OnBootSec=2h 1m`
- `OnStartupSec=1week 2days 3hours`
- `OnActiveSec=1hr20m30sec10msec`

时间表达式中的空格是可选的。最小粒度是纳秒，但如果你的定时器触发过于频繁（每两秒超过一次），systemd 会临时禁用它。

除了按周期间隔触发外，还可以通过包含 `OnCalendar` 选项调度定时器在特定时间激活。此功能与传统 cron 任务语法最匹配，但其语法更具表达力且灵活。表 4.7 显示了可以作为 `OnCalendar` 值的时间规范示例。

在时间表达式中，星号 `*` 是匹配任何合理值的占位符。与 crontab 文件一样，斜杠 `/` 表示增量值。然而，具体的语法与 crontabs 中使用的有所不同：crontabs 要求增量对象是一个范围（例如 `9-17/2`，表示“上午 9 点到下午 5 点之间每两小时”），但 systemd 时间表达式仅接受一个起始值（例如 `9/2`，表示“每两小时”）。

### 表 4.7 systemd 时间和日期编码示例

| 时间规范 | 含义 |
|---|---|
| `2017-07-04` | 2017年7月4日 00:00:00（午夜） |
| `Fri-Mon -*-7-4` | 每年的 7 月 4 日，但仅当落在周五至周一时 |
| `Mon-Wed -*---* 12:00:00` | 周一、周二和周三的正午 |
| `Mon 17:00:00` | 周一下午 5 点 |
| `weekly` | 周一的 00:00:00（午夜） |
| `monthly` | 每月 1 号的 00:00:00（午夜） |
| `*:0/10` | 每 10 分钟一次，从第 0 分钟开始 |
| `*--* 11/12:10:0` | 每天 11:10 和 23:10 |

### 瞬态定时器

你可以使用 `systemd-run` 命令根据任何标准的 systemd 定时器类型调度命令的执行，而无需创建特定任务的定时器和服务单元文件。例如，每十分分钟拉取一次 Git 仓库：

```
$ systemd-run --calendar=*:0/10* /bin/sh -c "cd /app && git pull"
Running timer as unit run-8823.timer.
Will run service as unit run-8823.service.
```

systemd 返回一个瞬态单元标识符，你可以使用 `systemctl` 列出它。（再次，我们对下面的输出格式进行了模糊测试……）

```
$ systemctl list-timers run-8823.timer
NEXT      Sat 2017-06-17 20:40
LEFT      -
LAST      Sat 2017-06-17 20:40
ACTIVE    active (1min ago)
PASSED     
```

```
$ systemctl list-timers run-8823.timer
NEXT      Sat 2017-06-17 20:40
LEFT      -
LAST      Sat 2017-06-17 20:40
ACTIVE    active (1min ago)
PASSED     
```

```
$ systemctl list-timers run-8823.timer
NEXT      Sat 2017-06-17 20:40
LEFT      -
LAST      Sat 2017-06-17 20:40
ACTIVE    active (1min ago)
PASSED     
```
