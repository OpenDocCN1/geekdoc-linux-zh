
### 6.1 系统启动目标

首先，在列表 6.5 中，`default.target` 单元的文件通过该工具定位，它决定了在系统启动时启动哪些服务。在这种情况下，使用了 `readlink` 命令来查找实际的目标文件，目标单元文件是 `graphical.target`。
同样注意列表 6.5，`systemctl` 命令比另外两个命令要用得多。它只需要 `systemctl get-default`，它就会显示实际的目标文件。由于默认目标文件在不同的发行版中位于不同的目录，因此最好始终使用 `systemctl` 工具。表 6.1 显示了更常用的系统启动单元文件。

#### 表 6.1 常用的系统启动单元文件

| Name | Description |
|---|---|
| `graphical.target` | 提供多用户通过本地终端和/或通过网络访问系统。提供图形用户界面 (GUI) 访问。 |

（续）

#### 表 6.1 常用的启动目标单元文件（续）

| Name | Description |
|---|---|
| `multi-user.target` | 提供多用户通过本地终端和/或通过网络访问系统。不提供 GUI 访问。 |
| `runlevel.target` | 为 SysV init 系统提供向后兼容，其中 `n` 设置为 1-5 以等同于所需的 SysV 运行级别。 |

在表 6.1 中，你会发现 `systemd` 为经典的 SysV init 系统提供了向后兼容性。SysV 运行级别将在本章稍后部分介绍。

`systemd` 配置文件是 `/etc/systemd/system.conf`。在该文件中，你会找到所有的默认配置设置，它们以哈希标记 (`#`) 开头。查看此文件是查看当前 `systemd` 配置的快速方法。如果你需要修改配置，只需编辑该文件。不过，最好通过输入 `man system-conf` 先浏览文件。

## 关注服务文件 (Service Files)

服务单元文件包含信息，例如使用的环境变量、服务何时启动、该服务依赖哪些目标等。这些配置文件位于不同的目录。

请记住，如果文件出现在两个目录位置，其中一个将具有优先级。以下列表显示了按优先级排序的目录：

1. `/etc/systemd/system/`
2. `/run/systemd/system/`
3. `/usr/lib/systemd/system/`

要查看各种服务文件，你可以再次使用 `systemctl` 工具。然而，查看单元时需要稍微不同的命令，如列表 6.6 所示。

#### 列表 6.6: 查看系统单元

```bash
$ systemctl list-unit-files
```

| UNIT FILE | STATE |
|---|---|
| `[...]` | |
| `dev-hugepages.mount` | static |
| `dev-mqueue.mount` | static |

除了单元文件的基础名称，你可以在列表 6.6 中查看单元的状态。这些状态被称为启用状态（enablement states），指的是服务何时启动。有 12 种不同的启用状态，但你经常看到以下三种：

- `enabled`（已启用）：服务在系统启动时。
- `disabled`（已禁用）：服务在系统启动时不启动。
- `static`（静态）：服务当其他单元依赖它时启动。也可以手动启动。

要查看存储特定 `systemd` 单元文件的目录或目录，使用 `systemctl` 工具。CentOS 发行版上的示例见列表 6.7。

#### 列表 6.7: 查找并显示 `systemd` 单元文件

```bash
$ systemctl cat ntpd.service

# /usr/lib/systemd/system/ntpd.service

[Unit]

Description=Network Time Service

After=syslog.target ntpdate.service network.service

[Service]

Type=forking

EnvironmentFile=/etc/config/ntpd

ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS

PrivateTmp=true

[Install]

WantedBy=multi-user.target

$ 
```

请注意列表 6.7，第一显示行显示了 `ntpd.service` 单元文件的名称和目录位置。接下来的几行是单元配置文件的内容。
对于单元文件，主要有三个配置部分，如下：

- `[Unit]`
- `[Service]`
- `[Install]`

在单元配置文件的 `[Unit]` 部分中，有一些基础指令。指令是修改配置的设置，例如列表 6.7 所示的 `After` 设置。最常用的 `[Unit]` 部分在表 6.2 中进行了描述。

#### 表 6.2 常见的服务文件 `[Unit]` 部分指令

| 指令 | 描述 |
| :--- | :--- |
| `After` | 设置此单元在指定的单元之后启动。 |
| `Before` | 设置此单元在指定的单元之前启动。 |
| `Description` | 对单元进行描述。 |
| `Documentation` | 设置一个指向文档源的统一资源标识符 (URL) 列表。这些 URL 可以是网络位置、特定的系统文件、`info` 页面和 `man` pages。 |
| `Conflicts` | 设置此单元不与指定的单元同时启动。如果任何指定的单元启动，则此单元不启动。（`Requires` 的相反。） |
| `Requires` | 设置此单元与指定的单元一起启动。如果任何指定的单元未启动，则此单元不启动。（`Conflicts` 的相反。） |
| `Wants` | 设置此单元与指定的单元一起启动。如果任何指定的单元未启动，此单元仍然会启动。 |

