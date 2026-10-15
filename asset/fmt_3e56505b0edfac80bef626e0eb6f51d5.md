
注意：`wtmp` 文件增长得非常快。你可能需要经常修剪它。

GNU `ac` 的工作原理与 `uix ac` 几乎相同，尽管它在某些方面更智能。因此，你应该预期 GNU `ac` 的输出与其他系统上 `ac` 的输出存在差异。使用命令 `info accounting` 来获取更多信息。

### 选项

- `-d`, `--daily-totals`

  打印每天的总计，而不是在最后只打印一个大总计。输出如下：Jul 3 total 1.17 Jul 4 total 2.10 Jul 5 total 8.23 Jul 6 total 2.10 Jul 7 total 0.30

- `-p`, `--individual-totals`

  除了通常的合并值外，还打印每个用户的时间总计。看起来像：bob 8.06 goff 0.60 maley 7.37 root 0.12 16.15

- `people`

  打印 `people` 中包含的所有用户使用的连接时间总和。注意，`people` 是用空格分隔的有效用户名列表；不允许通配符。

- `-f`, `--file filename`

  从文件 `filename` 而不是系统的 `wtmp` 文件读取。

- `--complain`

  当 `wtmp` 文件出现问题时（时间回溯、记录丢失或任何情况），打印适当的错误。

- `--reboots`

  重启记录不是在重启时写入，而是在系统启动时写入；因此，无法确切知道重启发生的时刻。用户可能在重启时登录系统，`ac` 会自动将登录和重启记录之间的时间计入用户（尽管可能应该这样做，例如如果系统关机很久）。如果你想计算这段时间，请包含此标志。*对于原生 ac*

- `--supplants`

  有时

- `--timewraps`

  有时，`wtmp` 文件中的项会突然跳回过去，而没有发生时钟更改记录。无法在这种情况下用户登录了多久。如果你想将登录和时间回溯之间的时间计入用户，请包含此标志。*为了兼容原生 ac，请包含此标志。*

- `--compatibility`

  这是输入上述三个选项的简写。

- `-a`, `--all-days`

  如果我们打印每日总计，则打印每一天的记录，而不是跳过没有登录活动的中间日期。如果没有此标志，这些中间日期积累的时间将被列出。

- `--lenency num`

  将容忍度设置为 `num`。

- `--suspicious num`

  将可疑度设置为 `num`。

- `-z|print-zeros`

  打印零。

- `--debug`

  调试。

- `-V|version`

  打印版本。

- `-h|--help`

  打印帮助信息

- 文件

  `wtmp` 文件

- 作者

  会计工具由 Noel Cragg 编写。

- 另请

  `login(1)`, `wtmp(5)`

### 参见

`aseqnet(1)`, `aseqview(1)`

### 作者

Takashi Iwai <tiwai@suse.de>

## 名称

`afs5log` - AFS 令牌初始化器

### 概要

```
afs5log [[ -v] [-5] [-k] [-p path] [cell[=principal]] ] ] [...]
```

### 描述

`afs5log` 命令使用 Kerberos 为指定的单元获取 AFS 令牌。如果没有指定单元，则为本地单元获取令牌。如果已知 af 服务的主体名称（principal name），也可以以 `cell=principal_name` 的形式给出单元名称。程序会尝试先获取 Kerberos IV 凭据，如果失败，`afs5log` 将创建 Kerberos 5 (2b样式) 令牌。

### 参数

`-v`

开启详细输出模式。`afs5log` 在工作时将打印调试信息。多次使用该选项可获取更详细的信息。

- `-p path`

确定指定路径所在的单元，并为该单元获取令牌。

- `-s strategy`

用指定的策略覆盖默认的令牌设置策略（“2b”）。识别的策略名称包括：`rx5` `rxk5`（需要 OpenAFS 1.6 或更高版本），`2b` `rxkad` “2b”（需要 OpenAFS 1.2.8 或更高版本）。

- `-5`

跳过使用 Kerberos IV 的尝试，仅使用 2b 样式令牌，该令牌仅支持 OpenAFS 1.2.8 及更高版本。

- `-k`

跳过使用 Kerberos IV 的尝试并使用 `rxk5` 样式令牌，该令牌仅支持 OpenAFS 1.6 或更高版本。

- `-n`

