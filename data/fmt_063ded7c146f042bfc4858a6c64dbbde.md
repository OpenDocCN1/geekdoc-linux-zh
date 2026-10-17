
```bash
#!/bin/bash
# Script submit_host_check
printf="/usr/bin/printf"
CMD="/usr/local/bin/send_nsca"
CFG="/etc/nagios/send_nsca.cfg"
HOST=$1
RESULT=$2
OUTPUT=$3
```

唯一缺失的是服务的描述。根据 Nagios 文档，最好将这两个脚本存储在插件目录的 `eventhandlers` 子目录下（通常需要创建），插件目录通常为 `/usr/local/nagios/libexec`，但在某些发行版中为 `/usr/lib/nagios/plugins/`。你可以通过匹配命令对象的宏 `$USER15$` 从中获取此内容。这最好定义在 `miscommands.cfg` 文件中：

```
define command {
  command_name submit_service_check
  command_line $USER15$/eventhandlers/submit_service_check $HOSTNAME$ '$n$SERVICEDESC$ '$SERVICESTATEID$ '$SERVICEOUTPUT$'
}
```

```bash
define command/
  command name submit_host_check
  command_line $USER$/eventhandlers/submit_host_check $HOSTNAME $HOSTSTATEID$
  '$HOSTOUTPUT$'
```

如果你为此项操作使用单独的文件，则你必须通过向 `/etc/nagios/nagios.cfg` 添加条目，确保确保 Nagios 会加载该文件。包裹在 `$SERVICEDESC$` 宏和 `command_line` 行中两个输出宏周围的单引号非常重要。它们的值有时包含空格，如果没有引号，命令行将会将这些空格解释为分隔符。

### 15.3 实际场景

分布式监控的一个应用场景是监控分支机构或外部办公室，在这些地方，非中心化的安装仅限于运行服务检查和主机检查，并将结果发送给中心实例。非中心实例不需要进一步的 Nagios 功能，例如通知系统或 Web 界面。

另一方面，如果由管理员负责分布式地点的网络维护，而中央 IT 部门仅负责特殊服务，那么非中心的 Nagios 服务器将会被配置为正常的、功能完备的安装，并通过 OSP/OCHP 机制选择性地仅将专家负责的检查结果转发到中心办公室。

无论何种情况，你必须确保检查项和服务在非中心和中心都是可用的。可以使用模板（第 75 页的 2.11 模板）和 `cfg_dir` 指令（2.1 主配置文件 `nagios.cfg`，第 55 页）简单地实现：你设置定义使得配置文件可以被复制：1.

## 15.3 避免配置文件的冗余

在以下示例中，我们假设非中心服务器仅执行主机和服务检查，并将结果发送到中心服务器，而不提供任何其他 Nagios 功能。在中心主机上设置了以下目录：

```
/etc/nagios/global
/etc/nagios/local
/etc/nagios/sites
/etc/nagios/sites/bonn
/etc/nagios/sites/Frankfurt
/etc/nagios/sites/berlin
...
```

用于每个地点的配置都位于 `/etc/nagios/sites/location` 目录下。在 `global` 之后，所有可以在所有地点相同地使用的定义（例如 `checkcommands.cfg` 中的命令定义）。该目录包含了中心服务器定义的特定定义。这些包含了服务和主机的模板，在其中必须区分非中心和中心。

此目录在非中心服务器上也被单独创建：仅从中心实例拷贝 `global` 和 `sites/location` 文件夹到分支机构。

这三个目录是通过 `/etc/nagios/nagios.cfg:` 中的 `cfg_dir` 指令进行读取的：

```bash
# # /etc/nagios/nagios.cfg
...
cfg_dir=/etc/nagios/global
cfg_dir=/etc/nagios/local
cfg_dir=/etc/nagios/sites
...
```

在服务定义中，只有非中心和中心页面相同的设置会被使用：

```bash
# /etc/nagios/sites/bonn/services.cfg
define service{
host_name bonn01
service_description HTTP
use bonn-svc-template
...
check_command           check_http
}
```

依赖于地点的参数通过模板来处理。

### 15.3.2 定义模板

为了使服务定义在中心和非中心服务器上一致，本地模板的名称必须与中心模板相同。你应该确保输入所有强制参数（第 53 页的第 2 章），即使这些参数在其中一个地点不是必需的，因为模板和服务的定义必须共同覆盖所有强制参数。

以下示例显示了一个用于非中心地点的服务模板：

```bash
# -- 波恩地点的现场配置
define service{
name                    bonn-svc-template
register                0
max_check_attempts     3
normal_check_interval   5
retry_check_interval    1
active_checks_enabled   1
passive_checks_enabled  1
check_period            24*7
obsess_over_services    1
notification_interval  0
notification_period    none
notification_options   n
notifications_enabled  0
contact_groups          dummy
}
```

对于非中心页面重要的参数以粗体打印。除了测试本身，`notifications_enabled` 会关闭活动测试。这只有当 Nagios 服务器本身处于位置 `/etc/nagios.cfg`（此处原文可能有误）时才有效。

中心服务器上同名的对应项如下：

```bash
# -- 中心服务器的服务模板
define service{
name                    bonn-svc-template
register                0
max_check_attempts     3
normal_check_interval   5
retry_check_interval    1
active_checks_enabled   1
passive_checks_enabled  1
check_period            none
obsess_over_services    0
notification_interval  480
notification_period    24*7
notification_options   u,c,r
notifications_enabled  1
contact_groups          admins
}
```

然而，在示例中，我们在波恩地点完全关闭了活动测试，将 `check_period none` 和 `check_freshness` 设置为 0。当然，到为止描述的系统也可以应用于主机检查。

# Nagios

### 通用

- 文档
- 帮助

## 监控

- 命令状态
- 服务详情
- 主机组浏览器
- 监控中心
- 服务组概览
- 服务组详情
- 服务组网格
- JBRD 状态图
- 服务性能
- 未授权
- 性能更新
- 网络状态

### 配置

- 编辑
- 注释
- 时间线轴

### 报告

- 事件
- 警报历史
- 警报列表
- 警报摘要
- 事件日志

### 配置

- 查看全部

Copyright (c) 1999-2007 Ethan Galstead

版本 3.0rc1

2007年12月17日

> 如果您已安装了 Nagios，请阅读文档以获取让一切运行起来的说明。

点击此处查看此版本中新增的特性简要概述。

更多信息：

访问 Nagios 首页页 http://www.nagios.org 获取有关错误修复、升级、支持等信息。

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_343_0.png)

图 16-1. 在“服务问题”和“主机问题”菜单项下的“未处理（Unhandled）”子项自 Nagios 3.0 以来一直显示在 Nagios Web 界面的起始页。

# 表 16-1. CGI 程序概览

| CGI 程序 | 描述 |
|---|---|