> 在 `systemd` 和单元配置文件的 `man` pages 中有大量有用信息。只需输入 `man -k systemd` 即可找到几个你可以探索的项目。例如，通过 `man systemd.service-command` 探索服务类型单元文件指令及更多内容。你可以在命令行输入 `man systemd.directives` 来查找所有各种指令的信息。

单元文件中的 `[Service]` 指令设置了特定于该服务的配置项。更常用的 `[Service]` 部分指令在表 6.3 中进行了描述。

#### 表 6.3 常见的服务单元文件 `[Service]` 部分指令

| 指令 | 描述 |
| :--- | :--- |
| `ExecReload` | 指明在单元重载时运行的脚本或命令（以及选项）。 |
| `ExecStart` | 指明在单元启动时运行的脚本或命令（以及选项）。 |
| `ExecStop` | 指明在单元停止时运行的脚本或命令（以及选项）。 |
| `Environment` | 设置由空格分隔的环境变量替换符。 |
| `Environment File` | 指明一个包含环境变量替换符的文件。 |
| `RemainAfterExit` | 设置为 `neither`（默认）或 `yes`。如果设置为 `yes`，当由 `ExecStart` 启动的进程终止时，服务将保持激活状态。如果设置为 `no`，则当由 `ExecStart` 启动的进程终止时会调用 `ExecStop`。 |
| `Restart` | 当由 `ExecStart` 启动的进程终止时，服务将重启。如果发出了 `systemctl restart` 或 `systemctl stop` 命令，则会被忽略。设置为 `no`（默认）、`on-success`、`on-failure`、`on-watchdog`、`on-abort` 或 `always`。 |
| `Type` | 设置启动类型。 |

`[Service]` `Type` 指令需要比表 6.3 提供的更详细的解释。该指令可以设置为至少六种不同的规范，这里列出了常见的规范：

- `forking`: `ExecStart` 启动一个父进程。该父进程创建服务的进程作为子进程并退出。
- `simple`:（默认）`ExecStart` 启动服务的主进程。
- `oneshot`: `ExecStart` 启动服务的主进程，该进程通常是一个配置设置或快速命令，然后进程退出。
- `idle`: `ExecStart` 启动服务的主进程，但它会等待所有其他启动作业完成。

# 第 6 章 ■ 维护系统启动与服务

你只会在服务单元文件中找到单元文件的 `[Service]` 部分。这个中间部分对于每个单元类型都不同。例如，在自动挂载单元文件中，你会发现 `[Automount]` 部分作为中间单元文件部分。

另一个需要额外解释的 `[Service]` 配置设置是 `Environment` 指令。Linux 系统使用名为“环境变量”的特性来存储有关 shell 会话和工作环境的信息（因此名为环境变量）。如果你想确保为服务正确设置特定的环境变量，你将希望使用 `Environment` 指令。列表 6.8 显示了 CentOS 发行版上的代码示例。

#### 列表 6.8：查看服务单元文件的 `Environment` 指令

```bash
$ echo $PATH

/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:[...]

$ systemctl --no-pager cat anaconda.service

# /usr/lib/systemd/system/anaconda.service

[Unit]

Description=Anaconda

[...

[Service]

Type=forking

Environment=HOME=/root MALLOC_CHECK=2 MALLOC_PERTURB=204 PATH=/usr/bin:///bin:/sbin:/usr/sbin:/bin:/mnt/sysimage/bin:[...]

LANG=en_US.UTF-8

[...]

$
```

在列表 6.8 中，你可以看到 `PATH` 环境变量的内容显示。该环境变量是一个用冒号分隔的目录列表，进程在其中查找命令。`anaconda.service` 单元文件使用 `Environment` 指令将特定的环境变量设置为其所需的参数。

## 查看 `systemctl`

你可能已经注意到，虽然有很多命令可以管理 `systemd` 和系统服务，但使用 `systemctl` 实用工具更简单更快速。

有几个基本的 `systemctl` 命令可供你管理系统服务。其中常用的是 `status` 命令。它提供了丰富的信息。列表 6.10 展示了在 CentOS 发行版上的两个示例。

#### 列表 6.10：通过 `systemctl` 查看服务单元状态

```bash
$ systemctl status ntpd

- ntpd.service - 网络时间服务
Loaded: loaded (/usr/lib/systemd/system/ntpd.service; disabled; vendor preset: disabled)
Active: inactive (dead)

$ systemctl status sshd

- sshd.service - OpenSSH 服务守护进程
Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
Active: active (running) since Sat 2019-09-07 15:5[...]
Docs: man:sshd(8)
man:sshd_config(5)

Main PID: 1130 (sshd)

Tasks: 1

CGroup: /system.slice/sshd.service

L1130 /usr/sbin/sshd -D

$
```

在列表 6.10 中，第一个 `systemctl` 命令显示了 `ntpd` 服务的状态。注意工具输出的第三行。它显示该服务已禁用（`disabled`）。第四行显示该服务处于非活跃（`inactive`）。本质上，这意味着 `ntpd` 服务没有运行（`inactive`），且没有配置在启动时启动（`disabled`）。`ntpd` 服务状态中另一个需要关注的项是 `Loaded` 行。注意它显示了单元文件的完整名称和目录位置。