假设如果单元名称和领域（realm）名称仅大小不同，则 AFS 服务的主体名称不包含实例。

### 参见

`pam_krb5(5)` `krb5.conf(5)`

## 缺陷

可能存在，但我们希望没有。如果你发现任何问题，请在 `http://bugzilla.redhat.com/` 针对“`pam_krb5`”组件提交 bug 报告。

### 作者

Nalin Dahyabhai <nalin@redhat.com>

## ALSACTL

## 名称

`alsactl` - ALSA 声卡驱动的高级控制

### 概要

```
alsactl [options] [store|restore|init] <card # or id or device>
```

```
alsactl monitor <card # or id>
```

### 描述

`alsactl` 用于控制 ALSA 声卡驱动的高级设置。它支持多个声卡。如果你的声卡具有某些似乎无法从混合器应用程序中控制的功能，那么你来对地方了。

### 命令

`store` 将所选声卡的当前驱动状态保存到配置文件中。

`restore` 从配置文件加载所选声卡的驱动状态。如果恢复失败（最终是部分失败），将调用 `init` 操作。

`nstore` 类似于 `restore`，但还会通知守护进程对可用声卡进行新的重新扫描。

`init` 尝试将所有设备初始化为默认状态。如果设备未知，则返回错误代码 99。

`daemon` 定期保存声音状态。

`rdaemon` 类似于 `daemon`，但会先恢复声音状态。

`kill` 通知守护进程执行指定操作（退出、重新扫描、保存并退出）。

`monitor` 用于监控从给定控制设备接收到的事件。

如果没有指定声卡，将对所有声卡的设置进行保存、加载或监控。

### 选项

`-h`, `--help`

帮助：显示可用标志和命令。

`-d`, `--debug`

使用调试模式：更详细。

`-v`, `--version`

打印 `alsactl` 版本号。

- `-f`, `--file`

选择使用的配置文件。默认是 `/var/lib/alsa/asound.state`。

- `-l`, `--lock`

使用文件锁来序列化对状态文件的并发访问（这是全局状态文件的默认设置）。

- `-L`, `--no-lock`

不使用文件锁序列化对状态文件的并发访问（包括全局状态文件）。

- `-O`, `--lock-state-file`

选择状态锁文件路径。

- `-F`, `--force`

配合 `restore` 命令。尽可能恢复匹配的控制元素。此选项现设置为默认值。

- `-g`, `--ignore`

配合 `store` 和 `restore` 命令。当未安装声卡时不显示“未找到声卡”且不设置错误退出状态码。

- `-P`, `--pedantic`

配合 `restore` 命令。不恢复不匹配的控制元素。这是是旧的默认行为。

- `-I`, `--no-init-fallback`

如果恢复失败，不初始化声卡。从 1.0.18 版本开始，`alsactl` 尝试将恢复操作作为默认来初始化卡。但这可能与旧版本不兼容。调用者可能期望在不存在状态文件时不触碰状态。此选项通过抑制初始化将恢复行为回退到旧版本。

- `-r`, `--runstate`

将恢复和初始化状态保存到此文件。该文件仅包含错误。错误会在文件末尾附加声卡 ID。

- `-R`, `--remove`

先删除 `runstate` 文件。

- `-E`, `--env=#`

设置环境变量（用于 `init` 操作，或你可以覆盖 `ALSA_CONFIG_PATH` 以读取不同的或优化的配置 - 可能对“启动”脚本有用）。

- `-i`, `--initfile`

`init` 的配置文件。默认使用 `PREFIX/share/alsa/00main`。

- `-p`, `--period`

`daemon` 命令的存储周期（秒）。

- `-e`, `--pid-file`

存储进程 ID 文件的路径，采用 UUCP 格式（ASCII）。

- `-b`, `--background`

在后台运行任务。

- `-s`, `--syslog`

使用 `syslog` 消息。

- `-c`, `--sched-idle`

将进程调度策略设置为空闲（`SCHED_IDLE`）。

### 文件

`/var/lib/alsa/asound.state`. 使用的配置文件。默认是 `/var/lib/alsa/asound.state`。

### 参见

`pam_krb5(5)` `krb5.conf(5)`

# 缺陷

可能存在，但我们希望没有。如果你发现任何问题，请在 `http://bugzilla.redhat.com/` 针对“`pam_krb5`”组件提交 bug 报告。

### 作者
