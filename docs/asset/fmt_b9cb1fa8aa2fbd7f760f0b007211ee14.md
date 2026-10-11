
# Linux 管理：入门指南

`initctl` 命令可用于显示所有作业及其状态的列表。例如，要列出所有作业及其状态，请运行：

```
[root@serverA ~]# initctl list
```

## /etc/inittab 文件

`/etc/inittab` 文件包含了 `init` 启动运行级别所需的所有信息。该文件中每行的格式如下：

```
id:runlevels:action:process
```

> 提示：以井号 (`#`) 开头的行是注释。看一眼你自己的 `/etc/inittab`，你会发现它已经包含了大量的注释。如果你以后需要更改 `/etc/inittab`，包含大量的注释来解释你正在做什么将对你自己有所帮助。

表 8-1 解释了 `/etc/inittab` 文件中条目四个字段的每一个意义，而表 8-2 定义了该文件中 `action` 字段可用的一些常用选项。

| /etc/inittab 项目 | 描述 |
| :--- | :--- |
| `id` | 一到四个字符的唯一序列，用于标识 `/etc/inittab` 文件中的此条目。 |
| `runlevels` | 应该调用进程的级别。某些事件非常特殊，可以在所有级别下被捕获（例如用于重启的 CTRL-ALT-DEL 组合键）。要表示一个事件适用于所有运行级别，请将 `runlevels` 留空。如果你想让某事在多个运行级别发生，只需在该字段中列出所有级别即可。例如，`runlevels` 条目 `123` 指定在运行级别 1、2 或 3 下运行的内容。 |
| `action` | 描述应该采取的动作。该字段的选项在下一个表中解释。 |
| `process` | 指定进入运行级别时要执行的进程（或程序）。 |

表 8-1. `/etc/inittab` 条目

| 字段 | 描述 |
| :--- | :--- |
| `action` in `/etc/inittab` | 进程每当终止时将重启。 |
| `respawn` | 进程在进入运行级别后将启动一次，`init` 将等待其完成。 |
| `once` | 进程在进入运行级别后将启动一次；然而，`init` 在可能执行该运行级别下的其他程序之前，不会等待进程终止。 |
| `boot` | 进程将在系统启动时执行。在这种情况下，`runlevels` 字段被忽略。 |
| `bootwait` | 进程将在系统启动时执行，`init` 将等待启动完成后再进入下一个要运行的进程。 |
| `ondemand` | 进程将在特定运行级别发生时执行。（这些运行级别是 a、b 和 c）运行级别不会发生变化。 |
| `initdefault` | 指定 `init` 启动时的默认运行级别。如果没有指定默认值，则会在控制台上提示用户输入运行级别。 |
| `sysinit` | 进程将在系统启动期间执行，在任何 `boot` 或 `bootwait` 条目之前执行。 |
| `powerwait` | 如果 `init` 接收到来自另一个进程关于电源问题的信号，此进程将等待该进程完成。 |
| `powerfail` | 与 `powerwait` 相同 |
| `powerok` | 与 `once` 相同，`init` 在可能执行该运行级别下的其他程序之前，不会等待进程终止。 |

表 8-2. 此文件中 `action` 字段的可用选项

在本节中，我们将介绍新的 `xinetd` 守护进程。如果你的系统使用 `inetd`，你应该能够查看 `/etc/inetinetd.conf` 文件，并看到 `inetd` 和 `xinetd` 之间的相似之处。

注意：你的 Linux 发行版可能没有默认安装 `xinetd` 软件。可以通过运行以下命令在 Fedora 发行版（或 RHEL, Centos）上使用 `yum` 安装 `xinetd` 软件包：

```
yum install xinetd
```

在像 Ubuntu 等基于 Debian 的发行版上，可以通过运行以下命令安装 `xinetd`：

```
sudo apt-get install xinetd
```

# /etc/xinetd.conf 文件

`/etc/xinetd.conf` 文件由一系列格式如下的块组成：

```
blockname

{

  variable = value

}
```

其中，`blockname` 是正在定义的块的名称，`variable` 是在块范围内定义的变量名称，`value` 是赋值给变量的值。每个块内部都可以定义多个变量。
有一个特殊的块被称为 `defaults`。在此块中定义的任何变量都会应用于文件中定义的所有块。
块格式的一个异常是 `includedir` 指令，它告诉 `xinetd` 去读取目录下的所有文件，并将其视为 `/etc/xinetd.conf` 文件的一部分。任何以井号 (`#`) 开头的行都是注释的开始。Fedora 自带的默认 `/etc/xinetd.conf` 文件如下所示：

```
# 这是主 xinetd 配置文件。

# default 部分中的设置将被所有服务配置继承-
defaults{

  instances = 50

  log_type = SYSLOG daemon info

  log_failure = HOST

  log_success = PID HOST DURATION EXIT

  cps = 50 10

}

includedir /etc/xinetd.d
```