同时也显示了 `sshd` 服务的状态，显示 `sshd` 正在运行（`active`）并配置为系统启动时启动（`enabled`）。

你可以使用几个简单的 `systemctl` 工具命令来管理系统服务并查看相关信息。常用的命令如表 6.5 所示。这些 `systemctl` 命令通常使用以下语法：

```bash
systemctl COMMAND UNIT-NAME...
```

## 第 6 章 ■ 维护系统启动和服务

#### 表 6.5 常用 `systemctl` 服务管理命令

| 命令 | 描述 |
|---|---|
| `daemon-reload` | 加载运行的指定单元的单元配置文件，以便在不停止服务的情况下更改单元文件配置。注意这与 `reload` 命令不同。 |
| `disable` | 标记指定单元在系统启动时时不自动启动。 |
| `enable` | 标记指定单元在系统启动时自动启动。 |
| `mask` | 防止指定单元启动。无法使用 `start` 命令或在系统启动时启动该服务。使用 `--mask` 选项也可以立即停止任何运行中的实例。使用 `--running` 选项仅在下次重启或取消掩码前屏蔽服务。 |
| `restart` | 停止并立即重启指定的单元。如果指定单元未启动，则将直接启动它。 |
| `start` | 启动指定的单元。 |
| `status` | 显示指定单元当前状态。 |
| `stop` | 停止指定的单元。 |
| `reload` | 加载运行的指定单元的服务配置文件，以便在不停止服务的情况下更改服务配置。注意这与 `daemon-reload` 命令不同。 |
| `unmask` | 撤销 `mask` 命令对指定单元的影响。 |

注意表 6.5 中 `daemon-reload` 和 `reload` 命令之间的区别。这是一个重要的区别。如果你需要为运行的服务加载系统单元文件配置更改，请使用 `daemon-reload` 命令。使用 `reload` 命令加载修改后的配置文件。例如，如果你修改了 `ntpd` 配置文件 `/etc/ntp.conf`，并希望新配置立即生效，你可以在命令行执行 `systemctl reload ntpd` 命令。

> 警告：在对服务使用 `systemctl mask` 命令时。这会将服务链接到 `/dev/null`（黑洞）以防止任何形式的服务启动。这被描述为“第三级关闭”。你将无法手动启动该服务。此外，如果你在使用 `mask` 时没有使用 `--running` 选项，该服务在启动时也不会启动。你可以通过对它使用 `systemctl unmask` 命令来重新启用启动服务的能力。

除了表 6.5 中的命令外，还有一些实用的 `systemctl` 命令可以用于管理系统服务。CentOS 发行版上的示例如列表 6.11 所示。

#### 列表 6.11：通过 `systemctl` 判断服务是否正在运行

```bash
### systemctl stop sshd

#

### systemctl is-active sshd

inactive

#

### systemctl start sshd

#

### systemctl is-active sshd

active

#
```

在列表 6.11 中，使用 `systemctl` 及其 `stop` 命令停止了 OpenSSH 守护进程（`sshd`）。没有使用 `status` 命令，而是使用 `is-active` 命令快速显示服务已停止（`inactive`）。重启 OpenSSH 服务并再次使用 `is-active` 命令显示服务现在正在运行（`active`）。表 6.6 显示了这些实用的状态检查命令。

#### 表 6.6 方便 `systemctl` 状态检查命令

| 命令 | 描述 |
|---|---|
| `is-active` | 显示单元是活跃还是非活跃。 |
| `is-enabled` | 显示单元是否已启用在启动时启动。 |
| `is-failed` | 显示单元是否处于失败状态。 |

服务可能由于许多原因失败：硬件问题、单元配置中缺少依赖项、设置错误等。你可以使用 `is-failed` 命令查看哪些失败了。（等等，此处 OCR 文本乱码了，根据提供的内容重新对齐）。

*根据提供的文本重新对齐：*

#### 列表 6.11：通过 `systemctl` 判断服务是否正在运行

```bash
### systemctl stop sshd

#

### systemctl is-active sshd

inactive

#

### systemctl start sshd

#

### systemctl is-active sshd

active

#
```

在列表 6.11 中，使用 `systemctl` 及其 `stop` 命令停止了 OpenSSH 守护进程（`sshd`）。没有使用 `status` 命令，而是使用 `is-active` 命令快速显示服务已停止（`inactive`）。重启 OpenSSH 服务并再次使用 `is-active` 命令显示服务现在正在运行（`active`）。表 6.6 显示了这些实用的状态检查命令。

#### 表 6.6 方便 `systemctl` 状态检查命令

| 命令 | 描述 |
|---|---|
| `is-active` | 显示单元是活跃还是非活跃。 |
| `is-enabled` | 显示单元是否已启用在启动时启动。 |
| `is-failed` | 显示单元是否处于失败状态。 |

（注：表 6.6 的 OCR 文本在源文件中是破碎的，根据标准的 `systemctl` 命令重构）。

#### 列表 12：通过 `systemctl` 判断服务是否正在运行

```bash
### systemctl stop sshd

#

### systemctl is-active sshd

inactive

#
```
