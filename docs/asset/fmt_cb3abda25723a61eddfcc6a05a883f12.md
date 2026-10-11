
- `jobs` 显示所有作业

- `jobs -1` 显示所有作业及其 PID

### nohup

**用途：** 运行对挂起信号免疫的进程。

**用法语法：** `nohup [COMMAND] &`

```bash
$ nohup SomeProgram.sh &
nohup: ignoring input and appending output to 'nohup.out'
$ exit
```

使用 `nohup` 命令启动后台程序

`nohup` 命令使进程对挂起信号免疫。挂起信号用于通知 shell 的子进程父进程正在终止。这通常会导致所有子进程终止。使用 `nohup` 可以允许程序在您注销后继续运行，如上述示例所示。

> **提示**
>
> 程序的输出将存储在名为 `nohup.out` 的文件中，该文件位于执行 `nohup` 命令的目录中。

**常见用法示例：**

- `nohup [COMMAND] &` 执行对挂起信号免疫的程序

### at / atq / atrm

**用途：** 调度程序在指定时间运行。

**用法语法：** `at [OPTIONS] [TIME|DATE]`

```bash
$ at 1am
at> MyProgram.sh
at> <CTRL + D>
job 1 at Sat May 30 01:00:00 2009
```

使用 `at` 命令调度进程

`at` 命令调度程序在指定时间运行。在上面的示例中，使用 `at` 命令启动名为 `MyProgram.sh` 的 shell 脚本。在此示例中，命令行指定的启动时间为凌晨 1 点。您还可以使用更传统的 Unix 时间指定方式，例如 01:00 或任何其他 HH:MM 组合。

> **提示**
>
> `at` 命令有一个名为 `now` 的特殊命令行参数。
>
> 这可以用作快捷方式，在调度作业时节省时间。例如，输入 `at now + 15 minutes` 将调度作业在当前时间 15 分钟后启动。

`atq` 命令显示队列中 `at` 作业的信息，如下一个示例所示。

**用法语法：** `atq`

```bash
$ atq
1 Sat May 30 01:00:00 2009 MyProgram.sh nick
```

使用 `atq` 命令显示作业队列

`atrm` 命令删除已调度的作业，如下一个示例所示。

**用法语法：** `atrm [JOBID]`

```bash
$ atrm 1
```

使用 `atrm` 命令移除已调度的作业

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `at [TIME]` | 调度程序在指定时间运行 |
| `atq` | 显示 `at` 作业队列 |
| `atrm [JOBID]` | 从 `at` 队列中移除已调度的作业 |

### batch

**用途：** 在 CPU 负载较低时安排程序运行。

**使用语法：** `batch [OPTIONS]`

```
$ batch 
tag> BigProgram.sh
tag> <CTRL + D>
job 1 at Fri May 29 20:01:00 200
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_119_0.png)

`batch` 命令用于安排程序在系统 CPU 负载较低时运行。这对于运行那些通常会影响系统性能的资源密集型程序非常有用。

在此示例中，使用 `batch` 程序来安排 `BigProgram.sh` 脚本在系统 CPU 负载较低时运行。

> **注意** 每个平台对“低负载”的定义各不相同。有关系统中 `batch` 命令用法的更多信息，请参阅 `man batch`。

**常见用法示例：**

- `batch` | 启动批量调度 shell

### crontab

**用途**：在指定时间安排程序运行。

**使用语法**：`crontab [OPTIONS]`

```bash
# crontab -l
30 12 * * 1-5 /root/SomeProgram.sh
```

显示已配置的 cron 任务

`crontab` 命令用于管理用户的计划 cron 任务。`Cron` 是大多数 Unix、Linux 和 BSD 系统上存在的一个子系统，用于按特定间隔安排程序运行。它与前面讨论的 `at` 命令不同，因为 `cron` 任务以重复的间隔运行（而 `at` 任务只运行一次）。

> 注意 `Cron` 这个名字源自希腊语单词 "chronos"，意思是“时间”。

在上述示例中，`-l` 选项用于显示当前用户的 `crontab`。下表描述了 `crontab` 文件中包含的字段。

| 分钟 | 小时 | 月中的日期 | 月份 | 星期几 | 程序 |
| :---: | :---: | :---: | :---: | :---: | :---: |
| 30 | 12 | * | * | 1-5 | /root/SomeProgram.sh |

`Crontab` 字段

在此示例中，`SomeProgram.sh` 将在每周一至周五下午 12:30 运行。星期几用数字表示，0=周日，1=周一，2=周二，等等。星号 (*) 是一个通配符，代表所有有效值。

`crontab -e` 用于编辑当前用户的 `crontab`，如下一个示例所示。

```bash
# crontab -e
30 12 * * 1-5 /root/SomeProgram.sh
```

编辑 `crontab`

**常见用法示例**：

- `crontab -l` | 列出当前用户的 `crontab`

- `crontab -e` | 编辑当前用户的 `crontab`

- `crontab -r` | 删除当前用户的 `crontab`

### 第 7 节：启动和关机

#### 概述

本章介绍了用于启动和关机 Unix、Linux 和 BSD 系统的命令。它还概述了流行平台的特定平台服务控制命令。

#### 本节涵盖的命令：

| 命令 | 用途 |
| --- | --- |
| shutdown | 关闭系统。 |
| poweroff | 关闭系统电源。 |
| reboot | 重启系统。 |
| halt | 停止系统。 |
| telinit | 更改运行级别。 |
| runlevel | 显示前一个和当前的运行级别。 |
| service | 管理 Linux 系统上的服务。 |
| sysv-rc-conf | 显示和编辑 Linux 运行级别配置。 |
| chkconfig | 显示和编辑基于 Red Hat Linux 系统上的运行级别配置。 |
| rc-update | 显示和编辑 Gentoo Linux 系统上的运行级别配置。 |
| rc-status | 显示 Gentoo Linux 系统上服务的状态。 |
| stopsrc, startsrc | 停止/启动 AIX 系统上的服务。 |
| lssrc | 显示 AIX 系统上服务的状态。 |
| svcs | 显示 Solaris 系统上服务的状态。 |
| svcadm | 启动/停止 Solaris 系统上的服务。 |

#### 本节使用的术语表：

**Init** (INITialization) 一个控制 Unix、Linux 和 BSD 系统启动（也称为初始化）的程序。

**运行级别 (Runlevel)** 一组由 `init` 程序使用的配置文件，定义了系统启动期间（或由 `telinit` 命令调用时）要加载的程序和服务。

**服务 (Service)** 提供服务的系统程序，如 Web 服务器、DNS 服务器、邮件服务器等。服务有时也被称为守护进程或服务守护进程。

### shutdown

**用途：** 关闭系统。

**使用语法：** `shutdown [OPTIONS] [TIME] [MESSAGE]`

```
# shutdown now
BROADCAST MESSAGE FROM ROOT:
The system is going down for shutdown now!
* Stopping services                       [  OK  ]
* Terminating processes                   [  OK  ]
...
The system will now halt.
```

`shutdown` 命令的示例输出

`shutdown` 命令用于关闭本地系统。可以执行几种不同类型的关机：`halt`（停止）、`poweroff`（断电）和 `reboot`（重启）。

> **注意**
>
> `shutdown` 命令的用法在不同的 Unix、Linux 和 BSD 平台之间有所差异。本页面上的示例适用于 Linux 系统。要获取特定于您环境的用法示例，请在本地系统上键入 `man shutdown`。

当执行 `shutdown` 命令时，会向登录到本地系统的所有用户广播警告。可以在时间参数后面指定一条可选消息，如下一个示例所示。
